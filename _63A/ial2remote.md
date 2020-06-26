---
layout: default
title:  'SP 800-63A: IAL2 Remote Identity Proofing'
permalink: /63A/ial2remote/
navOrder: 10
navTitle: IAL2 Remote
---

# IAL2 Remote Identity Proofing

> Note: This section of the SP 800-63A Implementation Resources repeats some of the text of other sections of the Implementation Resources as it is anticipated that this section for IAL2 remote identity proofing may be used as a stand-alone resource.

Identity proofing of applicants without requiring them to physically meet in person with CSP personnel is an important but challenging capability. It is important in providing access to CSP services to a larger portion of the population and in reducing the costs to both the applicant and the CSP. It is challenging because many of the identity proofing methods available to the CSP in a face-to-face interaction, such as detailed inspection of evidence documents, are difficult to perform with comparable security when conducted remotely. The requirements in NIST SP 800-63A for remote identity proofing attempt to strike a pragmatic balance between availability and convenient access to identity proofing services and security of the associated processes.

There are two methods of remote identity proofing that are defined in SP 800-63A.

- Conventional remote identity proofing represents the processes and controls for CSPs to identity proof and enroll applicants remotely at IAL2.
- Supervised remote identity proofing represents the processes and controls for CSPs to provide comparable levels of confidence and security to in-person IAL3 identity proofing for identity proofing processes that are performed remotely. Supervised remote identity proofing requires the use of specialized equipment under the CSPs' control that is deployed to a remote location and specific controls and specialized requirements for comparability to in-person IAL3 proofing processes. Detailed guidance for supervised remote identity proofing is provided in a separate section of the Implementation Resources.

Note that "unsupervised" (conventional) remote identity proofing is not intended to imply the lack of supervision for the identity proofing process, but rather that the specific requirements of supervised remote identity proofing for IAL3 are not required.

Conventional remote identity proofing, which may be used at IAL2, generally involves the applicant (the person undergoing identity proofing) using their own hardware to complete the proofing process. This will typically involve the use of a camera to capture images of the applicant and the evidence they are presenting. When available, devices such as scanners may be used to capture higher-resolution images of the evidence being presented. However, the use of separate devices like scanners may make it more difficult to securely associate the image of the captured evidence with the primary (webcam) session.

## Identity Resolution

Identity proofing begins with the resolution process. The applicant provides attribute information (e.g., name, physical address, date of birth, email address, phone number) to the CSP and one to three forms of identity evidence. In rare cases, the attribute information provided may not resolve to a unique individual; if this is the case, additional attributes may be requested to resolve the ambiguity. If necessary, ambiguities can be resolved through the use of knowledge-based verification (KBV).

### Identity Evidence Collection

Several combinations of evidence quality are accepted at IAL2 as shown in the table below.

IAL2
:   - One piece of SUPERIOR or STRONG evidence depending on strength of original proof and validation occurs with the issuing source, or
    - Two pieces of STRONG evidence, or
    - One piece of STRONG evidence plus two (2) pieces of FAIR evidence

A single piece of Superior or Strong evidence can be used for identity proofing at IAL2 if the evidence itself was issued pursuant to a sufficiently strong identity proofing process and if the CSP validates the evidence directly with the issuing source. See the Notional Strength of Evidence table in the Strength of Evidence section of these Implementation Resources. Strong evidence types that may be considered to meet this level of quality are presented as STRONG+ in that table.

Additional evidence strength combinations at IAL2 are: two pieces of STRONG evidence. or a single piece of Strong evidence along with two pieces of Fair evidence.

## Identity Validation

The objective of identity validation is to determine the authenticity, integrity and accuracy of identity evidence collected from the applicant to support the claimed identity for identity proofing. Identity validation is made up of two process steps: confirming the evidence is authentic and confirming that the data on the identity evidence is valid, current, and related to an actual, live individual.

Evidence validation for authenticity involves examining the evidence for:

- Confirmation of required information completeness and format for the identity evidence type.
- Detection of evidence tampering or the creation of counterfeit or fraudulent evidence.
- Confirmation of security features.

SP 800-63A Table5-2 _Validating Identity Evidence_(5.2.2) presents validation techniques for 5 levels of validation strength, ranging from unacceptable to SUPERIOR. One of the validation techniques that may be used for evidence validation at FAIR, STRONG, and SUPERIOR strength is to confirm that the evidence is genuine using "appropriate technologies". In this case, "appropriate technologies" refers to identity document validation products and services with the capability to perform one or more of the tests for authenticity listed below for the types of identity evidence presented. Such evidence validation products and services may be used for either in-person or remote identity proofing methods. Therefore, such products may be used when the identity evidence is physically presented for in-person proofing or submitted via video or images that are captured via scanner, webcam, or mobile phone camera for remote identity proofing. Such products and services should conduct one or more of the following necessary evidence authenticity tests:

- Test identity evidence for authenticity against document type libraries for information completeness, format, and correctness;
- Test identity evidence for authenticity through tamper and counterfeit detection; and
- Test identity evidence for authenticity by confirming presence and verification of security features for the type of evidence presented.

There are multiple commercial products that can perform these types of document validation capabilities at varying degrees of accuracy and reliability. If a single product cannot perform each of the three genuineness validation tests above, then other products should be used in combination to perform these validation tests or manual intervention and examination would be necessary. SP 800-63A Table5-2 _Validating Identity Evidence_(5.2.2) could be interpreted that use of appropriate technologies as described above alone would be sufficient for evidence validation at validation strengths of FAIR and STRONG. However, in practice most document validation products require some degree of manual intervention to resolve data collisions and evidence conflicts in order to proceed with identity proofing processes. Manual intervention to resolve collisions and conflicts most likely would require trained personnel from the product vendor or CSP personnel, depending on the type of product or service and any associated service level agreements.

Manual validation of identity evidence, particularly the confirmation of integrity of physical security features of the evidence, is particularly challenging when done remotely without specialized equipment. For example, some security features involving the texture of a printed medium and verification of the existence and quality of microprinting may not be remotely verifiable. Others like holographic coatings and color-shifting inks may be dynamically verifiable on a live video connection between applicant and proofing agent.

Therefore, the validation of evidence that may be submitted remotely for remote identity proofing methods is particularly challenging. For this reason, CSPs opting to provide remote identity proofing may find it most effective to use automated evidence validation products and services as described above which are permitted as "appropriate technologies" for evidence validation in SP 800-63A section 5.2.2. If such validation services are not used, operator training for evidence validation will depend on the CSP policies, guidelines and requirements. For this reason, training requirements for evidence validation requirements are not specified in SP 800-63A. Such training is especially important for CSPs that provide for IAL2 remote identity proofing or IAL3 supervised remote identity proofing For these remote identity proofing methods, images of identity evidence are submitted remotely, but the capabilities for evidence validation are very limited as seen in the table of common types of security features presented in the Identity Validation section of these Implementation Resources. If automated evidence validation solutions are not used, CSPs may choose to apply similar procedures for IAL2 remote proofing as are required for IAL3 supervised remote proofing. These procedures provide that a trained operator can remotely supervise the evidence collection process, require the applicant to turn or tilt evidence or apply lighting to be able to confirm security features on evidence that is presented for the identity proofing encounter in a recorded video or webcast. Alternatively, a CSP may use an automated interface for the capture of identity evidence images that similarly can direct the applicant to turn, tilt or provide lighting on evidence presented for identity proofing purposes. Therefore, the training for personnel involved in the validation of evidence for remote proofing methods will depend on the CSPs' policies and procedures. Regardless, the confirmation of genuineness of identity evidence presented to support the claimed identity for identity proofing is critical and necessary for identity validation.

## Evidence Information Validation

The second step in identity validation is to validate the correctness of information from the identity evidence against the issuing source for the evidence or an authoritative source that has linkage to the issuing source. This step applies to evidence validation at the STRONG and SUPERIOR Strengths (5.2.2): _All personal details and evidence details have been confirmed as valid by comparison with information held or published by the issuing source or authoritative source(s)._ It should be noted that the validation of all personal details and evidence details may not be possible for some types of common identity evidence. For example, state motor vehicle departments and driver's license verification services can typically verify issuing state and license number but may only be able to validate selected personal and document information from the license. Therefore, the CSP may not be able to validate all personal details and evidence information on the evidence but must validate all information that can be validated with the issuing or authoritative sources.

The results of identity evidence information validation and evidence genuineness validation should be recorded in enrollment records or audit logs as appropriate for the CSP.

### Identity Binding Verification

Verification of identity evidence is the process of confirming that the evidence, previously shown to be valid, actually refers to the applicant that is appearing for identity proofing; SP 800-63A refers to this as verification of the binding of the validated identity evidence to the applicant. As with evidence requirements for resolution and validation requirements above, verification requirements depend on the quality being ascribed to the evidence.

Verification generally applies to the evidence set as a whole. For example, if the applicant has three pieces of evidence and they all refer to the same person (which they always should), it is only necessary to perform verification against the strongest piece of evidence in the set, and at the corresponding strength of that piece of evidence.

The applicant's binding (i.e., ownership) to the validated identity evidence may be verified by comparison of the applicant to the strongest piece of identity evidence collected to support the claimed identity (e.g., typically a drivers' license, ID, or passport with a facial image photograph) by:

- physical comparison, using appropriate technologies, to a photograph, or
- biometric comparison, using appropriate technologies.

Physical comparison is a comparison by a person (i.e., CSP-trained personnel) of the applicant to the photograph (i.e., facial image) on any of the strongest piece(s) of validated identity evidence collected. This comparison can be an in-person comparison for in-person identity proofing processes or may be conducted remotely for remote identity proofing. In both cases, the operator must perform a physical comparison of the applicant to the facial image photograph on the evidence. That is, the in-person proofing personnel will physically compare the facial image of the live applicant to the photograph of facial image on the strongest piece of validated evidence. For remote physical comparison, the applicants' facial image may be captured by high resolution video or camera for physical comparison to the facial image photograph on the identity evidence. For remote facial image capture, the requirements of SP 800-63B, section 5.2.3. shall be applied and the methods for remote facial image collection and comparison are discussed below.

Biometric comparison is an automated comparison of a biometric characteristic (e.g., facial image, fingerprint, iris) collected and recorded as a reference on the strongest piece of identity evidence to a live capture of the same biometric characteristic for comparison.

For IAL2 remote identity proofing processes, either physical comparison or biometric comparison may be performed for identity verification based on the strongest piece of validated identity evidence. Remote identity proofing requires the collection of both an image of the identity evidence and a live capture of the facial image of the applicant for physical or biometric comparison. The CSP must employ liveness detection capabilities to ensure that the applicant's facial image used for comparison is "live" and not a spoofing or presentation attack. There are considerable risks of impersonation, presentation and spoofing attacks without mitigating controls to ensure live capture of the applicants' facial image. Potential methods for the determination of live facial image capture for remote proofing involve supervision by trained personnel and automated capabilities for liveness detection are presented below.

- A remote operator may supervise the identity proofing session (similar to the processes of supervised remote identity proofing (5.3.3.2)) and may conduct a real-time physical comparison between the image of the identity evidence and a live video of the applicant. In order to confirm the video stream is live and not pre-recorded, the operator may direct the applicant to move their head in specific ways, raise or lower eyes, or ask the applicant questions requiring response during the live capture video. Once a positive confirmation is recorded from the operator, and all other requirements are met, the identity verification may be completed in a single session.
- The CSP may employ automated capabilities which are specifically designed to compare the image of the identity evidence with the applicant and also employ liveness detection technologies. Pending a positive confirmation from the automated comparison, and the satisfaction of all other requirements, identity verification can be completed in a single session.
- The CSP may employ liveness detection technology during the capture of the facial image and an off-line operator performs the physical comparison of images captured during the identity proofing session. The identity proofing process may require more than one session with the applicant and is not completed until the operator provides a positive confirmation of the comparison and the other requirements are met.

It is noted that liveness detection is a necessary control whether the identity verification is performed through physical comparison of the live capture of the applicants' facial image to the photograph on the strongest piece of identity evidence or through automated biometric facial image comparison.

### Knowledge-Based Verification

Knowledge-Based Verification is not permitted for in-person identity proofing. However, Knowledge-Based Verification (KBV) may be used under very limited circumstances for remote identity proofing at IAL2. For remote IAL2 Identity proofing, KBV can only be used for the purposes of identity resolution and for identity verification of a single piece of identity evidence at the "fair" level (on the scale of unacceptable, weak, fair, strong, and superior). Due to the wide availability of KBV information and, therefore, KBV answers to potential impostors, KBV presents very limited strength to the verification process. The objective of the verification phase in identity proofing is to bind the validated identity evidence from the validation phase of identity proofing to the real-world identity of the applicant. Since IAL2 requires identity evidence of at least the "strong" level and, therefore, verification of binding at least at the "strong" level, KBV could never be used exclusively for verification of such binding. Additional verification of such binding is always required for identity evidence beyond KBV in order to meet IAL2 for SP 800-63A. Therefore, the CSP may use KBV for verification of binding to FAIR identity evidence at IAL2 as additional assurance for identity verification of binding to the applicant but could not be used as the sole or principal form of verification.

### Remote Identity Proofing Address Confirmation

Due to the risks and challenges presented by remote identity proofing, an additional requirement to the identity proofing steps for identity resolution, validation, and verification is required for remote identity proofing. For remote identity proofing, an enrollment code must be sent to a validated address for the applicant. The validated address may be postal address, SMS address, or email address. Enrollment codes are used for further confirmation of the binding of validated identity evidence (i.e., validated address) to the applicant. Note that address confirmation is mandatory for IAL2 remote identity proofing but may be performed optionally by CSPs that perform in-person identity proofing at IAL2 and IAL3

There are specific requirements for the security and validity periods for enrollment codes. Enrollment code validity periods are determined by the type of address where the enrollment code is sent, as follows:

- 10 days, when sent to a postal address of record within the contiguous United States;
- 30 days, when sent to a postal address of record outside the contiguous United States;
- 10 minutes, when sent to a telephone of record (SMS or voice);
- 24 hours, when sent to an email address of record.

Applicant enrollment for remote identity proofing processes is not complete until the correct enrollment code is provided by the applicant within the specified validity period.
