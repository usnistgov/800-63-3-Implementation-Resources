---
layout: default
title:  Verification
collection: 63A
permalink: /63A/Verification
---
The goal of identity verification is to confirm and establish a linkage between the claimed identity and the physical, live existence of the person actually presenting the evidence. This can be done by a physical or biometric comparison, or a KBV challenge, or by authenticating the applicant with methods and credentials that are appropriate for the level of assurance.

The following table presents the verification methods that should be considered to achieve a given level of strength of fair or above. The requirements for these levels have been outlined in Table 5-3 in SP800-63A.

**Table: Verification Methods and Strengths**

| **Strength** | **Method** | **Description** |
| --- | --- | --- |
| Superior | Biometric Verification | Comparison against strongest piece of evidence, remote or in-person |
| Strong | In-Person Physical Verification | Physical comparison to photograph against strongest piece of evidence |
| Strong | Remote Physical Verification | Physical comparison to photograph against strongest piece of evidence |
| Fair | Knowledge-Based Verification | Comparison of challenge response provided by applicant against known information, remote or in-person |

Biometrics can play a key role in identity proofing and verification of individuals. This utility can come in multiple stages of the identity proofing process.

In enrollment, agencies can capture biometrics in the form of fingerprints, face, iris images, etc. They can compare requirements with their options to identify which single or multi-modal biometric solution can best respond to their needs and implement the system accordingly.

**Table: Biometric Verification**

| Verification  | Strength | Example | Considerations |
| --- | --- | --- | --- |
| Biometric comparison of image of user to photo in issuer or authoritative records | Superior | The image of the user captured via a device (e.g., mobile or laptop camera) is comapred using an automated matching process to a picture stored in records (e.g., DMV database). | While less vulnerable to falisfied evidence, this is still subject to spoofing and other presentation attacks. Inclusion of PAD and image quality requirements can mitigate some of these risks. |
| Biometric comparison of image to template stored on evidence | Superior |  |  |
| Biometric comparison of image of user to photo on evidence | Strong | Using an automated matching process to compare the image of a user captured via a device (e.g., mobile device or laptop camera) to a picture on the piece of evidence.   | Approach is vulnerable to the user presenting a forged piece of evidence or presentation attacks featuring stolen images of the user or evidence. When instituting agencies should consider additional mitigation measures to help prevent such attacks, including Presentation Attack Detection (PAD), device analytics, and image quality requirements.  |
| Physical comparison by trained professional | Strong | A trained professional physically examines presented evidence and compares to the user to verify they are the same indivdual.  | Subject to human error, training of individuals in proper recognition and comparison techniques can help to mitigate some of this risk.  |
| Physical comparison by trained professional done remotely | Strong | A trained professional examines the evidence via a live and protected video session with the applicant to verfiy the indvidual presenting the evidence is the same individual on the evidence.  | Subject to both human error and technical diffculties. Incoprporation of technology aides, image quality requirements, and training can be leveraged to mitigate these threats. See section 5.3.3.2 for requirements associated with "Supervised Remote In-Person Proofing" events. |
| Knowledge Based Verification  | Fair | KBV leverages the users knoweldge of information associated with a piece of evidence to confirm their posession or association with it. This can be done through knowledge of recent transactions or responding to questions associated with the evidence.  | Knowledge Based Verification can be done to link an individual to a fair piece of evidence. However, since IAL2 requires the stronged piece of evidence to be verified, there is limited value in verification of "fair" evidence. |


