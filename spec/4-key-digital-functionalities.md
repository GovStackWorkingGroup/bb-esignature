# 4 Key Digital Functionalities

To facilitate eSignature service as described in section 2, the  building block MUST have specific key digital functionalities.&#x20;

## 4.1 HSM

The Hardware Security Module is an integral part of the eSignatures BB. The HSM ensures the protection of a key with utmost safety. Without a HSM the key can potentially fall in wrong hands and could result in huge mistrust. All keys used in our one time signatures are  created, used and destroyed within the HSM. The HSM should be configured with FIPS 140-2 Level 3.&#x20;

## 4.2 SCD

The SCD is the component where the users private key would be stored. The SCD could be a Smart card, Mobile App, Sim card App or equivalent. The SCD interacts with the eSignature BB using its own internal protocol. Every eSignature BB will support one or many such SCD. Most of the SCD would be protected with a secure PIN/Biometrics.

## 4.3 Timestamp

Time of a sign is an important part of the signature. Without a proper time of the signature we can never trust the signature, as one can not find if the signature happened before its expiry or after expiry. Most often this functionality is provided by the timestamping server hosted by the CA.

## 4.4 One Time Signing Service

This is one of the key functionality in eSignatures. This service is responsible to provide the One Time Signature API and interact with the HSM. This service validates the user against the Authorization Building Block.  A valid user is allowed to create a key in HSM and sign it.  Every key created here will also need a X509 certificate. The certificate management module will publish this created X509 certificate. &#x20;

## 4.5 SCD On-Boarding

SCD On-Boarding is the module responsible for the binding of the SCD & User. The module interacts with the Identity BB and would validate the user's precense before issuing the Certificate. This module is responsible to talk to the SCD for all types of key management & administrative needs. This module is hosted on a server and would ensure to maintain clear audit records and KYC records.

## 4.6 SCD Signing

The SCD Signing is one of the key functionality of eSignatures BB. When a user holds his key in a SCD then this module is responsible to interact with the SCD to sign any required document. This module works in a asynchronous mode. A signature is requested on demand using the API. But the module interacts with the SCD asynchronously.  The module is responsible to connect to SCD for all signing purposes.&#x20;

## 4.7 Certificate Management

All certificates that are created within the  SCD  will be hosted in this module. The modules let everyone have their X509 public certificate hosted for any verification. The module should have an administrative ability to let people revoke the keys on demand. The module has to maintain the OCSP & CRL-based revocations.&#x20;

## 4.8 Notification&#x20;

This module is responsible to notify the SCD device when a signature is needed. This helps the SCD to alert the user. The user can look through the notification and accept to sign the document. The module is also responsible for notification of a signature to the user's mobile phone/email/SCD. The notification to the user can be used as a audit record by the user.

##

