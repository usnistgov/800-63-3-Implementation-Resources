---
layout: default
title:  IAL2-IAL3 Use Case
permalink: /63A/UseCase
navOrder: 4  
navTitle: Use Case  
---

Assuming that IAL2 is selected for a particular use, let us walk through the identity proofing steps for an application case wherein a provider offers services through a mobile device.

### Resolution

The agency proceeds to resolve all core attributes collected from the applicant into a single identity. In the case of paper/in-person applications some of the resolution steps may require human intervention.

In our IAL2 example, following the initial registration step shown in the following diagram, the agency can leverage identity document image verification software to obtain the full name, address and DOB for an applicant from the image of their driver’s license or passport that they received via the app. Once attribute information is produced from the document image, the agency has two or more sets of attributes for the applicant –one from the application entries provided by the applicant, and one or more from the document(s).

![Registration Workflow]({{site.baseurl}}/img/workflow-3-enrollment.png){:width="1000"}

The agency can then run a matching algorithm, as depicted in the following figure, to obtain a similarity score that reflects the extent to which the different sets of identity attributes resolve, and, comparing this against a threshold, decide success or failure.

![Resolution Workflow]({{site.baseurl}}/img/workflow-4-resolution.png){:width="1000"}

### Validation

To validate the identity the agency must examine the documents collected from the applicant. Automated software (or an operator) will first check the security features on the document that has been uploaded by the applicant using the mobile application –-holograms, secure inks and other devices-– to check that it is genuine. Second, the agency will also validate the personalized information on the card –-name, date of birth, address, driver’s license or passport number, account number-– and make sure that the information in the documents is valid. An example is illustrated in the following figure, where an automated system that uses the picture of the applicant’s passport to extract information and physical security features to validate the evidence in terms of both the features and the information.

![Validation Workflow]({{site.baseurl}}/img/workflow-5-validation.png){:width="1000"}

### Verification

The agency completes the identity proofing process by verification. In this step, the identity of the actual individual applying is verified for a match against the individual whose identity information is built using resolution and validation of the documents provided. A general outline for the verification process has been shown in the following figure. In our example, the agency uses the mobile application to perform face verification of the individual which compares a face image submitted by the applicant in the final stage of identity proofing against face images in the background records of the applicant’s driver’s license or passport. Please note that this would be equivalent to a physical check if the applicant’s picture taken by the mobile app is compared simply to the image on the identity document; strong or superior biometric verification would require the verification of the applicant’ face image against an image (or template thereof) retained in the background repository by the state department of motor vehicles or the Department of State. For enhanced security, the agency can in addition use the bank account information provided by the applicant to submit two micro deposits of less than $1 each, and then ask the applicant to complete the final verification step by providing the micro deposit amounts in cents, appended into a 4-digit sequence. Upon successful verification the agency will issue credentials to the applicant, who can subsequently start using the service.
