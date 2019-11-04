---	
layout: default	
title:  Identity Risk Assessments  
permalink: /63-3/risk	
navOrder: 1  
navTitle: Risk  
---		
## Identity Risk Assessments

Risk assessments are formalized processes that aid agencies in identifying, estimating, and prioritizing information security and privacy risks by considering the threat and vulnerability landscape, and focusing on the potential harm of an adverse event and the likelihood such an event will occur. 

These assessments are important because:
- they reduce uncertainty; 
- they are proactive measures rather than reactive measures; 
- they allow for quicker, more efficient responses to adverse circumstances or events; 
- they increase organizational awareness of potential threats and vulnerabilities; 
- they could lead to cost savings in the event of an adverse circumstance or event; 
- they help safeguard PII, protecting customer privacy; and 
- they instill more confidence in an agency and its customers.  

To mitigate digital identity risks, [OMB M-19-17](https://www.whitehouse.gov/wp-content/uploads/2019/05/M-19-17.pdf) (Section IV, Governance item 4) requires federal government agencies to incorporate risk assessment processes consistent with SP 800-63-3 into their digital identity service offerings. Agencies may approach the risk assessment process in a way that best suits their mission and needs. The following methodology may prove beneficial to agencies seeking guidance on the risk assessment process: 

![Risk Assessment Process Flow]({{site.baseurl}}/img/RiskAssessmentProcessFlow.png)

### Digital Identity Risk Acceptance Statement Template

Agencies providing digital identity services shall codify their risk decisions in a Digital Identity Acceptance Statement, in accordance with NIST SP 800-63-3 and NIST SP 800-53 IA-1(a)(2)[1]. The former SP details how to manage identity and authentication risks via identity-related controls, but references the latter SP as needed for security controls.
In accordance with SP 800-63-3, a Digital Identity Acceptance Statement shall include, at a minimum, the following information: 
1.	Assessed Assurance Level(s),
2.	Implemented Assurance Level(s),
3.	Rationale, if implemented Assurance Level(s) differs from assessed Assurance Level(s),
4.	Comparability demonstration of compensating controls when the complete set of applicable 800-63 requirements are not implemented, and
5.	If not accepting federated identities, rationale.


Additional information included in the statement is up to individual agency discretion. 

A Digital Identity Risk Acceptance Statement template is provided for agency use. The use of this template is not required, but is intended to provide agencies with a better idea of what the statement could look like. Agencies may wish to include additional information that is not present in this template, or less information, but the required information outlined above must be included in the final statement. 

<a href="../img/Risk_Acceptance_Statement_Template_DRAFT.docx"> <button>Download the Digital Identity Risk Acceptance Statement Template</button> </a>

### Digital Identity Risk Management and the Risk Management Framework

References to digital identity risk management in NIST SP 800-63-3 do not establish additional risk management processes for agencies, but rather, supplement the NIST Risk Management Framework (RMF) and its component special publications. SP 800-63-3 requirements provide specific guidance related to digital identity risk that must be applied through the execution of RMF life cycle phases.

The RMF, a risk-based approach to security control selection, provides a process that integrates security and risk management activities into the system development life cycle. Although the RMF is designed to look at organizational risk on a broad scale, it can be applied at a smaller scale to digital identity risk management.

Agencies can apply the concepts of identity risk management and the guidelines outlined in NIST SP 800-63-3 around risk assessment frameworks to the steps outlined in the RMF when developing, implementing, and maintaining their identity risk management programs. The digital identity risk assessment can be considered Step 0 of the RMF process, as it is a precursor to selecting, implementing, assessing, and monitoring controls. The methodology then follows a similar process pattern as the RMF, with each step in the identity risk assessment process correlating to a step in the framework. For example, agencies _identify_ potential risks, _categorize_ them by impact level, _select_ assurance levels, and _implement_ risk treatment decisions.

The following table outlines the six RMF steps to managing organizational risk and the relevant corresponding identity risk management activities associated with each step:

**Table: Risk Management Life Cycle and Activities**

| **Step** | **Description** | **Corresponding Identity Risk Management Activities** |
| --- | --- | --- |
| **Step 0: Conduct Risk Assessment** |	Conduct a risk assessment to determine the extent to which risk must be mitigated by the identity proofing, authentication, and federation processes. |	Conduct a risk assessment to determine the extent to which risk must be mitigated by the identity proofing, authentication, and federation processes. |
| **Step 1: Categorize System** |	Categorize the system and the information processed, stored, and transmitted by that system based on an impact analysis. |	Identify appropriate identity assurance level(s) based on risk assessment and other analysis. |
| **Step 2: Select Controls** |	Select an initial set of baseline security controls for the system based on the security categorization; tailoring and supplementing the security control baseline as needed based on agency assessment of risk and local conditions.	 |	Select identity proofing process and technologies. Select authenticators and authentication controls. Select federation protocols and controls. |
| **Step 3: Implement Controls** | Implement the security controls and document how the controls are deployed within the system and environment of operation.  |	Implement select controls and authenticators. |
| **Step 4: Assess Controls** |	Assess the security controls using appropriate procedures to determine the extent to which the controls are implemented correctly, operating as intended, and producing the desired outcome with respect to meeting the security requirements for the system. |	Assess selected controls. |
| **Step 5: Authorize System** |Authorize system operation based upon a determination of the risk to organizational operations and assets, individuals, other organizations, and the Nation resulting from the operation of the system and the decision that this risk is acceptable. |	Codify identity risk management decisions in a Digital Identity Acceptance Statement and other documentation. |
| **Step 6: Monitor Controls** | Monitor and assess selected security controls in the system on an ongoing basis including assessing security control effectiveness, documenting changes to the system or environment of operation, conducting security impact analyses of the associated changes, and reporting the security state of the system to appropriate agency officials. |	Monitor and assess selected controls on an ongoing basis and make updates as necessary. |
