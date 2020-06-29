---
layout: default
title:  SP 800-63A
permalink: /63A/
navOrder: 1 
navTitle: Introduction  
---

# A.1 Introduction {#s-a-1}

NIST [Special Publication 800-63A](https://pages.nist.gov/800-63-3/sp800-63a.html) *Digital Authentication Guideline: Enrollment and Identity Proofing* provides detailed requirements for enrollment and identity proofing of individuals into digital identity systems. 

This document provides informational guidance for the implementation of services, controls and normative requirements presented in SP 800-63A. This document represents non-normative, supplemental guidance to facilitate the implementation of digital identity systems which are aligned with the requirements contained in NIST SP 800-63A. This guide contains examples and illustrative cases to provide practical and actionable guidance to readers. It is complemented by the following additional implementation resources, which, taken in their entirety, provide an end-to-end vision for federal identity and access management solutions:

- SP 800-63B Authentication and Lifecycle Management Implementation Guide
- SP 800-63C Federation Implementation Guide
- SP 800-63A Conformance Criteria for IAL2 and IAL3
- SP 800-63B Conformance Criteria for AAL2 and AAL3

These documents support the overall vision of NIST SP 800-63-3 by enabling a more comprehensive understanding for the implementation of conformant digital identity solutions, operations and systems.  These documents also do not restrict the manner in which agencies choose to comply with NIST SP 800-63, nor are they intended to restrict agencies from identifying and implementing controls based on an informed and comprehensive risk management process consistent with the NIST Risk Management Framework.

These guidance documents are organized by topic area to facilitate reference. The text of each topic area cites the pertinent sections of the SP 800-63-3 document suite covered in the supplemental guidance. This guidance may be used in combination with the companion SP 800-63A and SP 800-63B Conformance Criteria. The Conformance Criteria present detailed guidance for each normative requirement and control presented in SP 800-63A and SP 800-63B for IAL2 and IAL3 and AAL 2 and AAL3. Together these sets of informative guidance are intended to facilitate the understanding, implementation, and assessment of conformant digital identity systems and operations.

As technology continues to improve and solutions evolve, agencies are encouraged to explore new techniques and options for mitigating risk, so long as these actions are informed, well documented, and authorized by the appropriate authorities. NIST further encourages readers and implementers to provide feedback and lessons learned to the authors of this document to ensure this guide remains relevant and useful, and to ensure the core Digital Identity Guidelines are updated with new requirements as they are identified.

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
