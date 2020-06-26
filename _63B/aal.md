---
layout: default
title:  Authenticator Assurance Levels
permalink: /63B/AAL
navOrder: 3  
navTitle: AAL  
---

# B.3 Authenticator Assurance Levels {#s-b-3}

The following sections provide some further description of the three authenticator assurance levels (AALs) and in particular how the authenticator combinations permitted at each AAL were arrived at. As with the rest of these implementation resources, these descriptions are informative; refer to [SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html#sec4) for normative guidelines.

Authenticator assurance levels are associated with interactive sessions and not with the authenticators themselves. This is because combinations of authenticators, used together, can achieve a higher AAL than individually. On the other hand, some requirements, such as reauthentication time, that are more stringent at higher AALs can limit a given session to a lower AAL than the authenticators themselves might be able to support. So while a multi-factor cryptographic authenticator might be characterized as AAL3-capable, that doesn't mean that any session it is used to authenticate is necessarily AAL3.

## B.3.1 Authenticator Assurance Level 1 {#s-b-3-1}

AAL1 permits single-factor authentication using a wide variety of authenticators listed in [SP 800-63B Section 4.1.1](https://pages.nist.gov/800-63-3/sp800-63b.html#411-permitted-authenticator-types). By far the most common authenticator at AAL1 is the memorized secret, but from the standpoint of meeting AAL1 requirements it is equally acceptable to use a physical authenticator such as an OTP device. Physical authenticators and memorized secrets are, of course, susceptible to different types of threats. When multifactor authenticators are used at AAL1, the nature of those devices requires that the additional factor (a memorized secret or biometric) be provided to allow those authenticators to operate.

Biometrics by themselves are not considered authenticators in SP 800-63B; they must always be strongly bound to a physical authenticator and are considered an activation factor for that authenticator. This mitigates the relatively high false acceptance rate for biometrics and the risks associated with disclosure and non-revocability of biometric data. For that reason, a biometric cannot be used alone for authentication, even at AAL1.

## B.3.2 Authenticator Assurance Level 2 {#s-b-3-2}

AAL2 requires the use of two authentication factors, either (1) a physical authenticator and a memorized secret, or (2) a physical authenticator and a biometric that has been associated with it. Multi-factor authentication can be performed using either a multi-factor authenticator or through the use of two independent authenticators.

As detailed below, there are restrictions on the use of biometrics, in particular that they must be securely bound to a specific physical authenticator. For this reason, a memorized secret plus a biometric is not an acceptable combination for authentication.

In addition to the requirement for two authentication factors at AAL2, there are additional requirements relating to the authentication and the session. These include:
* Shorter reauthentication time
* Replay resistance
* FIPS 140 Level 1 for authenticators supplied by government agencies
* Authentication intent (recommended)

Multi-factor authenticators use an additional factor, either something you know or something you have, to unlock a secret that is stored in the (physical) authenticator.

## B.3.3 Authenticator Assurance Level 3 {#s-b-3-3}

AAL3 introduces several new requirements beyond AAL2, the most significant being the use of a hardware-based authenticator. There are several additional authentication characteristics that are required:

* Verifier impersonation resistance
* Verifier compromise resistance
* Authentication intent

Some of these characteristics are satisfied jointly by the authenticator and verifier, while others are primarily authenticator characteristics. When multiple authenticators are used, these requirements are satisfied by the use of at least one authenticator with the required characteristic. For example, if a hardware-based authenticator that is not verifier impersonation resistant is used, a software-based authenticator that provides verifier impersonation resistance will satisfy that requirement.

### B.3.3.1 Permitted Authenticator Types {#s-b-3-3-1}

[SP 800-63B Section 4.3.1](https://pages.nist.gov/800-63-3/sp800-63b.html#aal3types) identifies six combinations of authenticators that can meet the requirements of AAL3. There might be additional combinations that work, such as combinations of four or more authenticators to meet all of the AAL3 requirements, but these are unlikely to be used because of the complexity of the user experience.

Even though two authentication factors are required at AAL3, one combination of authenticators (Hardware Single-Factor OTP Device plus a Single-Factor Cryptographic Software Authenticator plus a Memorized Secret) consists of three authenticators. This combination stems from the fact that the hardware-based Single-Factor OTP Devices do not provide verifier impersonation resistance, so a Single-Factor Cryptographic Software Authenticator can satisfy that requirement. But since both of those authenticators are something you have, a Memorized Secret is required to satisfy the requirement for two different authentication factors.

Use of an authenticator or combination of authenticators on this list is not itself sufficient to meet the requirements of AAL3. For example, a multi-factor cryptographic device does not necessarily provide verifier impersonation resistance nor establish authentication intent. When an authentication system to meet AAL3 is designed, all of the AAL3 requirements need to be examined and satisfied, in addition to the choice of authenticator type(s).

## B.3.4 Privacy Requirements {#s-b-3-4}

While the privacy requirements in [SP 800-63B Section 4.4](https://pages.nist.gov/800-63-3/sp800-63b.html#aal_privacy) are expressed primarily in wording that applies to federal agencies, the requirements are relevant for other uses of authentication as well. A key requirement is that data that is collected be limited to its intended use (authentication) unless the subscriber consents to additional use. Any such additional use must be voluntary, and not be a condition for the use of the service without a strong justification.
