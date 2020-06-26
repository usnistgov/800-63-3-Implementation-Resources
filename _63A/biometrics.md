---
layout: default
title:  'SP 800-63A: Biometrics Collection'
permalink: /63A/biometrics/
navOrder: 7
navTitle: Biometrics
---

# A.7 Biometrics Collection {#s-a-7}

SP 800-63A presents two use cases for the collection of biometrics for purposes of identity proofing and enrollment: biometric matching of biometric data objects contained on identity evidence for the purpose of identity verification; and enrollment and registration of biometric characteristics as an authentication factor in the subscribers' enrollment account for purposes of account recovery and non-repudiation.

Biometric matching of biometric data objects contained on identity evidence for identity verification may be performed to provide binding of the evidence to the applicant for FAIR, STRONG, and SUPERIOR evidence strengths. Biometric collection for this purpose may be performed for in-person or remote identity proofing processes. Biometric matching is one of the optional methods for identity verification of the binding of the applicant to the evidence for FAIR and STRONG evidence verification; biometric matching is required for SUPERIOR verification binding. Therefore, biometrics collection is required for biometrics matching for SUPERIOR evidence verification binding and may be performed for binding FAIR and STRONG evidence whether the identity proofing process is in-person or remote.

Biometrics collection for enrollment and registration of biometric characteristics as an authentication factor in the subscriber's enrollment account for purposes of account recovery and non-repudiation is a requirement for IAL3 enrollment; this is optional for IAL2 account enrollment whether identity proofing is performed in-person or through remote processes.

In-person identity proofing biometrics collection requirements are presented in SP 800-63A section 5.3.3.1. These requirements provide controls against impersonation, presentation, and spoofing attacks. These requirements are also applicable to supervised remote identity proofing processes for IAL3 in-person identity proofing comparability. The in-person biometrics collection requirements of section 5.3.3.1 apply for both use cases described above. While it is envisioned that biometrics collection for remote identity proofing and enrollment for either use cases would principally involve facial image capture, biometrics collection for remote identity proofing and enrollment can be performed for any biometric modality. Remote identity proofing biometrics collection of any modality requires controls against impersonation, presentation, and spoofing attacks. The controls for supervised remote identity proofing presented in SP 800-63A section 5.3.3.2 allow the remote operator to view the applicant for the entire proofing session and inspect the biometric source (e.g., facial image, fingerprint) to detect attempts at spoofing or presentation attack.

If biometrics are collected for either use case described above for IAL2 identity proofing and enrollment, comparable controls to supervised remote proofing biometrics collection are necessary to control against attacks. Potential methods and controls for IAL2 identity proofing biometrics collection:

- Use of a live remote operator and specialized equipment to supervise and video capture the identity proofing and biometrics session similar to the controls for supervised remote identity proofing;
- Use of automated capabilities for biometric collection and comparison that also employ liveness detection technologies.

These methods for IAL2 remote identity proofing biometric collection and comparison are described in more detail in the Identity Verification section of these SP 800-63A Implementation Resources.
