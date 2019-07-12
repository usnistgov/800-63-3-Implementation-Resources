---
layout: default
title:  Lifecycle Management
collection: 63B
permalink: /63B/Lifecycle
navOrder: 5  
navTitle: Lifecycle  
---

## Authenticator Lifecycle Management

See [SP 800-63 B](https://pages.nist.gov/800-63-3/sp800-63b.html#sec6) for normative requirements.

### Authenticator Binding

One of the changes in SP 800-63B from previous editions of SP 800-63 is the explicit recognition of bring-your-own authenticators. It is no longer assumed that CSPs will issue authenticators, which is important in the case of physical authenticators and with the increased use of two-factor authentication: it should not be necessary for a subscriber to carry, manage, and protect a "keyring" of devices for authentication on multiple services. While this issue is mitigated greatly by the use of federated authentication, many subscribers will nevertheless have accounts at multiple CSPs. The use of multiple authenticators at each CSP, prompted by more secure account recovery procedures, also increases the number of authenticators that must be managed.

SP 800-63B uses the term binding rather than issuance to better accommodate bring-your-own authenticators since the authenticator(s) being used may have been issued elsewhere. At the same time, bring-your-own authenticators introduce a new problem: the need for the CSP to determine the type and strength of authenticators it binds to the account. This is discussed above.

The binding refers to the association between the subscriber's account at the CSP (the credential) and the authenticators that can be used to access it. While binding multiple authenticators does increase the attack surface of the subscriber's account, availability of a reasonable number of authenticators minimizes the need for account recovery, which can be made more secure if it is a rare event. It also accommodates the different interfaces available on different devices.

Each authenticator has a metadata record associated with it, including information on the binding that was established and unsuccessful authentications attempted with it. The latter includes state information that is needed to implement rate limiting of a specific authenticator as described in [Section 5.2.2](https://pages.nist.gov/800-63-3/sp800-63b.html#throttle) without necessarily rate limiting the entire account.

#### Binding at Enrollment

Binding of one or more authenticators usually immediately follows an identity proofing transaction. It is important that the binding of authenticators be strongly associated with the identity proofing process to ensure that the subject associating an authenticator with a subscriber's credential is, in fact, that subscriber.

#### Post-Enrollment Binding

Post-enrollment binding includes the binding of additional authenticators for backup purposes as well as in response to the loss, theft, or damage to an existing authenticator. The latter situation, often referred to as "account recovery", has been the weak point of many authentication systems. All of the effort in strongly authenticating subscribers is moot if an attacker can successfully claim the loss of one or more authenticators and obtain the binding of new authenticators under their control. For this reason, binding of new authenticators requires either authentication with existing authenticators or a repeat of some or all of the identity proofing process.

##### Binding of an Additional Authenticator at Existing AAL

The most common binding situation is when a subscriber wants to bind an additional authenticator to their account. This may occur as a result of the loss, theft of, or damage to an existing authenticator. It might also be done to create an additional backup authenticator or one that is compatible with a different hardware device.

Associating a new authenticator to an account is a somewhat more sensitive transaction than a routine authentication, because a successful attack that is not detected might provide the attacker with ongoing access to the subscriber's account. However, authentication at a higher AAL is often not possible because of the limitations of authenticators that the subscriber already has. To address this concern, SP 800-63B recommends that a notification be sent to the subscriber when a new authenticator is bound to the account to increase the likelihood of detection of an unauthorized binding.

##### Adding an Additional Factor to a Single-Factor Account

A special case that happens at most once per subscriber account is the need to associate a second factor when one authentication factor is currently bound. Because the account has been only used with single-factor authentication, it is assumed that the subscriber has already accepted the risk associated with that use and that the binding of a new authentication factor doesn't represent an escalation of privilege (e.g., access to personal information that wasn't accessible before).

As noted in this section, it is possible for a subscriber to add an additional authentication factor if only one is currently bound. This is usually a physical authenticator being added to an account that currently only has a memorized secret authenticator. As above, the subscriber should be notified of this event.

##### Replacement of a Lost Authentication Factor

In a perfect world, subscribers would never lose authenticators, or would have another authenticator of the same factor(s) available as a backup. However, in practice subscribers lose or damage authenticators with some regularity. It is often possible to bind additional physical authenticators to mitigate loss of something you have, but it is considerably more difficult to recover from the common situation where a memorized secret has been forgotten. Having a secondary memorized secret as a backup is not a good response, since this secondary secret would be rarely used and more likely to be forgotten.

The most common and problematic situation is the loss of a memorized secret. A special provision is made for recovery in this case, involving the use of two physical authenticators and a recovery code that is sent by the CSP to the subscriber's address of record. The recovery code serves as both notice to the subscriber and protection against an attacker that is able to steal two or more of the subscriber's authenticators. While not fully two-factor, this procedure confirms the subscriber's ability to receive messages at the address of record.

#### Binding to a Subscriber-provided Authenticator

So-called "bring your own" authenticators, while desirable from a convenience and complexity point of view, introduce some new issues. As discussed above, the CSP needs some assurance as to the type and security of authenticators that are bound to the subscriber's account. The CSP should always make a default assumption of the weaker authenticator type (e.g., single-factor as opposed to multi-factor crypto device, or software-based as opposed to hardware-based authenticator) when it is not able to reliably establish the nature of the authenticator. 

#### Renewal

The authenticator renewal process should begin well before the actual expiration of a previous authenticator. Lifetimes of physical authenticators should be chosen to balance the risk of the undetected loss of an authenticator and the cost and complexity of reissuance.

Authenticator expiration should not be seen as conflicting with the earlier guideline that memorized secrets should not have routine expiration. Expiration of memorized secrets (without some other indication of a security breach having occurred) should be avoided because of the users to choose poor memorized secrets when they know they will need to replace them soon.

### Loss, Theft, Damage, and Unauthorized Duplication

The possibility of authenticator loss, theft, damage, and unauthorized duplication require that the CSP provide an effective means for reporting and requesting the suspension or revocation of an authenticator without creating a mechanism for denial-of-service attacks on the subscriber. Suspension gives the subscriber an opportunity to intervene before an authenticator is removed from the account entirely, thereby mitigating the severity of such denial-of-service attacks.

### Expiration

Expiration of authenticators is permitted but not required by SP 800-63B. As discussed above, the decision whether and at what period to expire authenticators should be made by the CSP based on a risk analysis process. Expiration of some authenticators (certificate-based cryptographic authenticators) is sometimes useful to limit the growth of certificate revocation lists (CRLs) since revoked authenticators can be removed from the list once they have expired.

As discussed above, routine expiration of memorized secrets is discouraged because of the tendency for subscribers to choose weaker secrets when they have to change them periodically.

### Revocation and Termination

Revocation and termination address situations when a subject ceases to be a subscriber of a given CSP. Procedures used by specific CSPs, such as in FIPS 201 with respect to PIV credentials, supplement the information in this section.

While the use of an authenticator by a specific CSP for online authentication is relatively easy to revoke, authenticators that contain user attributes or that can be used for physical authentication require much more emphasis on physical collection and destruction. Relying parties that use information contained on such authenticators need to consider the possibility that those attributes are stale, and should verify the attributes with the CSP online when this is practical, depending on the sensitivity of the application.

