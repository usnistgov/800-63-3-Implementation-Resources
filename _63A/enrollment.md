---
layout: default
title:  'SP 800-63A: Enrollment Codes'
permalink: /63A/enrollment/
navOrder: 6
navTitle: Enrollment
---

# Enrollment Codes

The use of an enrollment code for address confirmation is a requirement for IAL2 remote identity proofing and enrollment. Enrollment codes are not used for address confirmation for in-person identity proofing and enrollment but may be used for authenticator binding if one or more authenticators were not registered to the subscriber's account at the time of in-person identity proofing. This is discussed in more detail below. For either enrollment code use case – IAL2 remote identity proofing address confirmation or in-person proofing authenticator binding – enrollment codes must meet specified entropy requirements (4.6). Enrollment codes must be comprised of:

- a random six-character alphanumeric or equivalent entropy; or
- a machine-readable optical label, such as a QR Code, that contains data of similar or higher entropy as a random six character alphanumeric.

For IAL2 remote identity proofing address confirmation, the enrollment code may be sent to any address that was validated in the identity evidence validation step of identity proofing -- postal, email, or telephone/SMS addresses. Enrollment codes used for address confirmation have specified validity periods depending on the type of address where the enrollment code is sent:

- 10 days, when sent to a postal address of record within the contiguous United States;
- 30 days, when sent to a postal address of record outside the contiguous United States;
- 10 minutes, when sent to a telephone of record (SMS or voice);
- 24 hours, when sent to an email address of record;

The IAL2 remote identity proofing and enrollment process is not complete until the applicant provides confirmation of the enrollment code within the specified validity period – through confirmation of the enrollment code or scanning and confirmation of the optical label/QR code.

Enrollment codes may also be used for in-person proofing and enrollment processes if an authenticator(s) is not registered to the subscribers' account at the time of in-person identity proofing and, therefore, the authenticator binding would need to occur at a later time. Enrollment codes may be used for authenticator binding to subscribers' accounts in such circumstances. Enrollment codes used for this purpose must meet the entropy requirements presented above and have a maximum validity period of 7 days. It is intended that enrollment codes used for this purpose would be provided to the applicant during the in-person proofing session and would not be mailed to the validated address of record.
