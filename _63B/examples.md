---
layout: default
title:  Authenticator Examples
permalink: /63B/AuthenticatorExamples
navOrder: 7 
navTitle: Examples
---

# B.7 Authenticator Examples {#s-b-7}

The following are examples of authenticators thought to represent each of the authenticator types described in [SP 800-63B](https://doi.org/10.6028/NIST.SP.800-63b). This list describes only authenticators; it does not include authentication providers (either products or as-a-service) that support authenticators made by third parties.

## B.7.1 Criteria for Inclusion {#s-b-7-1}

If your resource or product is: publicly available (either free or offered for sale) and described on the internet, it meets the basic criteria for inclusion in the this document. If your resource or product qualifies and you would like it listed here, send a description of it to <dig-comments@nist.gov>.

## B.7.2 Representations and Warranties {#s-b-7-2}

Certain commercial entities, equipment, or materials may be identified in this document or linked websites in order to support deployment of authentication systems supporting NIST SP 800-63-3. Such identification is not intended to imply recommendation or endorsement by NIST, nor is it intended to imply that the entities, materials, or equipment are necessarily the best available for the purpose.

| Authenticator Type | Example |
|--------------------|---------|
| Memorized Secret | Password |
| | PIN |
| Look-Up Secret | [Apple Recovery Key](https://support.apple.com/en-us/HT208072) |
| | [Google Backup Codes](https://support.google.com/accounts/answer/1187538?hl=en) |
| Out-of-Band | [Auth0 Guardian](https://auth0.com/docs/multifactor-authentication/guardian/user-guide) |
| | [Duo Push](https://duo.com/product/trusted-users/two-factor-authentication/authentication-methods/duo-push)
| Single-Factor OTP | [Google Authenticator](https://support.google.com/accounts/answer/1066447) |
| | [Bluink App](htttps://bluink.ca/key) |
| | [SecurID](https://www.rsa.com/en-us/products/rsa-securid-suite/rsa-securid-access/securid-hardware-tokens.html) |
| | [DIGIPASS GO](https://www.vasco.com/products/two-factor-authenticators/hardware/one-button/index.html) |
| | [SecureOTP](https://www.securemetric.com/two-factor-authentication-solution/) |
| Multi-Factor OTP | [SafeNet GOLD OTP Authenticator](https://safenet.gemalto.com/multi-factor-authentication/authenticators/one-time-password-otp/gold-challenge-response-token/) |
| Single-Factor Cryptographic Software | Client TLS certificate |
| | [SSH key](https://www.ssh.com/key/) |
| Multi-Factor Cryptographic Software | Password-protected Client TLS certificate |
| Single-Factor Cryptographic Device | [FIDO U2F authenticator](https://fidoalliance.org/approach-vision/) |
| | [Bluink Key](htttps://bluink.ca/key) |
| | [USBAuth](http://usbauth.com) |
| | [Keydo Fido U2F](https://www.neowave.fr/US/keydo_fido_u2f.html) |
| | [Yubikey](https://www.yubico.com/)[^u2f] |
| Multi-Factor Cryptographic Device | [FIDO UAF authenticator](https://fidoalliance.org/approach-vision/) |
| | [Badgeo ID 2.0](https://neowave.fr/US/badgeo_ID_2.html)|
| | [PIV](https://doi.org/10.6028/NIST.FIPS.201-2) and CAC cards |
| | [Tyfone Side-X](https://tyfone.com/products/side-x-digital-endpoint-security/) |
| | [Smart Card](http://www.smartcardalliance.org/smart-cards-intro-standards/) |
{:latex-columns="p@0.44\textwidth,p@0.52\textwidth" latex-table="B-7-1" latex-caption="Authenticator Examples"}

[^u2f]: Only verifier-impersonation resistant when used in FIDO U2F mode.