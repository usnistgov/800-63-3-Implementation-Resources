---
layout: default
title:  'SP 800-63A: Identity Validation'
permalink: /63A/validation/
navOrder: 4
navTitle: Validation
---

# A.4 Identity Validation {#s-a-4}

The objective of identity validation is to determine the authenticity, integrity and accuracy of identity evidence collected from the applicant to support the claimed identity for identity proofing. Identity validation is made up of two process steps: confirming the evidence is genuine and confirming that the data on the identity evidence is valid, current, and related to an actual, live individual.

## A.4.1 Validation of Evidence Authenticity {#s-a-4-1}

Evidence validation for authenticity involves examining the evidence for:

- Confirmation of required information completeness and format for the identity evidence type.
- Detection of evidence tampering or the creation of counterfeit or fraudulent evidence.
- Confirmation of security features.

SP 800-63A Table5-2 _Validating Identity Evidence_(5.2.2) presents validation techniques for 5 levels of validation strength, ranging from unacceptable to SUPERIOR. One of the validation techniques that may be used for evidence validation at FAIR, STRONG, and SUPERIOR strength is to confirm that the evidence is genuine using "appropriate technologies". In this case, "appropriate technologies" refers to identity document validation products and services with the capability to perform one or more of the tests for authenticity listed below for the types of identity evidence presented. Such evidence validation products and services may be used for either in-person or remote identity proofing methods. Therefore, such products may be used when the identity evidence is physically presented for in-person proofing or submitted via video or images that are captured via scanner, webcam, or mobile phone camera for remote identity proofing. Such products and services should conduct one or more of the following necessary evidence authenticity tests:

- Test identity evidence for authenticity against document type libraries for information completeness, format, and correctness;
- Test identity evidence for authenticity through tamper and counterfeit detection; and
- Test identity evidence for authenticity by confirming presence and verification of security features for the type of evidence presented.

There are multiple commercial products that can perform these types of document validation capabilities at varying degrees of accuracy and reliability. If a single product cannot perform each of the three genuineness validation tests above, then other products should be used in combination to perform these validation tests or manual intervention and examination would be necessary. SP 800-63A Table5-2 _Validating Identity Evidence_(5.2.2) could be interpreted that use of appropriate technologies as described above alone would be sufficient for evidence validation at validation strengths of FAIR and STRONG. However, in practice most document validation products require some degree of manual intervention to resolve data collisions and evidence conflicts in order to proceed with identity proofing processes. Manual intervention to resolve collisions and conflicts most likely would require trained personnel from the product vendor or agency personnel, depending on the type of product or service and any associated service level agreements. Agencies should include these considerations in the evaluation of products and services used for evidence validation for identity proofing.

Identity evidence may contain multiple forms of security features. Some forms of security features may be confirmed through visible inspection, tactile examination, specialized lighting, manipulation (e.g., tilting or turning to allow light refraction), or specialized equipment. Following are descriptions for common types of security features, including the capabilities necessary for confirmation of the security feature.

| Security Feature | Examination Capability | Description |
|---|---|---|
| Fine-line or Guilloche Pattern |Visual| Background pattern of continuous fine lines printed in wavy, overlapping pattern. |
| Ghost image|Visual| Half-tone reproduction of original image (e.g., facial image), may be printed behind printed data. |
| Overlapped data|Visual| Variable data (e.g., signature, seal, text) printed over another field such as facial image or seal. |
| Transparent image|Visual| See-through, window-like image feature (e.g., facial image) visible for both sides of the evidence. |
| Rainbow printing|Visual| Controlled color shifts of printed text in a continuous, linear fashion. |
| Holographic Images|Visual, Tilting| Light field record of objects that will appear and change as view of evidence is tilted and turned. Most state-issued driver's licenses and IDs contain at least one holographic image. |
| Variable laser engraved images|Visual, Tilting| Laser-engraved images at different angles so that image view changes with tilting angle of viewing evidence. |
| Iridescent Inks and Custom Foil Stamping|Visual, Tilting| Custom designs and printing that will change color properties depending on the angle at which evidence is viewed. |
| Laser perforation |Visual, Light, Tactile| Perforated holes made by laser beam to form images. The images can be viewed under light source; image holes have tactile feel. |
| UV printing |Visual, UV Lighting| A UV image or text that can only be viewed with special lighting. UV images may appear on the front or back of the evidence. |
| Microprinting |Visual, Magnifier| Microtext of static or variable data that can be confirmed when viewed under a magnifier. Requires magnification of at least 10X to view.  |
| Laser embossing|Tactile| Use of laser to emboss image or text for tactile feel on only one side of the evidence. |
| Barcode|Visual, Barcode Reader| Machine readable, encoded data (typically personalized printed data) for 2-D barcode, readable with barcode reader. |
| UV printing |Visual, UV Lighting| A UV image or text that can only be viewed with specialized lighting. UV images may appear on the front or back of a card. |
{:latex-columns="p@0.24\textwidth,p@0.30\textwidth,p@0.37\textwidth" latex-longtable="true"}

SP 800-63A (5.2.2) also provides that the genuineness tests above for identity evidence validation may be performed through confirmation of cryptographic security features contained on the evidence in order to meet FAIR and STRONG validation strength; this is a requirement for SUPERIOR validation strength. Such cryptographic security features generally refer to cryptographically signed (e.g., digitally signed) data objects that are stored on an integrated circuit chip on the data evidence that can be used to compare and validate printed information on the evidence. The federal Personal Identity Verification (PIV) Card is an example of this type of evidence. The cryptographically signed data objects on the chip can be used to confirm the personalized data, including facial image, printed on the evidence for evidence validation. Cryptographic security features require specialized equipment to access and validate cryptographically signed data objects on the evidence.

Unless identity evidence validation products and services as described above are used, CSP personnel will need to possess the capabilities to confirm correct information and format, detection of any tampering or counterfeiting, and presence and confirmation of security features for various types of identity evidence that may be presented by applicants. Due to the complexity of evidence validation, SP 800-63A (5.2.2) requires training for CSP personnel that are responsible for evidence validation: _Training requirements for personnel validating evidence SHALL be based on the policies, guidelines, or requirements of the CSP or RP._ CSPs should determine the types and scopes of various types of evidence that may need to be validated and adjust training requirements to address those types of evidence as well as the policies and procedures that are established for the presentation and validation of identity evidence.

Most of the capabilities to confirm security features on identity evidence are dependent upon physically viewing the evidence directly, tactile feel of the evidence, and viewing the evidence under specialized lighting or through the use of specialized equipment. Therefore, the validation of evidence that may be submitted remotely for remote identity proofing methods is particularly challenging. For this reason, CSPs opting to provide remote identity proofing may find it most effective to use automated evidence validation products and services as described above which are permitted as "appropriate technologies" for evidence validation in SP 800-63A section 5.2.2. If such validation services are not used, operator training for evidence validation will depend on the CSP policies, guidelines and requirements. For this reason, training requirements for evidence validation requirements are not specified in SP 800-63A. Such training is especially important for CSPs that provide for IAL2 remote identity proofing or IAL3 supervised remote identity proofing For these remote identity proofing methods, images of identity evidence are submitted remotely, but the capabilities for evidence validation are very limited as seen in the table of common types of security features presented above. If automated evidence validation solutions are not used, CSPs may choose to apply similar procedures for IAL2 remote proofing as are required for IAL3 supervised remote proofing. These procedures provide that a trained operator can remotely supervise the evidence collection process, require the applicant to turn or tilt evidence or apply lighting to be able to confirm security features on evidence that is presented for the identity proofing encounter in a recorded video or webcast. Alternatively, a CSP may use an automated interface for the capture of identity evidence images that similarly can direct the applicant to turn, tilt or provide lighting on evidence presented for identity proofing purposes. Therefore, the training for personnel involved in the validation of evidence for remote proofing methods will depend on the CSPs' policies and procedures. Regardless, the confirmation of genuineness of identity evidence presented to support the claimed identity for identity proofing is critical and necessary for identity validation.

## A.4.2 Evidence Information Validation {#s-a-4-2}

The second step in identity validation is to validate the correctness of information from the identity evidence against the issuing source for the evidence or an authoritative source that has linkage to the issuing source. This step applies to evidence validation at the STRONG and SUPERIOR Strengths (5.2.2): _All personal details and evidence details have been confirmed as valid by comparison with information held or published by the issuing source or authoritative source(s)._ It should be noted that the validation of all personal details and evidence details may not be possible for some types of common identity evidence. For example, state motor vehicle departments and driver's license verification services can typically verify issuing state and license number but may only be able to validate selected personal and document information from the license. Therefore, the CSP may not be able to validate all personal details and evidence information on the evidence but must validate all information that can be validated with the issuing or authoritative sources.

The results of identity evidence information validation and evidence genuineness validation should be recorded in enrollment records or audit logs as appropriate for the CSP.
