---
description: This section lists the technical capabilities of this Building Block.
---

# 6 Functional Requirements

The eSignature Building Block has several functional layers within it. Some functional layers follow the existing set of protocols and custom protocols, While the other functional requirements are defined within this specification. In this section, we will provide a clear indication to state what blocks follow what kind of protocols.

## 6.1 Hardware Security Module

* In the case of the One-Time Signature, a Hardware Security Module (HSM) must be used to create cryptographic keys. (REQUIRED)
* It must be used to sign a certificate. (REQUIRED)
* Keys shall not be exported. (REQUIRED)
* MUST be protected well with best security practices. (REQUIRED)

## 6.2 Signature Creation/Seal Device

* Signature Creation Device (SCD) should have secure storage to protect private keys. (REQUIRED)
* SCD may have proprietary APIs with the eSignature Building Block. (REQUIRED)
* SCD is assumed to be with the user. (REQUIRED)
* A user's PIN is a must for the SCD. (REQUIRED)
* Keys shall not be exportable. (REQUIRED)

## 6.3 Timestamp&#x20;

* For a valid signature, a timestamp server is a must. (REQUIRED)
* The timestamp server shall follow [RFC3161](https://www.ietf.org/rfc/rfc3161.txt). (REQUIRED)

## 6.4 Certifying Authority

* eSignature Building Block may be a certifying authority. (REQUIRED)
* If not, the Building Block shall have access to a certifying authority and be able to issue certificates or be a subordinate certification authority. (REQUIRED)

## 6.5 eSignature Service&#x20;

* Service shall support the onboarding of the Signature Creation Device (SCD). (REQUIRED)
* Service shall support both the key functionalities of signing using SCD and One-Time Signature. (REQUIRED)
* The user shall be authenticated through the ID Building Block for the One-Time Signature. (REQUIRED)
* The user shall be allowed to perform a signature through a pseudonym without user login. (REQUIRED)
* Optionally can support payments through a payment gateway. (OPTIONAL)
* Shall support all the listed signature types. (REQUIRED)
* Shall support redirection and callback as per the specification. (REQUIRED)

## 6.6 Audit&#x20;

* All user activities should be available for audit. (REQUIRED)
* May have the feature to tamper-proof the audit records. (REQUIRED)
* Auditors shall have the ability to get audit-proof of a transaction. (REQUIRED)

## 6.7 Certificate Management&#x20;

* Shall provide the ability to list and revoke a certificate. (REQUIRED)
* The user shall have the ability to revoke their keys (API-based or through customer care). (REQUIRED)
* Certificates shall have any of the following statuses (REQUIRED):
  * Active – The certificate is active and can be used for signing.
  * Expired – certificates are expired and should be renewed.
  * Suspended – certificate is suspended. The reason for suspension shall be provided together with status information.
  * Revoked – certificate is revoked. The reason for revoking shall be provided together with status information.
* Users shall be able to view their certificates and corresponding statuses. (REQUIRED)

## 6.8 Notification

* Shall provide the ability to notify the user over email, SMS, app notification, or any other equivalent. (REQUIRED)
* The user shall be notified of failed and successful transactions. (REQUIRED)

## 6.9 Messaging Interface

* The Messaging interface should send relevant information to the logging sub-block to maintain the history of all messages sent from this Building Block, which are useful for audit purposes. (RECOMMENDED)
* The messaging interface should provide the necessary protocol, data format, and information and interface to interact with the Messaging Building Block for sending notifications to a specific target Signature Creation Device or user through a variety of channels (SMS/email/etc.) (RECOMMENDED)



**Note:** The keywords "must", "must not", "required", "shall", "shall not", "should", "should not", "recommended", "may", and "optional" in this document are to be interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119)





## 6.11 Metrics&#x20;
