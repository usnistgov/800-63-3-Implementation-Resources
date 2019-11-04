---	
layout: default	
title:  Assurance Levels  
permalink: /63-3/assurance	
navOrder: 2  
navTitle: Assurance  
---		
## Assurance Levels

One of the major changes between SP 800-63-3 and earlier editions is the change from a single Level of Assurance (LOA) to three individual assurance levels:

* Identity Assurance Level (IAL), defined in SP 800-63A
* Authentication Assurance Level (AAL), defined in SP 800-63B
* Federation Assurance Level (FAL), defined in SP 800-63C

SP 800-63-3 provides the basis for selection of the individual assurance levels (xAL), while the requirements for meeting those assurance levels is found in the referenced volume.

The primary reason for moving from the single-dimensional LOA to individual xALs is to support use cases where the risks associated with identification, authentication, and federation are unequal. One example of this is services that are pseudonymous in nature, for example crisis hotlines. Strong authentication might be required to ensure that the same person is associated with multiple online sessions, but it may be unnecessary or even undesirable to establish the real-world identity of that person.

The detailed guidelines for selection of IAL, AAL, and FAL are given in [SP 800-63-3 Section 6](https://pages.nist.gov/800-63-3/sp800-63-3.html#CYOA). These guidelines are based on an enumeration of risk categories (financial loss or agency liability, personal safety, etc.) originally given in the now-obsolete OMB Memorandum M-04-04.

The guidelines are remarkably similar, but one shouldn't conclude that IAL, AAL, and FAL are necessarily the same. The risk associated with identification (identity proofing), authentication, and federation errors might be different from each other. Therefore, the selection of IAL, AAL, and FAL must be done with the corresponding risk profiles. It may be tempting to use the highest assurance levels available out of an abundance of caution. However, it should be noted that there are significant costs to both the organization and individual users associated with over-proofing, over-authentication, and use of unnecessarily secure federation protocols.
