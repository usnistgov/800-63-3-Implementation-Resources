---
layout: default
title:  Example Federation Scenarios
permalink: /63C/Scenarios
navOrder: 5  
navTitle: Scenarios  
---

### Example Scenarios

#### Shibboleth and SAML

SAML Federations like InCommon can operate at FAL1 or FAL2. Most InCommon IdPs are running on a Shibboleth identity provider. They pass assertions through a response to an authentication event. Most often, those assertions are not encrypted to the RP and therefore conform to FAL1. For a Shibboleth IdP, either encrypt all assertions to the RP or refrain from sending personally identifiable information such as `eduPersonPrincipalName` (or `eppn`) over the wire as an unencrypted SAML assertion.

SAML could reach FAL3 by providing an attribute within the SAML assertion that references a cryptographic key to be presented by the subscriber at the RP.

#### OpenID Connect

Typically, OpenID Connect Providers interact with OpenID Connect relying parties by providing a signed authentication assertion (the ID Token) which is separate from the transfer of personally identifiable information (from the UserInfo Endpoint). As such, these providers can safely operate at FAL1 because they are not bundling identity assertions with authentication information. This characterization is true for both the authorization code and implicit client types. 

If the ID Token contains personally identifiable information, it needs to be encrypted to the RP at FAL2. This is accomplished by using the JSON Web Encryption (JWE) specification and a key registered to the client. 

OpenID Connect could reach FAL3 by providing a claim within the ID Token that references a cryptographic key to be presented by the subscriber at the RP.

#### Personal Identity Verification (PIV) Card 

PIV cards are considered an authentication technology by the SP 800-63 guidelines, not a federation technology. However, PIV cards can be used to authenticate to an IdP and start a federation transaction. This approach allows the complex processing and validation of the PIV certificate chain to be handled by a specialized security component, the IdP, and identity information be sent to the downstream RPs by the federation protocol. The attributes contained in the PIV certificates can be transmitted by the IdP to the RP, assuming all consent and privacy considerations around attribute release have been followed as usual.

FALs are independent of AALs, and any authentication device may be used to start a federation transaction at any FAL. Therefore, the use of a PIV does not guarantee a high FAL, but it can help.

There are many benefits to using federated identity management as opposed to requiring independent registration of PIV cards for each subscriber. Federated identity management protocols such as OpenID Connect allow subscribers to authenticate at a relying party regardless of which authenticator they use at their IdP. This allows relying parties to securely accept registered subscribers whose IdPs do not use PIV cards.

#### Privacy-enhancing Federated Identity

In many cases, relying parties do not need to know the full identity of a subscriber. Relying parties need to request only as much information as they need to complete the transaction requested by the subscriber, and IdPs need to limit what information relying parties have access to within a transaction as per [Section 5.2](https://pages.nist.gov/800-63-3/sp800-63c.html#privacy-reqs). Furthermore, with protocols like OpenID Connect, the attributes of the subscriber can be sent separately from the assertion itself, limiting leakage of this information. 

Pairwise identifiers ought to be used in place of persistent or correlatable identifiers whenever possible (See [Section 6.3](https://pages.nist.gov/800-63-3/sp800-63c.html#ppi)). This limits relying parties in attempts of tracking or identifying individual subscribers across different systems. 

When possible, claim references ought to be used to communicate identity information rather than raw data (See [Section 7.3](https://pages.nist.gov/800-63-3/sp800-63c.html#protecting-information)). For example, if a relying party needs to know whether a subscriber is over eighteen years old, the IdP can respond that the subscriber is over eighteen without sharing the subscriber's age or birthdate.

#### Parallel Authentication

In some cases a relying party may wish to confirm certain aspects of a subscriber's identity above and beyond what the IdP provides. For example, a relying party could log in a subscriber using an IdP, receive a picture of the subscriber from the IdP, and require that an in-person agent verify that the picture matches the identity of the person authenticating. This use case is known as "parallel authentication" because two authentication events are happening next to each other: the assertion, and the verification of the biometric (photo) by a trusted agent. The focus of FAL is primary on the assertions being passed from the IdP to the RP, so most authentication events occurring at the RP would not affect the FAL of the transaction. 

At FAL3, holder-of-key transactions occur by verifying both the assertion from the IdP as well as the subscriber's presentation of proof of their personal key attested to in the assertion. 

### Brokered Identity Management

Some federated identity architectures are based on brokered identity management described in [Section 5.1.4](https://pages.nist.gov/800-63-3/sp800-63c.html#proxied), where a single broker intermediates transactions between registered IdPs and RPs. In this architecture, each entity in the system only has to register with one broker in order to interoperate with everyone else in the system. It also means that an IdP can authenticate a subscriber without knowledge of which RP requested the authentication event.

Recent advances in automated registration processes have made IdP/RP integrations much less onerous than they used to be. It is possible for an IdP and RP to register with each other in a very short amount of time without any manual processes. This has lessened the value of brokered identity architectures, since interoperability can be simple and fast even without a central broker.

While brokered identity management systems may appear to protect privacy by blinding an IdP from an RP, keep in mind that the broker itself is aware of all the parties involved in the transaction, and in some cases can see personally identifiable information about subscribers. Brokered identity management systems do not prevent subscriber tracking all together, they merely shift the ability to track subscribers from the IdPs and RPs to the broker.

Additionally, because brokers have access to active valid identity assertions, they are capable of impersonating subscribers. This increases the risk inherent in the entire architecture, since the broker represents a single point of failure which, if it is compromised, can in turn compromise every participant in the system.

NIST has been promoting privacy-enhancing technology in the brokered identity management space through the [Privacy-Enhanced Identity Federation project](https://nccoe.nist.gov/projects/building-blocks/privacy-enhanced-identity-brokers). This NIST building block outlines a set of goals which would constitute a new kind of brokered architecture. This architecture leverages a broker which cannot impersonate or track subscribers. This architecture is still theoretical, and may allow for a privacy-preserving and secure version of brokered identity management in the future.

