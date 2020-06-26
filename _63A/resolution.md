---
layout: default
title:  'SP 800-63A: Identity Resolution and Evidence Collection'
permalink: /63A/resolution/
navOrder: 3
navTitle: Resolution
---

# A.3 Identity Resolution and Evidence Collection {#s-a-3}

The identity resolution step in identity proofing processes and the collection of core identity attributes are parallel processes to establish a unique representation of the individual's identity for use during the proofing process and enrollment. The objective of the collection of core identity attributes is to resolve applicants' identity to a single unique entity for the given population and context. The types of identity attributes that may be retrieved from identity documents and used for identity resolution typically include, but are not limited to:

- name (first, last, middle) with combinations and variations,
- address (number, street, state, zip code) with combinations and variations,
- birth date (day, month, year) with combinations and variations,
- email address,
- Phone number.

Depending on the types of identity evidence that applicants can provide, there are many other types of identity attributes and information that may be collected and considered for identity resolution (e.g., place of employment, voting district, association membership, etc.). In general, self-asserted attributes not supported by identity evidence are not usable for purposes of identity proofing assurance higher than AAL1.

It is important to note that SP 800-63A limits the attribute information that may be collected and maintained: _Collection of PII SHALL be limited to the minimum necessary to resolve to a unique identity in a given_ _context and_ _to validate the existence of the claimed identity and associate the claimed identity with the applicant providing identity evidence for appropriate identity resolution, validation, and verification__._ _This MAY include the collection of attributes that assist in data queries._ (4.4.1.1, 4.2 #2) The goal of identity resolution is to uniquely distinguish an individual within a given population or context. Effective identity resolution uses the minimum set of attributes necessary to resolve to a unique individual. In addition, SP 800-63A requires that applicants are provided a notice of identity proofing at the time of evidence collection. Such notice should include, but is not limited to:

- the types of personal information necessary for collection to be collected
- whether such information is mandatory or voluntary,
- purposes for the collection and maintenance of personal information and attributes,
- whether the information will be retained and how it will be protected, and
- consequences of failure to provide required information.

There may be conflicts among attribute information collected for a given applicant that require resolution. The CSP may seek to resolve such conflicts though the collection of additional information, evidence and sources. Knowledge-based verification may be used for resolving information conflicts for purposes of identity resolution.

Identity evidence comprises physical or digital artifacts that identity system applicants can provide to prove the real-world existence of a claimed identity. Acceptable identity evidence is that which can be traced to issuing sources (e.g., state motor vehicle departments, state/federal government agencies, law enforcement agencies, utility company, financial institution).

## A.3.1 Collection Techniques {#s-a-3-1}

CSPs may use multiple techniques for collecting attributes and evidence in different media. These techniques pertain to digital or other methods of collection that result in the transmission of information from the applicant to the agency. Multiple techniques may be combined based on the CSP's requirements, applicant capabilities, and the overall approved identity proofing process flow. SP 800-63A does not specify whether all collection and identity proofing processes occur in a single session or in multiple sessions. The CSP should determine and document the information and collection and identity proofing processes, such information should be included in the notice of proofing described above.

Submitting evidence and attributes in multiple stages can become burdensome for an applicant. It is important to consider collecting the appropriate evidence up-front to avoid requiring the user to perform multiple interactions in order to establish an account. There should be a good balance between executing the proofing process and minimizing the burden on the applicant.

Applicants for in-person proofing should receive the notice of proofing described above prior to the in-person session so that they can be prepared for the session and be able to provide required information and identity evidence during the session. The processes below for collection of digital identity information and evidence are applicable to remote identity proofing processes but may also be used for in-person identity proofing processes for the submission of identity information and evidence prior to the in-person session.

### A.3.1.1 Digital {#s-a-3-1-1}

Initial application information may be captured via an online form directly from the applicant that is being proofed. In other cases, the agency may allow the applicant to provide some documents via remote means, such as submitting an image of an identification document like a passport or a driver's license. This workflow requires the utilization of some form of digital capture, such as a camera or a document scanner. Systems with optical character recognition capabilities that allow fields in a document to be pre-populated upon scanning should also allow the applicant to review and validate the information as correct. Some CSPs may choose to enforce requirements more directly by providing mobile applications for collection –e.g. camera capture functions that provide an overlay and illumination check feature to ensure applicants provide pictures with correct size and brightness.

Common methods which a CSP can use to digitally capture evidence are presented below.

[Table A-3-1. Digital Collection Methods](resolution.md#table-A-3-1){:name="table-A-3-1"}
{:latex-ignore="true"}

| Method | Device | Information |
| --- | --- | --- |
| Document Image Capture | Camera | This can be used to capture an applicant's photo or the image of an evidence such as a driver's license. Agencies can consider pictures at 300 dpi or above to be of sufficient resolution. |
| Document Image Capture | Scanner | This can capture a document, which is compared against a known template by automated software to extract information. For optical character recognition, scans at high than 300 dpi are typically considered to be of sufficient quality. |
| Barcode | Scanner | Commercial off-the-shelf scanners can capture and extract information from standardized barcodes embedded on identity evidence. |
{:latex-columns="p@0.28\textwidth,p@0.20\textwidth,p@0.43\textwidth" latex-table="A-3-1" latex-caption="Digital Collection Methods"}

### A.3.1.2 In Person {#s-a-3-1-2}

If an agency allows in-person registration, it may consider, for efficiency and convenience purposes, executing additional steps in the process, such as evidence validation, at the time of registration. The agency may provide kiosks to allow applicants to enter their information directly. Alternatively, applicants may meet with a representative of the agency to allow them to enter the applicant's information on their behalf. Note that when this is done it is important the process is conducted in a manner that allows the individual to verify their information has been accurately captured and input into the collection system. Training should be provided for all agency representatives to ensure that they are aware of organizational and federal policy concerning privacy and user experience.

### A.3.1.3 Paper Form {#s-a-3-1-3}

In the event an applicant does not have access to a connected device, is unable to use a computer, or otherwise wishes to submit the biographic information via a non-digital medium, the agency may offer the option to complete a paper form instead. Written entry of information should be avoided if it is possible to capture information via multiple choice selections and the applicant should be instructed to print clearly to reduce inaccuracies resulting from the interpretation of handwriting. Some organizations require enrollment via paper form only in person while some implementations may allow the applicant to complete the form remotely and mail it in. It is also important to note that in many use cases applicants are asked to fill out a paper form with sensitive personal information and mail it to the requesting organization. Precautions should be taken to minimize that risk and maintain transparency by informing the individual of the risks while the paper form is in transit. It should be noted that this method of attribute collection for identity resolution represents self-asserted information which is acceptable for IAL1 only. IAL2 and IAL3 require identity evidence submission, validation and verification.

## A.3.2 Strength of Evidence {#s-a-3-2}

SP 800-63A specifies (4.4.1.2, 4.5.2) the amount and strength of identity evidence that must be presented to meet IAL2 and IAL3 assurance levels as shown here.

IAL1
:  - No identity evidence is collected.

IAL2
:   - One piece of SUPERIOR or STRONG evidence depending on strength of original proof and validation occurs with the issuing source, or
    - Two pieces of STRONG evidence, or
    - One piece of STRONG evidence plus two (2) pieces of FAIR evidence

IAL3
:   - Two pieces of SUPERIOR evidence, or
    - One piece of SUPERIOR evidence and one piece of STRONG evidence depending on strength of original proof and validation occurs with the issuing source, or
    - Two pieces of STRONG evidence plus one piece of FAIR evidence

SP 800-63A also specifies (5.2.1) the characteristics of identity evidence in order to meet the following strength and quality classifications: UNACCEPTABLE, WEAK, FAIR, STRONG, and SUPERIOR. As indicated, one piece of STRONG evidence may be used to meet IAL2 requirements and one piece of SUPERIOR evidence and one piece of STRONG evidence may be used to meet IAL3 requirements depending on the strength of the original proof for the STRONG evidence and validation of the evidence occurs with the issuing source. The text _depending on the strength of the original proof_ refers to the identity proofing process that was used in order to issue that type of STRONG evidence. If the identity proofing process for issuance of the STRONG evidence confirmed the claimed identity by collecting two of more forms of SUPERIOR or STRONG evidence, then the STRONG evidence can be considered to meet the first part of the requirement for consideration as STRONG+[^strongplus] to meet the IAL2 and IAL3 requirements. State-issued REAL ID driver's licenses represent an example of this type of identity proofing requirements that may be considered to meet this condition. The text for the second condition for consideration as STRONG+ evidence is that _validation occurs with the issuing source_. This refers to the required validation of identity evidence (5.2.2) and STRONG evidence can be considered to meet this requirement if the evidence is validated with the issuing source. For the example above, state-issued REAL ID driver's licenses can be considered to meet this condition for consideration as STRONG+ evidence if the CSP validates information from the driver's license with the respective State Department of Motor Vehicles or the DMV databases maintained by the American Association of Motor Vehicle Administrators (AAMVA).

### A.3.2.1 Notional Strength of Evidence {#s-a-3-2-1}

SP 800-63A (5.2.1) is directed to CSPs to specify the strength of evidence that may be collected based on evidence quality characteristics. Such determinations are dependent upon the jurisdiction, population served, identity proofing policies, procedures, and controls applied, and the specific quality characteristics for the types of identity evidence that the CSP may collect. The following table presents notional strength based on the quality characteristics for common types of evidence that may be presented by applicants for identity proofing. It is noted that this classification is notional based on the general quality characteristics for the listed evidence types.

[Table A-3-2. Notional Strength of Evidence](resolution.md#table-A-3-2){:name="table-A-3-2"}
{:latex-ignore="true"}

| Type of Evidence | Strength | Notes |
| --- | --- | --- |
| US Passport | SUPERIOR | Includes US Passport cards |
| Foreign e-Passport | SUPERIOR | |
| Personal Identity Verification (PIV) card | SUPERIOR | |
| Common Access card (CAC) | SUPERIOR | |
| Personal Identity Verification Interoperable (PIV-I) card | SUPERIOR | |
| Transportation Worker Identification Credential (TWIC) | SUPERIOR | |
| Permanent Resident Card | SUPERIOR | Issued on or after May 11, 2010 |
| Native American Enhanced Tribal Card | SUPERIOR | |
| REAL ID cards | STRONG+ | Includes REAL ID driver's licenses and ID cards. REAL ID cards have a star printed in the upper right-hand corner. Card and personal information must be validated with appropriate DMV or AAMVA. |
| Enhanced ID cards | STRONG+ | Includes Enhanced ID driver's licenses and ID cards. Must be validated with appropriate DMV or AAMVA. |
| U.S. Uniformed Services Privilege and Identification Card (U.S. Military ID) | STRONG+ | Includes Uniformed Services Dependent ID Cards. Must be validated with appropriate military issuing source. |
| Permanent Resident Card | STRONG | Issued Prior to May 11, 2010 |
| Native American Tribal Photo Identification Card | STRONG | |
| Driver's License or ID card (REAL ID non-compliant) | STRONG | |
| School ID card | FAIR | Includes facial image photograph |
| Utility account statement | FAIR | |
| Credit/debit card and account statement | FAIR | |
| Financial institution account statement | FAIR | |
| US Social Security Card | WEAK | |
| Original or certified copy of a birth certificate issued by a state, county, municipal authority or outlying possession of the United States bearing an official seal | WEAK | |
{:latex-columns="p@0.32\textwidth,p@0.16\textwidth,p@0.43\textwidth" latex-longtable="true"}

[^strongplus]: The classification STRONG+ denotes evidence that may be considered to meet the evidence strength requirement for the IAL2 requirement for one piece of STRONG evidence and the IAL3 evidence strength requirement for one piece of SUPERIOR evidence and one piece of STRONG evidence, provided that the STRONG evidence must be validated with the issuing sources listed in order to meet this evidence strength classification.
