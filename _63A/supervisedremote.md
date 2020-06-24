---
layout: default
title:  'SP 800-63A: Supervised Remote Identity Proofing'
permalink: /63A/srip/
navOrder: 8
navTitle: SRIP
---

# Supervised Remote Identity Proofing

SP 800-63A section 5.3.3.2 provides for supervised remote identity proofing. Supervised remote identity proofing is intended to provide controls for comparable levels of confidence and security to the in-person identity proofing process for identity proofing processes that are performed remotely. Supervised remote identity proofing is optional for CSPs; that is, if a CSP chooses to use supervised remote identity proofing, then the requirements of section 5.3.3.2 would apply. It should be noted that the term "supervised remote identity proofing" has specialized meaning in SP 800-63A and is used only to refer to the specialized equipment and controls required in section 5.3.3.2.

Supervised remote identity proofing involves the use of a CSP-controlled station at a remote location that is connected to a trained operator at a central location. The goal of this arrangement is to permit identity proofing of individuals in remote locations where it is not practical for them to travel to the CSP for in-person identity proofing. Supervised remote identity proofing may also be used for achieving comparability with in-person requirements when face-to-face (i.e., in-person) encounters may present health risks to the applicant, CSP personnel or both. This may be necessary due to circumstances such as the COVID-19 pandemic where face-to-face encounters may present health risks. In these circumstances, supervised remote identity proofing may be used in a common facility where the applicant and CSP are in different locations in the facility but not actually interacting face-to-face. In such circumstances supervised remote identity proofing processing may be used.

Supervised remote identity proofing processes take advantage of improvements in sensor technology (cameras and biometric sensors) and communications bandwidth to closely duplicate the security of in-person identity proofing, which has been the requirement for high-assurance identity proofing in the past. This can be done through the use of a remote identity proofing station (or kiosk) which is under the control of the CSP or a third party that is trusted by the CSP to maintain its integrity.

The integrity of supervised remote identity proofing depends upon the applicant being continuously present and observed by the CSP operator during the entire session. An applicant who steps away from an in-process session may do so to alter their biometric source or substitute a different person to complete the identity proofing process.

The camera(s) a CSP employs to monitor the actions taken by a remote applicant during the identity proofing session should be positioned in such a way that the upper body, hands, and face of the applicant are visible at all times. Additionally, the components of the remote identity proofing station (including such things as keyboard, fingerprint capture device, signature pad, and scanner, as applicable) should be arranged such that all interactions with these devices is within the field of view. This may require more than one camera to view both the applicant and the room itself.

Technologies exist that allow for the digital validation of identity evidence via electronic means (such as RFID to read the data directly from e-passports and chip readers for smartcards). The scanners and sensors employed to access these features should be integrated into the remote identity proofing stations in order to reduce the likelihood of being tampered with, removed, or replaced. To be integrated means the devices themselves are a component of the workstation (i.e., smartcard readers or fingerprint sensors built into a laptop) or the devices, and their connections, are secured in a protective case or locked box.

For example, a kiosk located in a restricted area or one where it is monitored by a trusted individual requires less tamper detection than one that is located in a semi-public area such as a shopping mall concourse. (5.3.3.2 #6)

Requirements for protection and integrity of the kiosk depend on the specific kiosk capabilities (e.g., anti-tamper features). In most (perhaps all) cases, the kiosk will be overseen by a human attendant that can supplement the security features and protect the integrity of the kiosk. Between the attendant and the kiosk, the forms of protection provided may include (but are not limited to):

- Ensuring that only a single individual (applicant) interacts with the kiosk during any identity proofing session;
- Ensuring that the physical integrity of the kiosk and its sensors is maintained at all times;
- Verifying that the applicant is not using any devices to spoof biometric sensors (finger covers, for example); and
- Reporting any problems with the kiosk to the CSP

Supervised remote identity proofing stations/kiosks are required to employ mutual authentication where both the station/kiosk and server authenticate to each other. This is most often accomplished through the use of mutual TLS. Upon successful mutual authentication, an encrypted communication channel is established between the workstation/kiosk and the server which protects the data exchanged between them.
