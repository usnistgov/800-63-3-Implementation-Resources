---
layout: default
title:  Choosing Security Parameters
collection: 63C
permalink: /63C/SecurityParameters
navOrder: 2  
navTitle: Parameters  
---

### Choosing Security Parameters

Different federation protocols and implementations of those protocols have many options that lead to different outcomes in the security of a system. All of these options have trade-offs in terms of complexity, robustness, and other characteristics. Choosing the right set of options for a given situation helps ensure that transactions will be as secure, functional, and efficient as possible.

### Selecting a Federation Assurance Level (FAL)

The Federation Assurance Level (FAL) defined in SP 800-63C [[section 4]] provides a set of requirements for federation transactions. These requirements are grouped into an ascending scale of three levels: FAL1, FAL2, and FAL3. Each successive level includes all the features of lower levels and adds additional requirements on top of them. 

FAL1 provides a solid basis for federation and is appropriate for the vast majority of use cases. Most off-the-shelf products operate at FAL1 today without additional features. Most common deployments of SAML and OpenID Connect fulfill all the requirements of FAL1 today. FAL1 requires that all assertions be signed, time limited, and audience-restricted to prevent an assertion intended for one relying party to be replayed at another. 

FAL2 provides an extra layer of security by requiring that the assertion be encrypted so that the RP is the only party that can decrypt it. This protection is required if personally identifiable information will be sent in an identity assertion, as personally identifiable information needs to be protected in transit and an assertion is sometimes borne by intermediate parties in a transaction, such as a browser. This level requires that the IdP manage an encryption key for the RP, which necessitates additional complexity for both parties. The keys could be managed with a traditional PKI infrastructure that relies on a trusted certificate authority, but with many protocols the keys can be instead registered directly between parties. The RP also needs to manage and protect its decryption keys in order to read the information in the assertion. If the client's private decryption keys are leaked to another party, the additional protections provided by FAL2 no longer apply. 

FAL3 is intended to be forward-looking and is not yet readily available in off-the-shelf standards and products. FAL3 provides an additional layer in the form of a cryptographic key that are presented by the subscriber in addition to the signed and encrypted assertion itself. This level requires that the IdP manage references to keys representing the subscriber at each RP in addition to managing the keys for the RPs themselves. The IdP needs to correctly associate the subscriber's key to the correct RP in the assertion, and the RP needs to be able to process and validate the presentation of the key by the subscriber. This key could be the same key that's presented by the subscriber at the IdP, such as an X.509 certificate, or it could be a separate key with no identity information associated with it that's not used at the IdP, such as a FIDO token. In both cases, the assertion needs to reference the key and the RP needs to ensure the correct key is presented by the subscriber.

### Risk Management

Selecting and conforming to an FAL ought to be part of a larger risk management process and program. Conforming to FAL3 does not make an organization's security infallible, but instead provides protection against particular attacks while incurring certain costs to both the applications and the subscribers. Rather than attempting to make your federation infrastructure conform to the highest standards available, you need to analyze the risks that are inherent in your organization and choose how strongly to protect against them given their severity and likelihood of occurrence.

The additional information management and implementation complexity of higher FALs cannot be ignored, and the costs to all involved have to be weighed against perceived benefits. Unless there is a compelling reason to use the features of higher FALs, FAL1 is the default for most use cases. FAL1 is the industry standard for authentication at this point in time. The risks of implementing a system at FAL1, when compared to higher FALs, may be negligible depending on relevant use cases and attack vectors. When PII needs to be passed, it ought to be passed in a secondary channel where possible instead of in the assertion itself, regardless of the FAL.

Because it is the front door to many critical systems, authentication is a key piece of risk management strategy. Strong federation can protect against many potential subscriber impersonation and man-in-the-middle attacks. Instead of each RP needing to manage subscriber accounts and authenticators separately, creating many vulnerable surfaces, federation concentrates the key security practices in a dedicated component, the IdP. Upgrades to authenticators, software, and practices at the IdP automatically benefit the downstream RPs and the overall network. 

### Personally Identifiable Information (PII)

Personally Identifiable Information (PII) needs to be limited to only what's needed to perform a transaction [[section 7.3]]. For many login transactions, the RP will need to know only an identifier for the current subscriber. After an initial login, this identifier is used by the RP to tie the subscriber to a record in the RP application, and this record often contains attributes collected from various sources including the IdP and direct interaction with the subscriber. 

All assertions contain a subject identifier, which uniquely identifies the subscriber represented by the assertion to the RP. Since the subject identifier is required with every assertion, the subject identifier shouldn't have any PII internally. For example, IdPs wouldn't use usernames, employee numbers, simple sequences, or other easily predictable and correlatable information for the subject identifier. Instead, to prevent PII leakage, IdPs can use approved cryptography to assign random subject identifiers to all users. Alternatively, IdPs could derive subject identifiers from PII using approved cryptography. For example, the IdP could run an internally unique identifier (like an employee number) through an approved hashing function. The output of the hashing function would be the subject identifier, and the PII used to generate it has been protected since it cannot be re-derived from the output of the hashing function.

Assertions at all levels can include additional attributes about the subscriber [[section 6]], potentially including PII. The RP might require some of this information to perform its function, such as an email address to contact a subscriber. However, the RP will not know if it needs information for a given subscriber before that subscriber has been logged in, since the required information could be available locally to the RP without requesting it from the IdP. This presents a dilemma for systems trying to practice data minimization.

Some protocols, such as SAML, require all available attributes be present in the assertion itself. In such cases, the RP needs to be very judicious about which attributes it requests. In other protocols, such as OpenID Connect, attributes can be sent through both the assertion and a secondary channel, the UserInfo endpoint. In OpenID Connect the ID Token serves as the assertion, and by default it contains a non-PII subject identifier for the subscriber. Additional information about the subscriber can be obtained through the UserInfo Endpoint by using an OAuth access token. Since this information is communicated in the back channel from the IdP to the RP over a an authenticated protected channel, it need not be separately encrypted as it is not handled or presented by an intermediary party (though of course it can be encrypted as well).

### Selecting a Presentation Mechanism

Assertions can be sent either over the back channel between the IdP and RP [[section 7.1]] or over the front channel using the subscriber and their browser as an intermediary [[section 7.2]]. While both methods are allowed at all FALs, back channel presentation has a number of advantages and is preferred where possible.

Since the assertion is transmitted directly from the IdP to the RP over an authenticated protected channel, the RP has a high level of assurance that the assertion is from the IdP in question. The RP can also be sure that the assertion is generated in response to a specific authentication request since the RP needs to present an assertion reference to retrieve it. 

Front channel presentation systems are simpler for RPs to implement, as they don't have to handle assertion references or trading them for assertions. As a consequence, front channel presentation systems can be more susceptible to assertion injection, whereby an attacker can present a valid assertion to an unsuspecting RP in order to force a login at that RP, potentially taking over a session. A back channel presentation system is subject only to injection of an assertion reference, which can be more strongly tied to an authentication request. 

To enforce least-privilege and least-knowledge security principles, it is preferable to have each RP request its own assertion instead of re-using one assertion for multiple RPs. With front-channel presentation, it is tempting for a system to create a single assertion to be presented to multiple RPs by the browser. The browser then needs to determine which sites to present the assertion to, and which to request a new assertion for. With a back channel presentation mechanism, only the assertion reference is passed to the RP from the browser. Since the assertion reference is one-time use and limited to a single RP [[section 7.1]], it cannot be used accidentally multiple times at multiple RPs.

Additionally, assertions passed in the front channel are visible to an intermediary party, the browser. The assertion's payload, which intended for consumption by the RP, can include PII attributes, internal security information, or other sensitive data. To avoid untended data leakage, the IdP can employ several techniques:

1. Encrypt the payload to the RP's key, as is required at FAL2 and FAL3.
1. Limit the information contained in the assertion payload to non-sensitive information, and use a secondary mechanism to convey sensitive details such as in Section 2.3.
1. Use a back-channel presentation mechanism to prevent the assertion itself from being seen by the intermediary. 

