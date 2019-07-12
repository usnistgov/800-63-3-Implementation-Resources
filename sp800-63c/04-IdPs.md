---
layout: default
title:  Guide for Identity Providers
collection: 63C
permalink: /63C/IdP
navOrder: 4  
navTitle: IdPs  
---

### Guidance for Identity Providers

The nature of federation protocols allows the IdP to specialize in security in a way that benefits all RPs that connect to it. With traditional application security methods, such as having a password on each RP, every RP is fully responsible for its security. However, due to common practices like password reuse, compromise of a single RP can lead to the compromise of many other RPs for a given account. In a federation network, the identity provider (IdP) is the only party that can assert the presence and validity of subscribers and their attributes. The compromise of a single RP does not cascade through the network. Instead, the security of all subscribers rests on the security of their IdP. Consequently, a compromise of the IdP will affect all downstream parties. As such, it is vitally important that the IdP be held to the highest of security standards in implementation and deployment. 

#### Purpose

As the lynchpin of security in a federation network, IdPs have the difficult task of keeping track of both subscribers and RPs, and connecting them in a secure fashion with a federation protocol. However, unlike RPs that are trying to provide a service or application, the IdP's primary purpose is to act as a security component for the rest of the federation. As a specialty service, it makes sense to invest heavily in good security practices.

#### General Guidance

IdPs manage the primary authenticators and authentication processes for subscribers in a federation. Guidance for managing such authentication can be found in [[SP 800-63B]], all of which needs to be applied at the IdP. In particular, IdPs ought to implement phishing-resistant technologies in subscriber-facing pages and may want to consider the use of heuristic or risk-based security for all connections, including APIs. Additionally, the attributes and identities asserted by the IdP are subject to whatever verification practices the IdP uses. Guidelines for such identity proofing and verification are found in [[SP 800-63A]]. 

Much of the technical friction in setting up a federation stems from IdPs which are built and configured in such a way that onboarding new RPs requires a significant amount of manual human intervention [[section 5.1.1]]. Any time there is unwarranted friction in a security process, the consumers of that process (in this case RP implementors) will often find creative and usually-insecure workarounds to that process. Much of this friction is removed when IdPs support automated discovery mechanisms and simple automated registration [[section 5.2.2]]. In order to ease RP onboarding, IdPs ought to make their configurations discoverable in a machine-readable format over a secure protected channel, as appropriate to the protocol in use. 

IdPs need to use approved cryptographic systems to generate all key material [[section 4.1]]. IdPs also need to securely store all private key material in such a way that attackers, RPs, end users, and other parties do not have access to the private key. Public keys need to be made available to RPs over authenticated protected channels or via trusted out of band processes, such as hand configuration by a systems administrator. An IdP can use a single key pair across different RPs on the network, and the keys can be rotated on a regular basis.

The IdP's private keys, which are used to sign assertions, need to be protected from subscribers, RPs, and other unintended parties. If the IdP's private keys are compromised, an attacker could generate arbitrary assertions and impersonate any subscriber on the network at any RP. If an RP's keys are compromised, an attacker could impersonate a request from that RP but not attack any other RPs or the IdP itself. 

IdPs have to securely store any symmetric secrets used by RPs in a fashion that reduces the likelihood of their capture, such as by storing a hash of the secret instead of the secret itself. All symmetric secrets need to be generated using approved cryptography, and a different secret needs to be generated for every RP that the IdP associates with. Similarly, if an RP talks to multiple IdPs, it has to have a separate secret for each IdP. 

If an IdP provides public and private keypairs to subscribers or RPs, the IdP need to store only the public portion of the key. 

#### Guidance by Product Family

This document covers two main product families that enable federated identity transactions - SAML and OpenID Connect, the latter of which is built on top of OAuth. Other protocols and approaches are possible to use while fulfilling the requirements of the guidelines.

##### SAML

Both IdPs and RPs ought to publish metadata in a well-known location. While there is no widely accepted standard for SAML metadata exchange, it is advisable to use a well-documented metadata endpoint to serve the IdPs metadata in the form of a single XML file to any RP who wishes to consume it.

The IdP needs to always check signatures on metadata, and only accept metadata that has been signed by the presenting RP.

Identity federations like [InCommon](https://www.incommon.org/) share the metadata of hundreds of IdPs and RPs in a structured manner [[section 5.1.3]]. Adding an IdP's metadata to such federations will help RPs to find it easily.

Apply best practices to protect subscriber information. All SAML assertions containing personally identifiable information ought to be encrypted to the relying party to protect the PII from being leaked to the browser. Assertions containing only authentication information and no personally identifiable information can relax this encryption requirement.

##### OpenID Connect

IdPs can use OpenID Connect's discovery mechanism, published in JSON format at an HTTPS location ending in `/.well-known/openid-configuration` as specified in the OpenID Connect discovery specification. The discovery document contains all of the information that an RP would need to interact with the server. This document is usually made available in a location based on the IdP's unique issuer URL.

If personally identifiable information is bundled with authentication information in a token, it ought to be protected through encryption of the ID Token or use of a back-channel presentation mechanism. If personally identifiable information is made available at the UserInfo Endpoint, such assertions need not be encrypted but have to instead be passed over an authenticated protected channel (HTTPS and TLS).

It is recommended that OpenID Connect IdPs support a dynamic client registration to make it easy for RPs to register without manual intervention. Note that dynamic registration does not release data to the RP, it merely allows the RP to ask for login to be authorized at runtime [[section  4.2]].

There is a test suite for OpenID Connect providers to verify whether their instance of OpenID Connect is compliant with the standard, available from [http://openid.net/certification/testing/](http://openid.net/certification/testing/). 

The OpenID Connect community has reviewed libraries in several different languages to search for bugs and non-compliant processes, available at [http://openid.net/developers/libraries/](http://openid.net/developers/libraries/). Whenever possible, leverage these libraries in development.
 
OpenID Connect relies heavily on the [JOSE standard](https://datatracker.ietf.org/wg/jose/about/), particularly JWT and JWK. All tokens an keys in an implementation have to conform to those standards. It is recommended that IdPs use an established JOSE and JWT library to ensure all appropriate checks have been made during implementation. 

Additional security standards like [token binding](https://datatracker.ietf.org/wg/tokbind/documents/) and [proof key for code exchange](https://tools.ietf.org/html/rfc7636). While those standards are not factors in determining the FAL of an OpenID Connect IdP, they considered to be best practice in the industry.

