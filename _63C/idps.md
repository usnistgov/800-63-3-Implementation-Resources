---
layout: default
title:  Guide for Identity Providers
permalink: /63C/IdP
navOrder: 4  
navTitle: IdPs  
---

# C.4 Guidance for Identity Providers {#s-c-4}

While every RP is responsible for its own internal security, the nature of federation protocols allows the IdP to specialize in security in a way that benefits all RPs that connect to it. With traditional application security authentication methods, security breaches can cascade between systems. Common practices like password reuse allow the compromise of a single RP to lead to the compromise of many other RPs for a given account. In a federation network, the identity provider (IdP) is the only party that can assert the presence and validity of subscribers and their attributes. The compromise of a single RP does not cascade through the network. 

As the linchpin of security in a federation network, IdPs have the difficult task of keeping track of both subscribers and RPs as well as connecting them in a secure fashion with a federation protocol. Compromise of the IdP will affect all downstream RPs. However, unlike RPs that are trying to provide a service or application, the IdP's primary purpose is to act as a security component for the rest of the federation. As such, it is vitally important that the IdP be held to the highest of security standards in implementation and deployment. As a specialty service, it makes sense to invest heavily in good security practices.

## C.4.1 General Guidance {#s-c-4-1}

IdPs manage the primary authenticators and authentication processes for subscribers in a federation. Guidance for managing such authentication can be found in [SP 800-63B](https://pages.nist.gov/800-63-3/sp800-36b.html), all of which applies to the IdP. In particular, IdPs need to manage and store subscriber credentials appropriately for the types of credentials in use. IdPs also ought to implement phishing-resistant technologies in subscriber-facing pages and may want to use risk-based security methods for all connections, including any hosted identity APIs. 

Additionally, the attributes and identities asserted by the IdP are subject to whatever verification practices the IdP uses. Guidelines for such identity proofing and verification are found in [SP 800-63A](https://pages.nist.gov/800-63-3/sp800-63a.html). Since IdPs manage subscriber attributes, including PII, IdPs need to protect all such attributes to ensure they are not divulged to attackers or other unintended parties. An IdP must also follow data minimization practices and not divulge more attributes about a subscriber than are necessary to fulfill the identity request and affect a successful login.

Much of the technical friction in setting up a federation stems from IdPs which are built and configured in such a way that onboarding new RPs requires a significant amount of manual human intervention (See [Section 5.1.1](https://pages.nist.gov/800-63-3/sp800-63c.html#manual-registration)). Any time there is unwarranted friction in a security process, the consumers of that process (in this case, RP implementors) will often find creative and usually-insecure workarounds to that process. Much of this friction is removed when IdPs support automated discovery mechanisms and simple automated registration (See [Section 5.1.2](https://pages.nist.gov/800-63-3/sp800-63c.html#dynamic-registration). In order to ease RP onboarding, IdPs ought to make their configurations discoverable in a machine-readable format over a secure protected channel, as appropriate to the protocol in use. Registration of new RPs can be streamlined through developer portals and dynamic registration systems at the IdP.

IdPs need to use approved cryptographic systems to generate all key material as per [Section 4.1](https://pages.nist.gov/800-63-3/sp800-63c.html#key-mgmt). IdPs also need to securely store all private key material in such a way that attackers, RPs, end users, and other parties do not have access to the private key.  An IdP can use a single asymmetric key pair across different RPs on the network, and the keys can be rotated on a regular basis to further prevent the chance or forgery. The IdP's Public keys ought to be made available to RPs over authenticated protected channels to allow RPs to fetch the keys when needed, especially if the IdP rotates its keys. The public keys can also be transferred via a trusted out of band processes, such as hand configuration by a systems administrator.

The IdP's private keys, which are used to sign assertions, need to be protected from subscribers, RPs, and other unintended parties. If the IdP's private keys are compromised, an attacker could generate arbitrary assertions and impersonate any subscriber on the network at any RP. While an RP's keys also need to be protected, the possible damage is much less. If an RP's keys are compromised, an attacker could impersonate a request from that RP but not impersonate any other RPs or the IdP itself. 

IdPs have to securely store any symmetric secrets used by RPs in a fashion that reduces the likelihood of their capture, such as by storing a hash of the secret instead of the secret itself. All symmetric secrets need to be generated using approved cryptography, and a different secret needs to be generated for every RP that the IdP associates with. Similarly, if an RP talks to multiple IdPs, it has to have a separate secret for each IdP and not re-use them.

If an IdP provides public and private keypairs to subscribers or RPs, the IdP need to store only the public portion of the RP's key. This practice prevents the IdP becoming a potential attack target for this key material.

## C.4.2 Guidance by Product Family {#s-c-4-2}

This document covers two main product families that enable federated identity transactions - SAML and OpenID Connect, the latter of which is built on top of OAuth. Other protocols and approaches are possible to use while fulfilling the requirements of the guidelines.

### C.4.2.1 SAML {#s-c-4-2-1}

Both IdPs and RPs ought to publish metadata in a well-known location. While there is no widely accepted standard for SAML metadata exchange, it is advisable to use a well-documented metadata endpoint to serve the IdPs metadata in the form of a single XML file to any RP who wishes to consume it.

The IdP needs to always check signatures on metadata and to only accept metadata that has been signed by the presenting RP.

Identity federations like [InCommon](https://www.incommon.org/) share the metadata of hundreds of IdPs and RPs in a structured manner as per [section 5.1.3](https://pages.nist.gov/800-63-3/sp800-63c.html#authorities). Adding an IdP's metadata to such federations will help RPs to find it easily.

Apply best practices to protect subscriber information. All SAML assertions containing personally identifiable information ought to be encrypted to the relying party to protect the PII from being leaked to the browser. Assertions containing only authentication information and no personally identifiable information can relax this encryption requirement.

### C.4.2.2 OpenID Connect {#s-c-4-2-2}

IdPs can use OpenID Connect's discovery mechanism, published in JSON format at an HTTPS location ending in `/.well-known/openid-configuration` as specified in the [OpenID Connect discovery specification](https://openid.net/specs/openid-connect-discovery-1_0.html). The discovery document contains all of the information that an RP would need to interact with the server. This document is usually made available in a location based on the IdP's unique issuer URL, and a single discovery location should be considered canonical for a given IdP.

If personally identifiable information is bundled with authentication information in an ID Token, it ought to be protected through encryption of the ID Token or use of a back-channel presentation mechanism. If personally identifiable information is made available at the UserInfo Endpoint, the ID Token need not be encrypted. All back-channel communications have to pass over an authenticated protected channel, such as HTTPS over TLS with server certificate validation.

It is recommended that OpenID Connect IdPs support a dynamic client registration to make it easy for RPs to register without manual intervention. Note that dynamic registration does not release any subscriber data to the RP, it merely allows the RP to ask for login to be authorized at runtime (See [Section  4.2](https://pages.nist.gov/800-63-3/sp800-63c.html#runtime)).

The OpenID Foundation has made a test suite available for OpenID Connect providers to verify whether their instance of OpenID Connect is compliant with the standard, available from [http://openid.net/certification/testing/](http://openid.net/certification/testing/). 

The OpenID Connect community has reviewed libraries in several different languages to search for bugs and non-compliant processes, available at [http://openid.net/developers/libraries/](http://openid.net/developers/libraries/). Whenever possible, developers should leverage these proven libraries in development.
 
OpenID Connect relies heavily on the [JOSE standard](https://datatracker.ietf.org/wg/jose/about/), particularly JWT and JWK. All tokens an keys in an implementation have to conform to those standards. It is recommended that IdPs use an established JOSE and JWT library to ensure all appropriate checks have been made during implementation. 

IdPs should implement additional security standards such as [MTLS for OAuth 2](https://tools.ietf.org/html/rfc8705) and [Proof Key for Code Exchange (PKCE)](https://tools.ietf.org/html/rfc7636) to enable higher security interactions. While such standards are not factors in determining the FAL of an OpenID Connect IdP, they considered to be best practice in the industry.
