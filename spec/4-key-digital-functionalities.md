---
description: >-
  Key Digital Functionalities describe the core (required) functions that this
  Building Block must be able to perform.
---

# 4 Key Digital Functionalities

To facilitate the eSignature service as described in section 2, the Building Block must have specific Key Digital Functionalities.&#x20;

## 4.1 HSM

The Hardware Security Module (HSM) is an integral part of the eSignature Building Block. The HSM ensures the protection of a key with utmost safety. Without an HSM the key can potentially fall into the wrong hands and could result in huge mistrust. All keys used in our one-time signatures are created, used, and destroyed within the HSM. The HSM should be configured with FIPS 140-2 Level 3.&#x20;

## 4.2 SCD

The eSignature creation device (SCD) is the component where the user's private key would be stored. The SCD could be a Smart card, Mobile App, Sim card App, or equivalent. The SCD interacts with the eSignature Building Block using its own internal protocol. Every eSignature Building Block will support one or many such SCDs. Most of the SCD would be protected with a secure PIN/Biometrics.

The SCD should be qualified with at least one of the following FIPS 140-2/3 Level 3 or Annex II of [Regulation (EU) No 910/2014 (eIDAS)](https://en.wikipedia.org/wiki/EIDAS) or equivalent common criteria certification.

## 4.3 Timestamp

The time of a sign is an important part of the signature. Without a proper time of the signature, we can never trust the signature, as one can not find if the signature happened before its expiry or after expiry. Most often this functionality is provided by the timestamping server hosted by the CA.

## 4.4 One-Time Signing Service

This is one of the key functionality of eSignature. This service is responsible to provide the One Time Signature API and interact with the Hardware Security Module (HSM). This service validates the user against the Authorization Building Block.  A valid user is allowed to create a key in HSM and sign it.  Every key created here will also need an X509 certificate. The certificate management module will publish this created X509 certificate. &#x20;

Keys created during One Time Signature should be deleted as soon as the signature process is over. Logs SHOULD be kept in a database of the details of the deletion. Logs MUST include timestamps and identify the user and affiliation that performed the transaction.

## 4.5 SCD On-Boarding

eSignature creation device (SCD) On-Boarding is the module responsible for binding the SCD and user. The module interacts with the Identity Building Block and would validate the user's presence before issuing the Certificate. This module is responsible for talking to the SCD for all types of key management and administrative needs. This module is hosted on a server and would ensure the keeping of clear audit records and Know Your Customer/Client (KYC) records.

## 4.6 SCD Signing

The SCD Signing is one of the vital functions of eSignature Building Block. When a user holds its key in an SCD then this module is responsible for interacting with the SCD to sign any required document. This module works in asynchronous mode. A signature is requested on demand using the API. However, the module interacts with the SCD asynchronously.  The module is responsible for connecting to SCD for all signing purposes.&#x20;

## 4.7 Certificate Management

All certificates that are created within the  SCD  will be hosted in this module. The modules let everyone have their X509 public certificate hosted for any verification. The module should have an administrative ability to allow people to revoke the keys on demand. The module has to maintain the OCSP & CRL-based revocations.  Key revocation is not available in Onetime Signatures as the certificate is short-lived.

## 4.8 Notification&#x20;

This module is responsible for notifying the SCD device when a signature is needed. This helps the SCD to alert the user. The user can look through the notification and accept to sign the document. The module is also responsible for notification of a signature to the user's mobile phone/email/SCD. The notification to the user can be used as an audit record by the user. The notification Building Block can be used to send notifications to the end user.

## 4.9 **Messaging Interface**

The interface handles protocols to interact with the Messaging Building Block for sending notifications to the user. This interface abstracts the messaging with an omnichannel interface and lets the user handle its preferred communication channel. &#x20;

## **4.10 Information Mediator Interface**&#x20;

This interface handles protocols to interact with the Information Mediator Building Block in order to securely expose Private API services to other Building Blocks and also enables the eSignature Building Block to access services of other Building Blocks and applications through the Information Mediator Building Block.

## 4.11 Observation interface

This interface handles the necessary health, metrics, logging, traceability, and circuit breakers for the given Building Block.  While there are no certain standards to this, it is recommended to follow the [OpenTelemetry](https://opentelemetry.io/) design to address the challenges.



