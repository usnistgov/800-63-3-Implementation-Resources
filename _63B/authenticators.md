---
layout: default
title:  Authenticators
permalink: /63B/Authenticators
navOrder: 4  
navTitle: Authenticators  
---

## Authenticators and Verifiers

See [SP 800-63 B](https://pages.nist.gov/800-63-3/sp800-63b.html#sec5) for normative requirements.

### Authenticator Types

There are nine recognized authenticator types.

Pre-registered knowledge tokens (sometimes referred to as security questions or knowledge-based authentication (KBA)), an authenticator (token) type that existed in SP 800-63-2, has been withdrawn in SP 800-63B because they often rely on information that is private but not secret. They also encourage the use of the same answers to authenticate on multiple sites, which is a problem if any of them is compromised. In addition, they often must be stored in an unhashed form, introducing a further vulnerability, because the recalled answers may be approximate (e.g., "Central High" vs. "Central High School" or "Central HS"). The use of hints in prompts for memorized secrets has also been prohibited because of similar security concerns and the possible use of hints as a work-around to support security questions.

The single-factor cryptographic software authenticator, discussed in [SP 800-63B Section 5.1.6](https://pages.nist.gov/800-63-3/sp800-63b.html#sfcs), is a new authenticator type introduced in SP 800-63B.

#### Memorized Secrets

<div class="text-left" markdown="1">
  <table style="width:100%">
    <tr>
      <td>
        <img src="sp800-63b/media/Memorized-secret.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;">
      </td>
      <td>
        The memorized secret is by far the most common type of authenticator. It is also the only authenticator that is a <i>something you know</i> authentication factor (pre-registered knowledge tokens were also something you know in SP 800-63-2 and earlier editions).
      </td>
    </tr>
  </table>
</div>


The term *memorized secret* was chosen as a single term encompassing passwords, passphrases, and PINs. The intent of a memorized secret is that it be potentially memorable to a subscriber, even if not chosen by the subscriber. This differentiates it from a key, which is never chosen by the subscriber, typically has at least 112 bits of entropy, and therefore is not expected to be memorized nor entered by the average subscriber.

One of the significant changes in SP 800-63B is a rethinking of the role of memorized secrets and minimization of their burden on subscribers. In accordance with Executive Order 13681 [EO 13681], transactions involving any significant risk, including any which involve the release of personal information, require multi-factor authentication. As a result, memorized secrets alone will be used only when a relatively low level of security is required.

Research [find relevant Herley paper] has shown that there is a significant gap between the requirement for memorized secrets that must protect against an offline attack as compared with those that only protect against throttled online attacks. For memorized secrets to be considered secure against current offline attacks, a considerably higher minimum length would be required. Even so, there is no assurance that subscribers would pick memorized secrets that don't lend themselves to automated guessing attacks. Accordingly, a two-pronged approach was adopted:
* Set minimum memorized secret requirements to protect against online attacks only, accept the risk of offline attacks, and throttle online attempts.
* Require verifiers to implement secure hashing of memorized secrets, including iterated hashing with a salt, and recommend hashing with a secret value as well.

This puts the burden on the verifier, rather than the subscriber, to the maximum extent possible.

At the same time, SP 800-63B attempts to make it as easy as possible for a subscriber to choose a memorized secret that is as secure as possible. Because memorized secrets are required to be hashed before storage by the verifier, the length of the stored value is independent of the length of the memorized secret. There is no good reason, therefore, to prevent memorized secrets from being almost arbitrarily long, nor to prohibit the use spaces and of certain special characters. Since non-English speakers might more readily memorize a secret in their own language, Unicode characters should also be permitted (not just to permit the creation of emoji passwords as some have suggested).

It is nevertheless desirable to provide some degree of protection against subscribers who choose frequently used memorized secrets. SP 800-63B requires the use of a blacklist to prevent subscribers from choosing such secrets.

No size is specified for the blacklist. While it might be tempting to use lists of millions of compromised passwords (such lists are readily available on the internet), it is really only the ones that are fairly commonly used, a much shorter list, that represent a significant risk of online attack. Excessively long lists are also likely to be frustrating to the subscriber, as are the composition rules (inclusion of specific character classes in memorized secrets) currently in common use. Bear in mind that common passwords are not just words, but sometimes typing patterns such as "qwertyuiop".

In addition to common memorized secrets perhaps obtained elsewhere, it is useful to include other things that might be relevant to the specific service being authenticated, such as the agency name or domain name, or possibly even such things concatenated with common expletives.

When a subscriber attempts to choose a blacklisted memorized secret, it is helpful to give additional guidance to them. Measures like strength indicators (password meters) may encourage them not to choose a memorized secret that is a trivial modification of one on the blacklist.

##### Examples

As mentioned above, memorized secrets include passwords, passphrases, and PINs. The term passphrase is often used when the expectation is that the secret will be longer than a password, and when spaces may be included, but otherwise the terms are equivalent. PINs normally denote a numeric secret that is often randomly chosen by the CSP/verifier and assigned to the user. The length requirement for randomly chosen PINs is shorter than for user-chosen secrets because they would be expected to be uniformly distributed and therefore have more entropy than a user-chosen secret of the same length and composition. CSP-chosen secrets may be used for memorized secrets other than PINs as well, although the length requirements for such secrets are the same as for user-chosen memorized secrets.

#### Look-up Secrets

<div class="text-left" markdown="1">
  <table style="width:100%">
    <tr>
      <td>
        <img src="sp800-63b/media/Look-up-secrets.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;">
      </td>
      <td>
        Look-up secrets are secrets that are issued by the CSP to the subscriber each of which can be used for one successful authentication. They are considered <i>something you have</i>, the "something" being the printed or other media containing a set of these secrets. They are well-suited to use as a backup authenticator to be used when a primary authenticator is lost, stolen, or malfunctions.
      </td>
    </tr>
  </table>
</div>


The primary disadvantage of look-up secrets is that they can only be used for a specific number of authentications, after which a new set of look-up secrets needs to be issued to the subscriber. However, they are among the lowest-cost authenticators to issue. Issuance of look-up secrets can occur in person (typically at the end of an in-person identity proofing session), via postal mail, or in a mutually-authenticated protected session where the subscriber authentication also included something you have.

Look-up secrets must, of course, be protected from disclosure. While storage requirements for look-up secrets are not specified in SP 800-63B, look-up secrets that are used as backup authenticators would normally be stored in a locked container on the subject's premises. Issuance of look-up secrets should be accompanied by suitable advice on protecting the secrets, as well as procedures for revoking the secrets should they be lost or stolen. As noted in [SP 800-63B Section 5.1.2.1](https://pages.nist.gov/800-63-3/sp800-63b.html#lusa), look-up secrets may be issued online over a secure channel; this normally requires a mutually-authenticated session at AAL2 or higher. Non-secure mechanisms such as email are unsuitable for the distribution of look-up secrets.

In some cases, look-up secrets are issued in a form suitable for the subscriber to carry with them, e.g., in a wallet. While something carried in a wallet is probably more likely to be lost or stolen, that theft or loss is more likely to be detected quickly. Accordingly, issuers of look-up secret authenticators that are designed to be carried should have procedures in place to allow rapid reporting and revocation of authenticators that are no longer under the subscriber's control.

Look-up secrets need to be protected by the verifier as well. While [Section 5.1.2.1 of SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html#lusa) permits look-up secrets to have as little as 20 bits of entropy, their use as backup authenticators makes usability less of a concern and permits the use of look-up secrets with sufficient entropy to resist offline attacks. The use of high-entropy look-up secrets is highly encouraged.

##### Examples
The most common form of look-up secret authenticator is a printed list of secrets. These secrets are generated using an approved random bit generator, and may be expressed in any encoding that provides acceptable usability. This often includes grouping the secret into a number of sections to enhance its readability from the media on which it is delivered. One popular format is the version 4 (random) UUID, because of the wide support available for rendering UUID values.

One-time secrets can be used sequentially or a particular order specified by the verifier (e.g., "Enter OTP #4:"). This gives a bit of a challenge/response characteristic to the transaction. However, look-up secrets are required to be used only once, so "OTP #4" in this example would not be reused. This requirement is meant to ensure that an attacker with pervasive access to the authentication session (e.g., a key logger) would not be able to exploit the authenticator output in the future. The use of a specified order (verifier challenge) is acceptable but not required.

A third common example of a look-up secret authenticator is a secret grid. In this arrangement, the verifier gives the coordinates for squares in a grid under the control of the subscriber. Again, the grid squares can be used only once to meet SP 800-63B requirements. This also has the disadvantage that it is difficult to store the values in the individual squares securely: if the squares contain short values, hashed values stored by the verifier would be easily dictionary attacked. This form of look-up secret authenticator, while permissible, does not have any particular advantages and, being more susceptible to dictionary attacks, is discouraged.

#### Out-of-Band Devices

<div class="text-left" markdown="1">
  <table style="width:100%">
    <tr>
      <td>
        <img src="sp800-63b/media/Out-of-band-OOB.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;">
      </td>
      <td>
        Out-of-band authenticators use a private communication channel that is separate from the channel being authenticated to establish the claimant’s control of a specific physical device. An out-of-band authenticator is <i>something you have</i>.
      </td>
    </tr>
  </table>
</div>



While there are many different implementations of out-of-band authenticators, it is important to remember that the primary objective is to establish that the claimant controls a specific device associated with the subscriber—that the claimant and subscriber are the same person. To the extent that devices can be substituted without re-enrollment or more than one device can be used for a given out-of-band authentication, the authenticator is weaker, or in some cases unsuitable for use. Accordingly, (1) email services and (2) telephony that terminates in a voice-over-IP (VoIP) endpoint are not acceptable for out-of-band authentication because these often can be received by more than one endpoint. If the registration of an out-of-band device is rejected because it is a VoIP endpoint, it is helpful to explain the rationale for this to the subscriber.

It is also important to ensure that the activity on the out-of-band device be associated with a specific session on the primary channel. The transfer or verification of a secret between the primary and secondary channels avoids the opportunity for an attacker with good timing to obtain authentication of a different session controlled by them.

By far, the most common authentication flow for out-of-band authenticators is for the relying party to send a secret to the subscriber's device via a secondary channel and request that value be returned over the primary channel. However, at least two other out-of-band authentication flows are possible. As described in [SP 800-63B Section 5.1.3.1](https://pages.nist.gov/800-63-3/sp800-63b.html#ooba), the secret can also be output via the primary channel and returned over the secondary channel. This may permit the use of a QR code or similar mechanism to transfer the secret to the out-of-band device (often a mobile smartphone), potentially improving usability. The primary channel and out-of-band device may also display a secret and prompt the claimant to compare the consistency of those secrets to ensure that the claimant is authenticating the correct session. The verifier then accepts a yes/no response from the out-of-band device. This is a less effective method, because it depends on the subscriber actually making the comparison and not just selecting "yes".

In all of these situations, it is important that the out-of-band device be securely and uniquely authenticated. This requires the use of a secret in the device, perhaps in the form of a client certificate or, if using the telephone network, a SIM card.

It should be noted that the authenticator is not required to be a physically separate device from that on which the authentication is occurring. The requirement for separation applies to the communication channel, not the device. Therefore, it is permissible to authenticate a browser session on a mobile device using an application resident on the same device, provided they use separate communication channels (e.g., TLS sessions) and provided that the application uniquely identifies itself to the verifier.

##### Examples

The most common example of an out-of-band device is also a restricted authenticator: the use of SMS to send a random secret to the subscriber's mobile telephone. Many security weaknesses with this have been identified, including SS7 (telephone signaling) vulnerabilities and the possibility of the telephone number being reassigned to a different device, perhaps by social engineering of a carrier or retail representative by an attacker.

Some secure communications apps, such as Signal, create a fingerprint that changes if the device on which the app is running ever changes. This allows the verifier to securely detect a change in endpoint. The combination of strong device binding and the end-to-end encryption of the secondary channel permits the authentication secret to prove possession of a specific device, making this a fully acceptable alternative to the use of SMS.

A verifier-specific application can also be used to terminate the user side of the secondary communication channel. This application would need to maintain a secret (probably a key pair) that it uses to authenticate to the verifier in accepting or providing the secret being exchanged.

#### Single-Factor OTP Device

<div class="text-left" markdown="1">
  <table style="width:100%">
    <tr>
      <td>
        <img src="sp800-63b/media/Single-factor-otp-device.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;">
      </td>
      <td>
        A single-factor OTP device is something that is in the possession of the subscriber that generates one-time passwords that are displayed and manually entered by the claimant. Even though it is referred to as a "device", this authenticator can be either a distinct physical device or a software application running on a general-purpose device such as a smartphone. A single-factor OTP device is <i>something you have</i>.
      </td>
    </tr>
  </table>
</div>


Single-factor OTP devices that are not time-based usually operate based on the pressing of a button to obtain a single one-time password. While it is important that a one-time password be accepted only once, non-time-based devices might be operated by mistake, as a test, or in a session that authenticates unsuccessfully due to a communications error. Accordingly, the verifier should accept any of several possible future one-time passwords, and advance its state to the authenticator output most recently used when a successful authentication is performed.

Time-based OTP devices maintain an internal clock that must be kept in relative synchronization with the verifier. This can be difficult because the OTP device, under control of the subscriber, may be expected to operate for several years despite being subjected to temperature changes and other environmental factors that contribute to clock drift. The verifier needs to consider possible clock drift in its determination whether to accept a given OTP value. These devices are usually shipped from manufacturers with their clocks pre-synchronized, and the manufacturer may provide a verification service for their use. As in any case when authentication is outsourced, verifiers need to consider the security practices of the manufacturer when assessing overall misauthentication risk.

Unlike earlier editions of SP 800-63, SP 800-63B treats devices that are connected directly to the endpoint as crypto devices rather than as OTP devices, even if they only supply a one-time password. The authentication output for OTP devices is defined to be manually transferred from the OTP device to the application being authenticated. For this reason, OTP devices are never considered verifier-impersonation resistant as described in [SP 800-63B Section 5.2.5](https://pages.nist.gov/800-63-3/sp800-63b.html#verifimpers). The goal of verifier-impersonation resistance is to not depend on the claimant detecting a phishing attack, and an OTP authenticator cannot control where its output is entered.

##### Examples

A number of readily-available commercial OTP products, both hardware and software, are available on the market. The Initiative for Open Authentication (OATH) is an industry consortium promoting the use of OTP authenticators.

#### Multi-Factor OTP Devices

<div class="text-left" markdown="1">
  <table style="width:100%">
    <tr>
      <td>
        <img src="sp800-63b/media/Multi-factor-otp-device.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;">
      </td>
      <td>
        Multi-Factor OTP Devices are similar to Single-Factor OTP devices, but require activation by input of a memorized secret or the successful presentation of a biometric in order to obtain a one-time password. A multi-factor OTP device is <i>something you have</i> and is activated by <i>something you know</i> or <i>something you are</i>.
      </td>
    </tr>
  </table>
</div>


Many of the same considerations associated with single-factor OTP devices apply to these authenticators as well.

When the wrong memorized secret is entered, the authenticator can take one of two actions. One is to generate an intentionally incorrect output; this allows the verifier to implement a throttling strategy to discourage guessing attacks on the memorized secret. Another possibility is to display an error indication on the device. This avoids the usability impact if the user mis-enters the secret, but requires that the authenticator implement the throttling strategy describes in [SP 800-63B section 5.2.2](https://pages.nist.gov/800-63-3/sp800-63b.html#throttle), which may be challenging on some devices.

Because of the significant false reject rates associated with biometrics, the generation of an intentionally incorrect output is likely to have a greater impact on devices activated by a biometric. In using biometric-activated OTP devices, the severe throttling requirements described in [SP 800-63B Section 5.2.3](https://pages.nist.gov/800-63-3/sp800-63b.html#biometric_use) should be considered, and alternatives provided if the user is unable to successfully complete biometric authentication. These alternatives could include the use of a memorized secret for activation, or use of a completely different authenticator.

#### Single-Factor Cryptographic Software

<div class="text-left" markdown="1">
  <table style="width:100%">
    <tr>
      <td>
        <img src="sp800-63b/media/Single-factor-software-crypto.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;">
      </td>
      <td>
        A single-factor cryptographic software authenticator is a secret cryptographic key and associated software stored on a software-accessible medium. Authentication is accomplished by proving possession of the embedded key. A single-factor cryptographic software authenticator is <i>something you have</i>.
      </td>
    </tr>
  </table>
</div>


The characteristics of cryptographic authenticators depend on the method by which the authenticator output is generated. One such method is the generation of a one-time password; this is different from an OTP device because the authenticator output is directly supplied to the application by the authenticator. This makes a larger (higher entropy) authenticator output practical, but does not provide the additional security benefits of a challenge-response protocol.

##### Examples

The classic example of a single-factor cryptographic software authenticator is the use of a client X.509 (TLS) certificate. The certificate (signed public key) is accompanied by a private key that is held securely by the subscriber. The verifier needs to have some basis for associating the public key with the subscriber. This may be accomplished by a certificate that is signed by a certificate authority accepted by the verifier (in some cases, by the verifier itself) associating the certificate's common name with the subscriber. Alternatively, the verifier may directly associate the certificate's public key with the subscriber. Because the verifier only needs to associate specific certificates with subscribers, the use of generally-recognized root certificate authorities is often not required.

(other examples, perhaps using signatures and symmetric crypto?)

#### Single-Factor Cryptographic Devices

<div class="text-left" markdown="1">
  <table style="width:100%">
    <tr>
      <td>
        <img src="sp800-63b/media/Single-factor-crypto.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;">
      </td>
      <td>
        Single-factor cryptographic devices are similar to single-factor cryptographic software authenticators, except that the private key is contained within a hardware device and cannot be exported in normal operation. This means that the hardware device also performs the cryptographic operations associated with authentication. A single-factor cryptographic device is <i>something you have</i>.
      </td>
    </tr>
  </table>
</div>


As with cryptographic software authenticators, cryptographic device authenticators have capabilities that range from one-time password generation (not challenge-response, and not verifier-impersonation resistant) to others having many of the supplementary characteristics described in [Section 5.2](https://pages.nist.gov/800-63-3/sp800-63b.html#52-general-authenticator-requirements).

##### Examples

Single-factor cryptographic devices exist in a wide range of shapes and sizes. "Smart cards" with an embedded processor in a credit card form factor are quite popular, and may be read either via a dedicated device associated with the endpoint or through a USB adapter. Other devices, notably FIDO U2F authenticators, have direct USB interfaces and may be designed to be kept on a subscriber's (physical) keychain or for semi-permanent installation in an endpoint such as a laptop computer.

Single-factor cryptographic devices may also be embedded in a user endpoint, such as in a hardware TPM in a user device. Cryptographic devices with wireless interfaces, particularly NFC, are also emerging and may prove popular, particularly for mobile devices that may lack USB and similar hardware interfaces.

Some single-factor cryptographic devices operate in more than one mode, and it is important to consider the capabilities of the particular mode being used. For example, some authenticators that implement FIDO U2F (a challenge-response protocol that may be verifier impersonation resistant) also implement a legacy one-time password mode, which is not verifier impersonation resistant.

#### Multi-Factor Cryptographic Software

<div class="text-left" markdown="1">
  <table style="width:100%">
    <tr>
      <td>
        <img src="sp800-63b/media/Multi-factor-software-crypto.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;">
      </td>
      <td>
        Multi-factor cryptographic software authenticators are similar to single-factor cryptographic software authenticators except that they require the input of a memorized secret in order to access the private key for authentication. Multi-factor cryptographic software authenticators are <i>something you have</i> and are activated by <i>something you know</i>.
      </td>
    </tr>
  </table>
</div>


One of the operational problems associated with multi-factor cryptographic software authenticators is in determining whether a multi-factor authentication has in fact taken place. Since the encrypted private key is available to the subscriber's software, a non-cooperative subscriber could decrypt and store the key, degrading authentication to single-factor (but less effort for the subscriber) without the verifier's knowledge or consent. Since there is less opportunity to extract and decrypt the private keys on some platforms (particularly some mobile devices), these authenticators are more certain to be effective on these than on general-purpose devices.

Note that since [SP 800-63B Section 5.2.3](https://pages.nist.gov/800-63-3/sp800-63b.html#biometric_use) requires that biometrics be used as part of a physical authenticator, biometrics are not an acceptable method for unlocking the secret key of a multi-factor cryptographic software authenticator.

#### Multi-Factor Cryptographic Devices

<div class="text-left" markdown="1">
  <table style="width:100%">
    <tr>
      <td>
        <img src="sp800-63b/media/Multi-factor-crypto-device.png" alt="authenticator" style="width: 100px;height: 100px;min-width:100px;min-height:100px;">
      </td>
      <td>
        Multi-factor cryptographic device authenticators are similar to single-factor cryptographic device authenticators except that they require activation by the entry of a memorized secret or verification of a biometric. Multi-factor cryptographic device authenticators are <i>something you have</i> and are activated by either <i>something you know</i> or <i>something you are</i>.
      </td>
    </tr>
  </table>
</div>


Since the private key (authentication secret) associated with the device is embedded in a hardware device with security requirements (depending on the AAL at which it is used), activation of the authenticator can cause decryption of the secret key, as in the case of a multi-factor cryptographic software authenticator. It can also simply make the key available to an authentication operation. The latter is the mode in which biometric activation usually operates.

The activation factor can be provided to the authenticator directly (i.e., by keyboard input or biometric sensor directly on the device). More frequently, the activation factor is provided by the host endpoint; this requires additional trust in the endpoint, e.g., to make sure that a keylogger is not installed or that a biometric sensor is not being spoofed. If the biometric sensor or endpoint is separate from the authenticator, the sensor or endpoint needs to be authenticated as described in [SP 800-63 Section 5.2.3](https://pages.nist.gov/800-63-3/sp800-63b.html#biometric_use).

The activation factor, either a memorized secret or biometric, is subject to throttling on repeated unsuccessful attempts as described in [SP 800-63B Section 5.2.2](https://pages.nist.gov/800-63-3/sp800-63b.html#throttle). The state information for this throttling can be kept by the authenticator or unsuccessful authentication attempts can be indicated to the verifier, which would then limit the number of attempts permitted.

As with other cryptographic authenticators, a range of capabilities is possible, including generation of one-time passwords and challenge-response. The primary distinguishing factor between a cryptographic device and an OTP device is that the former is directly connected to the endpoint and the latter requires manual entry of the authenticator output by the claimant.

##### Examples

The classic examples of multi-factor cryptographic authenticators are US Government PIV and Department of Defense CAC authenticators. Other "smart card" authenticators, such as the Estonian e-resident card, are also in this category. Multi-factor cryptographic devices can also be embedded in endpoints, as is the case of FIDO UAF authenticators.

### General Authenticator Requirements

The subsections of [Section 5.2](https://pages.nist.gov/800-63-3/sp800-63b.html#52-general-authenticator-requirements) describe requirements applicable to multiple classes of authenticator, or in some cases supplemental requirements applicable at higher AALs. These are summarized in the table below.

|  | Rate Limiting | Biometrics | Attestation | VI Resistance | VC Resistance | Replay Resistance | Intent |
|-----|-----|-----|-----|----|-----|-----|-----|
| **Memorized Secret** | Required | N/A | N/A | No | No | No | Yes |
|**Look-up Secret** | Required | <64 bits | N/A | N/A | No | Maybe | Yes | Yes |
| **OOB** | Not required | N/A | N/A | No | Yes | Yes | Yes |
| **SF OTP** | Required | N/A | N/A | No | No | Yes | Yes |
| **MF OTP** | Required | N/A | Offline | No | No | Yes | Yes |
| **SF Crypto SW** | Not required | N/A | N/A | Maybe | Maybe | Yes | Maybe |
| **SF Crypto Dev** | Not required | N/A | Issuance or certificate | Maybe | Maybe | Yes | Maybe |
| **MF Crypto SW** | Required for activation | N/A | Offline, procedures | Maybe | Maybe | Yes | Yes* |
| **MF Crypto Dev** | Required for activation | Required for biometric activation | Issuance or certificate | Maybe | Maybe | Yes | Yes* |

\* If the activation factor is not cached

#### Physical Authenticators

This section addresses the need for physical authenticators (any authenticator that includes something you have) to be protected against theft and loss. The CSP needs to establish procedures to handle these situations, and needs to ensure that the subscriber knows what to do (how to report the event) when they occur.

In order to avoid denial-of-service attacks on subscribers, the CSP needs to identify the subscriber when accepting such a report. Typically, the cost associated with erroneously suspending a subscriber is lower than that associated with use of a stolen authenticator, so this identification can often be weaker than would be acceptable for authentication. However, in certain cases erroneous suspension could be very serious, so procedures for revocation need to be designed accordingly.

#### Rate Limiting (Throttling)

Rate limiting, also referred to as throttling, is the primary defense against online attacks on the authenticator, authenticator output, or an activation factor used by a multi-factor authenticator. The throttling parameters have been chosen based on the value being guessed by the attacker having approximately 20 bits of entropy, or a likelihood of success of 1 in 1 million guesses. The 100 guesses permitted therefore gives an attacker approximately a 1 in 10 thousand chance of success.

Rate limiting, of course, is another opportunity for an attacker to be able to perform a denial-of-service attack on the subscriber. Several suggestions are made to mitigate that possibility. The use of a CAPTCHA tends to protect against automated attacks, and the use of delays increases the likelihood that the attack will be discovered before being complete. The scope of the rate limiting (such as by IP address) can also be limited, although it is important to consider the capabilities of potential attackers to launch a distributed attack from many IP addresses.

When multiple authentication factors are being used, it is sometimes possible to rate-limit only when one of the factors is successful. For example, an authentication using a memorized secret plus an OTP authenticator output might only throttle (or perhaps even prompt for) the OTP when the memorized secret is correct. It might also prompt for both and not indicate which factor, if any, had succeeded and thereby only throttle the unsuccessful factor, whichever it was, if the other factor was correct.

#### Use of Biometrics

Biometric authentication is a rapidly evolving area, and it is important to use biometrics consistent with actual measured performance characteristics. It is also important to work within the revocability and secrecy limitations of biometrics.

One of the primary limitations of biometrics is that they cannot be revoked: it isn't possible to change your fingerprint, iris pattern, or other modalities if your biometric becomes known to a potential attacker. This is addressed by the requirement that there be a strong binding between the biometric and a physical authenticator. A biometric is enrolled for use with a specific physical authenticator, and if there is a suspicion of misuse, it is the physical authenticator, not the biometric itself, that is revoked or suspended.

Biometrics are also not secret. High-resolution cameras have been shown to reveal a person's iris pattern in enough detail for authentication, and fingerprints are left behind on many things you touch. There is, of course, the challenge of producing a model that replicates the subscriber, a challenge that is made more difficult with the use of presentation attack detection (PAD) technology. But liveness detection and the need to replicate some aspect of the subscriber is only difficult if the attacker does not control the biometric sensor. "Skimmers" for credit cards and PINs are commonplace, and use of skimmers and devices that can spoof biometrics should be expected as well. If the sensor and processing cannot be trusted, a collected biometric could be substituted for that from an actual sensor. For this reason, the sensor (or endpoint with a tightly integrated sensor) needs to be authenticated to ensure that it is not an impostor.

Current performance of biometric sensors and processing leads to the requirement of a false-match rate of 1 in 1000 or better. Furthermore, this rate is measured under conditions of a zero-effort attack: biometrics from random people being tested, without intentionally picking biometrics that are more likely to be accepted. Because this rate is significantly lower than authenticators like memorized secrets and OTPs, more restrictive throttling requirements have been adopted. Depending on whether PAD is implemented, throttling begins at 5-10 failed attempts, and increases exponentially after that. For this reason, an alternate modality, or the use of a memorized secret as the second factor, is probably required in most situations.

Biometrics can be verified centrally, although increases in processor performance (e.g., in mobile devices) makes it increasingly practical to verify biometrics at the sensor. If central verification is performed, additional requirements about the security of the biometric data in transit and authentication of the sensor/endpoint are imposed. In particular, use of a biometric is required to be tightly bound to specific device(s) for which the sensor and endpoint have been determined by the verifier to meet the required performance parameters.

#### Attestation

While verifiers must of course authenticate the claimant, they must also have some information about the manner in which that has occurred. In some cases, this may be obvious, e.g., the use of a memorized secret plus an OTP, with both authenticator outputs being presented to the verifier. In others, the similarities between some multi-factor authenticators and their single-factor counterparts gives rise to a need to securely determine what type of authenticator is used. This need is particularly evident for "bring your own authenticator" systems, where the subscriber uses an authenticator obtained elsewhere rather than one that has been provided by, and is known to, the CSP.

Another situation in which attestation is useful is in determining whether the security requirements of the authenticator have been met. For example, at AAL3, multifactor authenticators are required to meet FIPS 140 Level 3 physical security and Level 2 overall. Attestation information describing the authenticator being used can allow the CSP or verifier to determine whether that requirement has been met.

Attestation usually is required only at the time the authenticator is bound to the subscriber's account and not in connection with each authentication, since it is expected that it will be difficult to move secrets from an acceptable authenticator to one that is less secure.

#### Verifier Impersonation Resistance

Verifier Impersonation Resistance is a characteristic of some cryptographic authenticators that binds the authenticator output to a specific authenticated protected session (usually a TLS session). Verifier impersonation resistance is effective against certain types of "phishing" attacks where the claimant is misdirected to a look-alike site where they attempt to authenticate.

When authentication is attempted at a phishing site operated by the attacker, the attacker can capture the authenticator output and initiate their own authentication session with the actual relying party. If a one-time password (such as from an OTP device), the attacker can use the authenticator output immediately after it is entered, so even a time-based OTP does not protect against the attack. Challenge-response protocols are similarly ineffective because the attacker can open an authentication session and obtain the challenge nonce, relay it to the claimant, and then have the necessary response to authenticate the attacker's own session.

Establishment of authenticated protected sessions creates encryption keys unique to the session using Diffie-Hellman key exchange. This key can be included in calculating the authenticator output, so that the output is not valid for any other authenticated protected session (such as that between the attacker and the actual relying party in the example above).

Note that verifier impersonation resistance requires both a directly-connected authenticator (a cryptographic device or cryptographic software authenticator) as well as support in the application, such as a web browser, in which it will be used. Some cryptographic devices do not actually bind to the protected session secrets and are therefore not verifier impersonation resistant.

#### Verifier-CSP Communications

SP 800-63B assumes a very close relationship between the verifier and the CSP: that they are two different roles for the same entity or that they are very closely associated, perhaps under common administration. In the latter case, this section reinforces the requirement that all communications between the entities be strongly protected by a mutually-authenticated secure channel.

#### Verifier Compromise Resistance

A common form of authentication compromise is an attack on the verifier, which if successful may be able to harvest information that can later be used to authenticate to that verifier. Authentication protocols where the verifier has data that can only be used to verify, and not generate, the authenticator output are referred to as bring verifier compromise resistant.

Public keys used with approved algorithms and having at least the minimum security strength specified in SP 800-131A are considered to be verifier compromise resistant, as are hashed keys when the key being hashed has the necessary security strength. So, for example, look-up secrets that are sufficiently complex would be considered verifier compromise resistant when hashed with an approved algorithm.

Certain types of authenticators, notably OTP devices and cryptographic devices that generate one-time passwords cannot be verifier compromise resistant because they need to share a secret with the authenticator in order to generate an authenticator output for comparison.

#### Replay Resistance

An authenticator output is considered replay resistant if its output can be used only once for authentication. Most authenticators specified are replay-resistant, with the notable exception of memorized secrets when they are used independently (other than as an activation factor for a multifactor authenticator).

#### Authentication Intent

One of the concerns with embedded and directly-connected authenticators (typically cryptographic device authenticators) is the question of whether malware in the endpoint device that hosts the authenticator can cause authentication to occur without the subscriber's knowledge or consent. In this situation, the malware could proxy authenticator challenges from the attacker if needed, and obtain the authenticator output needed to sign the attacker into a service of interest. In common use, some cryptographic authenticators are left connected for multiple authentications, and are subject to this concern.

All authenticators that require claimant intervention establish authentication intent, provided that there is no caching of claimant input and that the intervention cannot be spoofed by software (e.g., by simulating keyboard input). In most cases, multifactor authenticators also establish intent unless claimant input is cached, although certain biometric modalities such as facial recognition may require additional measures to establish intent. Caching of claimant input should be avoided because it weakens the establishment of intent.

Authentication intent does not require that the claimant be authenticated in any way, only that someone has taken an action requesting authentication at the endpoint. This could be through the pressing of a button or the insertion or connection of an authenticator that is capable of only one authentication per insertion, for example.

Wireless authenticators (e.g., NFC, Bluetooth, ISO 14443) require special consideration with respect to authentication intent. Since a connection with the authenticator could be established by an attacker who happens to be close to a subscriber carrying one of these authenticators, intent cannot be established by connection to the authenticator alone. These authenticators should require the pressing of a button or similar action to operate, even if a challenge/response protocol is being used (a mobile attacker could proxy an authentication challenge nonce and collect the result).

#### Restricted Authenticators

As both authentication technologies and attacker capabilities mature, some authenticator classes and sub-classes will inevitably become less effective. In severe cases, these authenticators will be removed from acceptable use. In SP 800-63B, this has been done with pre-registered knowledge tokens (knowledge-based authentication) and with the use of email as an out-of-band authentication technique.

When continued use represents a lower immediate risk, authenticators may be classed as "restricted authenticators". Use of restricted authenticators requires additional scrutiny as described in SP 800-63B, particularly that a risk assessment be performed by the implementing organization.

Restricted authenticators should not be used for new implementations; authenticators that are restricted may be removed from future editions of SP 800-63B as attacker capabilities mature further.

At present, the use of PSTN (SMS and voice) to deliver out-of-band secrets is restricted. This was prompted by several factors, including:

* The demonstrated ability of attackers to obtain reassignment of telephone numbers used for authentication to new devices they control
* Weaknesses in SS7 security that provide attackers with the opportunity to intercept out-of-band secrets sent via text messages
* Ability in many cases for subscribers or attackers to forward these notifications to a new device, breaking the ability to determine possession of a specific device
