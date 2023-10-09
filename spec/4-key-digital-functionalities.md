---
description: >-
  Key Digital Functionalities describe the core (required) functions that this
  Building Block must be able to perform.
---

# 4 Key Digital Functionalities

To facilitate the eSignature service as described in section 2, the Building Block must have specific Key Digital Functionalities.&#x20;

## 4.1 Hardware Security Module

The Hardware Security Module (HSM) is an integral part of the eSignature Building Block. The HSM ensures the protection of a key with utmost safety. Without an HSM the key can potentially fall into the wrong hands and could result in huge mistrust. All keys used in our one-time signatures are created, used, and destroyed within the HSM. The HSM should be configured with FIPS 140-2 Level 3. This device will follow PKCS11 or JCE standards.

## 4.2 Signature Creation/Seal Device

The eSignature creation device (SCD) is the component where the user's private key would be stored. The SCD could be a Smart card, Mobile App, Sim card App, or equivalent. The SCD interacts with the eSignature Building Block using its own internal protocol. Every eSignature Building Block will support one or many such SCDs. Most of the SCD would be protected with a secure PIN/Biometrics.

The SCD should be qualified with at least one of the following FIPS 140-2/3 Level 3 or Annex II of [Regulation (EU) No 910/2014 (eIDAS)](https://en.wikipedia.org/wiki/EIDAS) or equivalent common criteria certification.

## 4.3 Timestamp

The time of a sign is an important part of the signature. Without a proper time of the signature, we can never trust the signature, as one can not find if the signature happened before its expiry or after expiry. Most often this functionality is provided by the timestamping server hosted by the CA. This service follows [RFC 3161](https://datatracker.ietf.org/doc/html/rfc3161)

## 4.4 One-Time Signing Service

This is one of the most important functionality of eSignature. This service is responsible for providing the One Time Signature API and interacts with the Hardware Security Module (HSM). This service validates the user against the Authorization Building Block.  A valid user is allowed to create a key in HSM and sign it.  Every key created here will also need an X509 certificate. The certificate management module will publish this created X509 certificate. &#x20;

Keys created during One Time Signature should be deleted after the signature process. Logs SHOULD be kept in a database of the details of the deletion. Logs MUST include timestamps and identify the user and affiliation that performed the transaction.

## 4.5 Signature Creation Device On-Boarding

eSignature creation device (SCD) On-Boarding is the module responsible for binding the SCD and user. The module interacts with the Identity Building Block and will validate the user's presence before issuing the Certificate. This module is responsible for talking to the SCD for all types of key management and administrative needs. This module is hosted on a server and would ensure the keeping of clear audit records and Know Your Customer/Client (KYC) records.

## 4.6 Signature Creation Device Signing

The SCD Signing is one of the vital functions of the eSignature Building Block. When a user holds its key in an SCD then this module is responsible for interacting with the SCD to sign any required document. This module works in asynchronous mode. A signature is requested on demand using the API. However, the module interacts with the SCD asynchronously.  The module is responsible for connecting to SCD for all signing purposes.&#x20;

## 4.7 Certificate Management

All certificates that are created within the  SCD  will be hosted in this module. The module lets everyone have their X509 public certificate hosted for any verification. The module should have an administrative ability to allow people to revoke the keys on demand. The module has to maintain the OCSP & CRL-based revocations.  Key revocation is not available in Onetime Signatures as the certificate is short-lived.

## 4.8 Notification&#x20;

This module is responsible for notifying the SCD device when a signature is needed. This helps the SCD to alert the user. The user can look through the notification and accept to sign the document. The module is also responsible for notification of a signature to the user's mobile phone/email/SCD. The notification to the user can be used as an audit record by the user. This interface abstracts the messaging with an omnichannel interface. The notification Building Block can be used to send notifications to the end user/device. &#x20;

## 4.9 Public Observation Interface

This interface handles the necessary health, metrics, traceability and legal needs for the given Building Block.  While there are no certain standards to this, it is recommended to follow the [OpenTelemetry](https://opentelemetry.io/) design to address some of the challenges. Issuance of signature certificates is usually backed by several legal regulations. The requirements can range from KYC details available upon Judicial intervention, Revocation and Transparency of the revoked certificate as per OCSP/CRL (Similar to [RFC 6961](https://datatracker.ietf.org/doc/html/rfc6961)/[RFC 5280](https://www.rfc-editor.org/rfc/rfc5280)) and Dispute Resolution.&#x20;

## 4.10 Signature Backend

Once the signature is completed the signature backend keeps the signature until the eService server makes a request. Once the eService has received the Signature Token (SignatureId), It can request the eSignature BB to send the final signature. Once the Signature Token is validated the BB sends the signature. This happens over a backend-protected channel.&#x20;

## 4.11 eService Callback

This is the callback service available in eService. Once the signature is complete the user will be redirected to the eService. This module is responsible for understanding the redirect request and the HTTP parameters that are passed during this redirection.&#x20;

## 4.12 Signature Validation

This module is responsible for validating a digital signature. This is provided as a library. A format-specific validation library should be provided. The majority of the format adopted in this specification provides a clear explanation of how to validate the signature.  But in a few specified formats like ASC, it may be necessary for the signature service to explicitly state the validation mechanism. It is also expected that the service provider will provide a library, application (optional), and online service(optional)  to validate the signature.



