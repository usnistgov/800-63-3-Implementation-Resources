---
layout: default
title:  Guide for Relying Parties
permalink: /63C/RP
navOrder: 3 
navTitle: RPs  
---

# C.3 Guidance for Relying Parties {#s-c-3}

While it is the responsibility of the IdP to provide strong and trustworthy federation assertions, relying parties need to validate the elements of an assertion during a federated transaction as in [Section 6.2](https://pages.nist.gov/800-63-3/sp800-63c.html#61-assertion-protection). 

Relying parties can be a valuable target for attackers to impersonate valid subscribers or gain valuable information about them. If relying parties do not check the validity of the information they receive, attackers can gain access to the various services that subscribers are logging in to. 

If all of these checks are performed properly, the compromise of a single relying party does not threaten the rest of the network. This is in contrast to systems with some kinds of individual authenticators at each site, where the theft of a subscriber's password from one site often leads to the compromise of other sites in the network due to password reuse. 

## C.3.1 General Guidance {#s-c-3-1}

Relying parties need to do two major checks against incoming assertions:

 - check that the assertion itself is internally consistent, and
 - check that the assertion is verifiably from a trusted source.

Relying parties need to validate IdP signatures, assertion expirations, and audience parameters within an assertion to validate that the assertion itself is internally consistent. Additionally, RPs need to test that these validation checks are working at all times because there will be no outward indication that something is wrong with the system until an attack occurs. In other words, RPs need to ensure that they are rejecting invalid assertions just as much as they are accepting valid assertions.

RPs need to also verify the origin of the information that they receive, as an attacker might try to inject a valid assertion from another subscriber in order to take over an account. RPs can do this by making sure that the assertion is signed by a trusted IdP's key and that the assertion is not being replayed. RPs also need to check the source of the assertion. This most often means that they will accept an assertion only if it is presented in response to a direct request for one, and not at any other time. This also means that an RP will only accept assertions generated and signed by the IdP they were connecting to.

### C.3.1.1 Validating IdP Signatures {#s-c-3-1-1}

At all FALs, an identity assertion is signed by an IdP so that it cannot be forged by an attacker as per [Section 6.2.2](https://pages.nist.gov/800-63-3/sp800-63c.html#signed-assertion). The IdP is the only entity with access to its private key (detailed in [Section 4.1](https://pages.nist.gov/800-63-3/sp800-63c.html#key-mgmt)), so a valid signature indicates that the assertion is from the IdP itself and not an attacker, and that it has not been modified by an attacker. If an RP does not check the validity of the IdP signature, attackers will be able to forge identity assertions and gain access to protected systems without authorization. Additionally, if the relying party does not check the signature, an attacker could modify an otherwise valid assertion in transit, associating attributes and access rights to the current subscriber that were not asserted by the IdP. 

Some protocols cover the entire assertion with a signature, while others cover only portions of it. The relying party has to take care to not accept unsigned portions of the assertion as validated even when presented alongside a signed assertion.

Validating the signature is not enough. The RP also needs to make sure it is using the correct key for the claimed IdP, especially if the RP accepts assertions from multiple IdPs. In OpenID Connect, for example, the IdP is identified by the "iss" field of the ID Token's payload, and the signing key is identified by the "kid" field in the ID Token's header. The RP will accept the token if and only if the signature validates using the identified key from the identified issuer, and then only if the issuer is trusted to provide identities to this RP. Additionally, the RP will accept the assertion only if it is issued by the IdP that the RP is currently communicating with. Otherwise, a rogue IdP could replay an assertion issued by another IdP in an attempt to grant an attacker access to the RP.

Testing whether RPs will reject unsigned assertions or assertions with invalid signatures is critical, though not an obvious test to do. Properly authorized transactions will still work even if an RP is not checking assertion signatures, since the RP will accept the (valid) assertion whether or not it has a valid signature. Therefore, in such cases there is no outward indication of a problem in the system and there will be no error messages or login failures to indicate that something is wrong. Only a failure from a negative test -- that is to say, the explicit rejection of an unsigned assertion or an assertion with an invalid signature -- will indicate that a relying party is properly checking keys and signatures.

#### C.3.1.1.1 Retrieving IdP Keys {#s-c-3-1-1-1}

The RP can trust the assertion's signature only as much as it can trust that the keys used to verify the signature are associated with the IdP as per [Section 6.2.2](https://pages.nist.gov/800-63-3/sp800-63c.html#signed-assertion). The keys need to be retrieved in a secure fashion, such as over an authenticated protected channel or having been pre-placed by a systems administrator. Only the keys identified in the assertion can be used to evaluate the signature of an assertion. 

### C.3.1.2 Checking Assertion Expirations {#s-c-3-1-2}

Federated identity assertions are intended to be short-lived, since they are used to establish a session at the RP and not to manage a full session at the RP (see [Section 5.2](https://pages.nist.gov/800-63-3/sp800-63c.html#privacy-reqs)). While details vary per protocol family, an assertion lasting a small number of minutes will in most cases give the system ample time to process the assertion and create a session for the subscriber. Since federation assertions are passed between different systems on the network, it is reasonable to allow a small amount of padding to the time checks to account for clock skew. This skew ought to be very short, such as a few seconds, so as to not inadvertently open the attacker's window for using expired assertions. A time synchronization protocol such as NTP can be used on all systems on the network if possible to ensure the system clocks are as accurate as possible. 

An identity assertion which expires quickly makes it difficult for attackers to misuse the assertion and also ensures that any identity or authorization information included in the assertion is not out-of-date. RPs need to be tested to ensure they do not accept expired assertions, which can be done by presenting the RP with an expired but otherwise valid assertion and seeing if the RP accepts or rejects it.

Some assertions also contain a timestamp indicating when the assertion was issued, and an RP should not accept any assertion that claims to have been issued in the future. Some assertions will also have a timestamp indicating when the assertion is not to be used before, which an RP can process to ensure it is not accepting an assertion too early. The use of the "not-before" processing mechanism is relatively rare in modern federation protocols, as the assertions are created in response to specific login requests. 

All of the date fields have to be covered by the assertion's signature.

### C.3.1.3 Checking Audience Restrictions {#s-c-3-1-3}

Common attacks include taking an assertion intended for one RP and presenting it at another RP, with or without modification. When an IdP creates an assertion, it includes an audience field indicating which RP requested the assertion as in [Section 6.2.4](https://pages.nist.gov/800-63-3/sp800-63c.html#624-audience-restriction). By checking the audience field of the assertion, an RP can detect when an attacker is presenting an assertion intended for a different RP.

If an RP does not check for a matching audience parameter, it is possible for an attacker to get a valid assertion from any RP registered with the IdP and replay it at the target RP to gain unauthorized access.

An RP that is not checking audience parameters will still accept a valid authorization with no outward indication of a problem. Therefore, it is important to test the RP with an assertion containing an errant or missing audience field.

The audience field has to be covered by the assertion's signature.

### C.3.1.4 Checking Assertion Uniqueness {#s-c-3-1-4}

An attacker that gains possession of a bearer assertion could try to replay that assertion at an RP in order to take over a subscriber's session. To prevent this, an IdP is required to make each assertion unique as per [Section 6.2.1](https://pages.nist.gov/800-63-3/sp800-63c.html#assertion-id). The RP consequently needs to check the assertion for uniqueness within the assertion's expiry window by checking any unique identifiers within the assertion and accepting each unique assertion identifier once and only once to establish a session with a single subscriber. If an assertion is seen multiple times by an RP, especially from multiple connections, the RP can consider this assertion stolen. 

The RP ought to remember the identifiers of assertions as long as those identifiers are valid. Since assertions have a relatively short lifespan, this can be accomplished without large storage requirements by remembering only otherwise-valid assertion IDs within their validity window. If an assertion is replayed after it has expired, it will be rejected based on its expiration.

## C.3.2 Guidance by Product Family {#s-c-3-2}

This document covers two main product families that enable federated identity transactions - SAML and OpenID Connect, the latter of which is built on top of OAuth. Other protocols and approaches are possible to use while fulfilling the requirements of the guidelines.

### C.3.2.1 SAML {#s-c-3-2-1}

All parties need to be careful about passing and validating metadata. Incorrectly communicated or configured metadata could leak information about a subscriber that was not approved for distribution. Metadata that is not validated could have been tampered with by an attacker to gain access to valuable personal information.

The RP has to always check certificates before accepting identity assertions. Attackers can forge certificates and phish subscribers in an attempt to impersonate them.

SAML is not well-suited for use when the RP is a mobile or desktop application. Additionally, SAML does not provide a good means for protecting APIs. These limitations should be considered when choosing a product family.

### C.3.2.2 OpenID Connect {#s-c-3-2-2}

Different OAuth grant types or "flows" are appropriate for different kinds of applications at different FALs.

The authorization code flow is a back-channel presentation mechanism and ought to be used whenever possible, particularly for web server, native, or mobile applications. It is the most common and most secure way to implement OAuth, the underlying protocol of OpenID Connect. It can accommodate all three FALs depending on the exact configuration of the application. The authorization code flow makes use of back channel assertion presentation, which reduces the attack surface of the RP significantly by sending the assertion directly from the IdP to the RP without an intermediary party touching it. The RP ought to authenticate itself when presenting the authorization code to the IdP.

If the RP is a native or mobile application, it can use the [PKCE extension](https://tools.ietf.org/html/rfc7636) or [dynamic client registration](https://tools.ietf.org/html/rfc7591) to ensure that different copies of the client software can not impersonate each other at the IdP. The [best current practices for OAuth 2 mobile applications](https://tools.ietf.org/html/rfc8252) specification provides additional guidance.

In-browser applications, sometimes known as Single Page Applications (SPAs), are particularly challenging. The implicit grant type is a front-channel presentation mechanism and is applicable for applications which are implemented entirely in front-end code and have the capability to store secrets outside of the subscriber's web browser. However, best current practice is to use PKCE and the authorization code grant type for an SPA, or to use the OIDC hybrid flows to protect information. Best practices for these applications are currently under development by the OAuth working group in [draft-ietf-oauth-browser-based-apps](https://tools.ietf.org/html/draft-ietf-oauth-browser-based-apps). 

The lack of ability to store secrets means that these sorts of applications can usually only function at FAL1 because they have no method of private key management which would enable encryption of identity assertions. Modern browsers could allow a dynamic registration of the SPA and an in-browser protected keypair, but this is not a common deployment pattern at this time.

The client credentials and resource owner credentials grant types are not allowed at any FAL.
