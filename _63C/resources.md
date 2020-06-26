---
layout: default
title:  Federation Resources
permalink: /63C/Resources
navOrder: 6  
navTitle: Resources  
---

# C.6 Educational Resources {#s-c-6}

All specifications for identity federation standards mentioned in this resource guide are freely available online:

[OAuth 2 (RFC 6749)](https://tools.ietf.org/html/rfc6749])  
[OpenID Connect](http://openid.net/connect/)  
[Security Assertion Markup Language](http://saml.xml.org/saml-specifications)

These specifications outline multiple, sometimes mutually exclusive, ways to implement federated identity. Therefore, it's important to read the specifications in their entirety before creating an implementation and to follow community best practices.

Federation standards communities actively track known vulnerabilities in existing standards. 

The IETF lists OAuth Security Concerns in in [RFC 6819](https://tools.ietf.org/html/rfc6819) and hosts a [working group](https://tools.ietf.org/wg/oauth/) to track OAuth standards and vulnerabilities.

The OpenID Foundation lists OpenID Connect security concerns [within the specification itself](http://openid.net/specs/openid-connect-core-1_0.html#Security) and hosts a [working group](http://openid.net/wg/connect/) which actively tracks vulnerabilities.

OASIS has published [SAML Privacy and Security Considerations](http://docs.oasis-open.org/security/saml/v2.0/saml-sec-consider-2.0-os.pdf) and hosts a [mailing list](https://lists.oasis-open.org/archives/security-services/) to track SAML vulnerabilities.

## C.6.1 Communicating with Stakeholders {#s-c-6-1}

Stakeholders need to be aware that selecting an FAL is part of a larger risk- and resource-management process. While it is tempting for stakeholders to request the highest level of security, that is not always in the best interest of the organization. Federated identity projects at higher FALs can be long and complicated, and such complications can take resources away from other work that a security team could be doing that would be of greater benefit to the organization.

Many organizations today operate at FAL1, which is sufficient for most use cases. FAL1 is the industry standard, and there are many libraries and off-the-shelf products that can help an organization implement an FAL1 conformant federated identity system.

Conformance to FAL2 or FAL3 is appropriate for some business cases where there is a risk of fraudulent activity which would be prevented by token encryption, or when the transactions protected by the login is of particularly high value to warrant the additional complexity.
