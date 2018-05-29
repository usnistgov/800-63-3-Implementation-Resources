---
layout: default
title:  SP 800-63A
collection: 63A
permalink: /63A/
---
NIST Special Publication 800-63-A Digital Identity Guidelines: Enrollment and Identity Proofing (SP 800-63 or NIST SP 800-63A) provides detailed requirements for enrollment and identity proofing of individuals with which federal identity management systems are expected to comply.

The tools and resources here provide non-normative guidance to agencies and service providers on techniques to implement identity management systems which are aligned with the requirements contained in NIST SP 800-63A. These resources leverage examples and illustrative cases to provide practical and actionable guidance to readers.

Identity proofing is the process by which a Credential Service Provider (CSP) collects and verifies information about a person for the purpose of issuing credentials to that person, as illustrated in the figure below. These processes, consistent with the requirements in NIST SP 800-63-3, are intended to help agencies achieve the following objectives:

- **Resolve** a claimed identity to a single, unique identity within the context of the population of users served by the CSP.
- **Validate** that all evidence that is supplied is valid (correct) and genuine (not counterfeit or misappropriated); and that the claimed identity exists in the real world.
- **Verify** that the claimed identity is associated with the real person supplying the identity evidence.

![Identity Proofing Process Flow]({{site.baseurl}}/img/ProofingProcess.png)

Please note that while the diagram above illustrates the identity proofing process as a roadmap composed of concrete successive steps, it is meant more generally to convey the relationships between the different objectives and their definitions. In reality, collection of evidence for these steps can often take place concurrently, with no additional evidence collected beyond the initial steps in enrollment, which is both used for identity resolution and validated.
