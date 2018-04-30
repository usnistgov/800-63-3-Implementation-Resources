## 4 Authenticator Assurance Levels

The following sections provide some further description of the authenticator assurance levels (AALs) and in particular how the particular authenticator combinations permitted at each AAL were arrived at. As with the rest of these implementation resources, these descriptions are only informative; refer to SP 800-63B for normative guidelines.

It is the intent of SP 800-63B to permit the use of a higher-AAL authenticator or combination of authenticators to authenticate a session at a lower AAL. While the user experience with a higher-AAL authenticator is often more complex, it is frequently more convenient not to maintain and use different authenticators for lower AAL(s).

Even if a higher-AAL authenticator is used, other characteristics of the authenticated session such as reauthentication time are determined by the session AAL, not by the type of authenticator used. For example, if an AAL3-capable authenticator is used in an AAL1 session, the AAL1 reauthentication requirements apply.

SP 800-63B encourages the binding of multiple authenticators with a subscriber account. For an application requiring a given authenticator assurance level, all authentication transactions that are able to access the application are required to be of at least the specified AAL. This includes authenticators that are used for “account recovery” when another authenticator is not available (typically a forgotten memorized secret). Another way to look at it is that the minimum AAL of all the authenticators or combinations of authenticators used to access the application (the “low-water mark”) is the maximum AAL that the application can require.

### 4.1 Authenticator Assurance Level 1

AAL1 permits single-factor authentication using a wide variety of authenticators listed in SP 800-63B Section 4.1.1. By far the most common authenticator at AAL1 is the memorized secret, but it is equally acceptable to use a physical authenticator such as an OTP device at AAL1. When multifactor authenticators are used at AAL1, the nature of those devices requires that the additional factor, i.e., a memorized secret or biometric, be provided to allow those authenticators to operate.

Biometrics by themselves are not considered authenticators in SP 800-63B because they must always be strongly bound to a physical authenticator and are considered an activation factor for that authenticator. For that reason, a biometric cannot be used alone for authentication, even at AAL1.

### 4.2 Authenticator Assurance Level 2

AAL2 requires the use of two authenticator factors, either a physical authenticator and a memorized secret or a physical authenticator and a biometric that has been associated with it. Multi-factor authentication can be performed using either a multi-factor authenticator or through the use of two independent authenticators.

As detailed in Section 5.2.3 below, there are restrictions on the use of biometrics, in particular that they must be securely bound to a specific physical authenticator. For this reason, a memorized secret plus a biometric is not an acceptable combination for authentication.

Multi-factor authenticators use an additional factor, either something you know or something you have, to unlock a secret that is stored in the (physical) authenticator. This introduces new challenges: How can the verifier determine that two factors were actually used in the authentication? How can the verifier determine that the use of a biometric factor to unlock the authenticator meets the AAL2 performance requirements? If the authenticator is supplied by the CSP (not a “bring your own” authenticator), the verifier of course can be assured that the authenticator meets AAL2 requirements by virtue of its trust relationship with the CSP. User-supplied authenticators that include some sort of attestation of its provenance, such as a certificate signed by the manufacturer, can generally be assumed to meet the specifications presented by that manufacturer. In the absence of this or a similar basis for the verifier to establish the nature of the authenticator, verifiers do not have a basis for assuming that a (purported) multifactor authenticator meets AAL2 requirements.

### 4.3 Authenticator Assurance Level 3

AAL3 introduces several new requirements beyond AAL2, the most significant being the use of a hardware-based authenticator. There are also several additional authentication characteristics that are required:

* Verifier impersonation resistance
* Verifier compromise resistance
* Replay resistance
* Authentication intent

Some of these characteristics are satisfied jointly by the authenticator and verifier, while others are primarily authenticator characteristics. When multiple authenticators are used, these requirements are satisfied by the use of at least one authenticator with the required characteristic. For example, if a hardware-based authenticator that is not verifier impersonation resistant is used, a software-based authenticator that provides verifier impersonation resistance will satisfy that requirement.

#### 4.3.1 Permitted Authenticator Types

SP 800-63B Section 4.3.1 identifies six combinations of authenticators that can meet the requirements of AAL3. There might be additional combinations that work, such as combinations of four or more authenticators to meet all of the AAL3 requirements, but these are unlikely to be used because of the complexity of the user experience.

Even though two authentication factors are required at AAL3, one combination of authenticators (Hardware Single-Factor OTP Device plus a Single-Factor Cryptographic Software Authenticator plus a Memorized Secret) consists of three authenticators. This combination stems from the fact that the hardware-based Single-Factor OTP Devices do not provide verifier impersonation resistance, so a Single-Factor Cryptographic Software Authenticator can satisfy that requirement. But since both of those authenticators are something you have, a Memorized Secret is required to satisfy the requirement for two different authentication factors.

Use of an authenticator or combination of authenticators on this list is not sufficient to meet the requirements of AAL3. For example, a multi-factor cryptographic device does not necessarily provide verifier impersonation resistance nor establish authentication intent. When an authentication system to meet AAL3 is designed, all of the AAL3 requirements need to be examined and satisfied, in addition to the choice of authenticator type(s).

### 4.4 Privacy Requirements

While the privacy requirements in SP 800-63B Section 4.4 are expressed primarily in wording that applies to federal agencies, the requirements are relevant for other uses of authentication as well. A key requirement is that data that is collected be limited to its intended use (authentication) unless the subscriber consents to additional use. Any such additional use must be voluntary, and not be a condition for the use of the service without a strong justification.
