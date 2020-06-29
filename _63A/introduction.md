---
layout: default
title:  SP 800-63A
permalink: /63A/
navOrder: 1 
navTitle: Introduction  
---

# A.1 Introduction {#s-a-1}

NIST Special Publication 800-63A _Enrollment and Identity Proofing_ provides detailed requirements and controls for the enrollment and identity proofing of individuals into digital identity systems. These resources provide informational guidance for the implementation of services, controls and requirements presented in SP 800-63A. These implementation resources should be read alongside SP 800-63A.

## A.1.1 Identity Proofing {#s-a-1-1}

Identity proofing is the process by which a Credential Service Provider (CSP) collects and verifies information about a person for the purpose of issuing credentials to that person, as illustrated in Figure 1.
 
[Figure 1: Individual Identity Proofing Journey](introduction.md#fig-1){:name="fig-1"}
{:latex-ignore="true"}

![Individual Identity Proofing Journey]({{site.baseurl}}/{{page.collection}}/images/ProofingProcess.png){:style="width: 1047px;" latex-src="ProofingProcess.png" latex-fig="1"}

These identity proofing processes and associated controls and requirements are presented in NIST SP 800-63A in order to achieve the following processing objectives:

- **Resolve** a claimed identity to a single, unique identity within the context of the population of users served by the CSP.
- **Validate**
    - that all evidence that is supplied is valid (correct) and genuine (not counterfeit or misappropriated); and
    - that the claimed identity exists in the real world.
- **Verify** that the claimed identity is associated with the real person supplying the identity evidence.
