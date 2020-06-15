---
layout: default
title:  Example Federation Scenarios
permalink: /63C/Scenarios
navOrder: 5  
navTitle: Scenarios  
---

# Example Scenarios

This section describes some common scenarios in use across different protocols and deployment patterns. 

## Shibboleth and SAML

SAML Federations like InCommon can operate at FAL1 or FAL2. Most InCommon IdPs are running on a Shibboleth identity provider. They pass assertions through a response to an authentication event. Most often, those assertions are not encrypted to the RP and therefore conform to FAL1. For a Shibboleth IdP, either encrypt all assertions to the RP or refrain from sending personally identifiable information such as `eduPersonPrincipalName` (or `eppn`) over the wire as an unencrypted SAML assertion.

SAML can reach FAL3 by providing an attribute within the SAML assertion that references a cryptographic key to be presented by the subscriber at the RP. The subscriber would then need to present proof of possession of that key directly to the RP in order to reach FAL3.

## OpenID Connect

Typically, OpenID Connect Providers interact with OpenID Connect relying parties by providing a signed authentication assertion (the ID Token) which is separate from the transfer of personally identifiable information (from the UserInfo Endpoint). As such, these providers can safely operate at FAL1 because they are not bundling identity assertions with authentication information. This characterization is true for both the authorization code and implicit client types. 

If the ID Token contains PII and is passed on the front channel (through the implicit or hybrid flows), it needs to be encrypted to the RP at FAL2 to protect the PII. This is accomplished by using the JSON Web Encryption (JWE) specification and a key registered to the RP.

OpenID Connect can reach FAL3 by providing a claim within the ID Token that references a cryptographic key to be presented by the subscriber at the RP. The subscriber would then need to present proof of possession of that key directly to the RP in order to reach FAL3.

## Personal Identity Verification (PIV) Card 

PIV cards are considered an authentication technology by the SP 800-63 guidelines, not a federation technology. Therefore, using a PIV card during a login determines the AAL, as well as the IAL that was used to issue the PIV card. As FALs are independent of AALs, any authentication technology can be used to start a federation transaction at any FAL. Therefore, the use of a PIV card does not imply any particular FAL.

Since they are authenticators, PIV cards can be used to authenticate to an IdP and start a federation transaction. This approach allows the complex processing and validation of the PIV certificate chain to be handled by a specialized security component, the IdP, and identity information be sent to the downstream RPs by the federation protocol. 

Recall that in a federation protocol, the subscriber's attributes are contained in the assertion or in an associated identity API. Therefore, the attributes contained in the PIV certificates can then be transmitted by the IdP to the RP through those mechanisms, assuming all consent and privacy considerations around attribute release have been followed as usual. However, not all attributes in the certificate need be sent, allowing an IdP to tailor the information that it discloses to a given RP. Additional attributes can also be sent in the federation transaction that are not included in the certificate itself. Additionally, the attributes sent through federation are significantly easier to update than those within the PIV card's certificates, which necessitate issuance of a new certificate in its entirety.

Federated identity protocols allow subscribers to authenticate at an RP regardless of which authenticator they use at their IdP. This allows an RP to support all derived PIV credentials that an IdP has associated with the subscriber without having to verify the derived PIV credentials directly.

A PIV card can also be used to reach FAL3 by acting as the secondary authenticator alongside the assertion. If the assertion contains a reference to the PIV authentication certificate, and the RP directly verifies that the subscriber can present that certificate, then FAL3 can be reached.

## Privacy-enhancing Federated Identity

In many cases, RPs do not need to know the full set of attributes available for a subscriber. RPs need to request only as much information as they need to complete the transaction requested by the subscriber, and IdPs need to limit what information RPs have access to within a transaction as per [Section 5.2](https://pages.nist.gov/800-63-3/sp800-63c.html#privacy-reqs). Furthermore, with protocols like OpenID Connect, the attributes of the subscriber can be sent separately from the assertion itself, limiting leakage of this information. 

Pairwise identifiers ought to be used in place of persistent or correlatable identifiers whenever possible (See [Section 6.3](https://pages.nist.gov/800-63-3/sp800-63c.html#ppi)). This limits relying parties in attempts of tracking or identifying individual subscribers across different systems. 

When possible, claim references ought to be used to communicate identity information rather than raw data (See [Section 7.3](https://pages.nist.gov/800-63-3/sp800-63c.html#protecting-information)). For example, if a relying party needs to know whether a subscriber is over eighteen years old, the IdP can respond that the subscriber is over eighteen without sharing the subscriber's age or birthdate.

## Parallel Authentication

In some cases a relying party may wish to confirm certain aspects of a subscriber's identity above and beyond what the IdP provides. For example, a relying party could log in a subscriber using an IdP, receive a picture of the subscriber from the IdP, and require that an in-person agent verify that the picture matches the identity of the person authenticating. This use case is known as "parallel authentication" because two authentication events are happening next to each other: the assertion, and the verification of the biometric (photo) by a trusted agent. The focus of FAL is primary on the assertions being passed from the IdP to the RP, so most authentication events occurring at the RP would not affect the FAL of the transaction. 

At FAL3, holder-of-key transactions occur by verifying both the assertion from the IdP as well as the subscriber's presentation of proof of their personal key attested to in the assertion, which is another form of parallel authentication.

## Brokered Identity Management

Some federated identity architectures are based on brokered identity management described in [Section 5.1.4](https://pages.nist.gov/800-63-3/sp800-63c.html#proxied), where a single broker intermediates transactions between registered IdPs and RPs. In this architecture, each entity in the system only has to register with one broker in order to interoperate with everyone else in the system. 

Recent advances in automated registration processes have made IdP/RP integrations much less onerous than they used to be. Since it is now more possible for an IdP and RP to register with each other in a very short amount of time, or without any manual intervention, the value of a broker solely as an integration point is much less.

The use of a broker can also blind the participants of the transaction from each other. Specifically, an IdP can authenticate a subscriber without knowledge of which RP requested the authentication event, and that an RP need not know which IdP a subscriber used to authenticate to the broker. While brokered identity management systems may appear to protect privacy by blinding an IdP from an RP, keep in mind that the broker itself is aware of all the parties involved in the transaction, and in some cases can see personally identifiable information about subscribers. Brokered identity management systems do not prevent subscriber tracking all together, they merely shift the ability to track subscribers away from the IdPs and RPs and on to the broker.

Additionally, because brokers have access to active and valid identity assertions, they are capable of impersonating subscribers at RPs. The broker can also effectively impersonate any RP to an IdP, and any IdP to an RP. This power increases the risk inherent in the entire architecture, since the broker represents a single point of failure which, if it is compromised, can in turn compromise every participant in the system.

NIST has been promoting privacy-enhancing technology in the brokered identity management space through the [Privacy-Enhanced Identity Federation project](https://nccoe.nist.gov/projects/building-blocks/privacy-enhanced-identity-brokers). This NIST building block outlines a set of goals which would constitute a new kind of brokered architecture. This architecture leverages a broker which cannot impersonate or track subscribers. This architecture is still theoretical and may allow for a privacy-preserving and secure version of brokered identity management in the future.

## Communicating xAL

The value of the FAL for a given federation transaction should be inherently detectable by the nature of the transaction itself. Namely, the RP can tell if the assertion is encrypted and it will know if it has prompted for a secondary key-based authenticator. However, only the IdP inherently knows the IAL and AAL for the subscriber. The IdP can communicate that information to the RP in the assertion by using a format such as [Vectors of Trust](https://tools.ietf.org/html/rfc8485) or the [SAML Authentication Context](https://docs.oasis-open.org/security/saml/v2.0/saml-authn-context-2.0-os.pdf), in combination with an appropriate trust framework. Since the RP has no way of directly verifying the IAL or AAL being asserted, it must trust that the IdP is asserting accurate and valid information regarding the subscriber. 

It is still up to the RP to decide whether any given subscriber can perform an action within the RP's system. An RP could decide that most operations are allowable for people logging in at AAL2, for instance, but certain sensitive applications would require AAL3. Or an RP could request an FAL3 assertion, along with its key reference, but only prompt the subscriber for their key if a privileged operation required such escalation. Until such time that the secondary key is proofed by the RP, the subscriber is operating at FAL2.