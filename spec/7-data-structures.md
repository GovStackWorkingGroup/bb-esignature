---
description: >-
  This section provides information on the core data structures/data models that
  are used by this Building Block.
---

# 7 Data Structures

## 7.1 Data Elements

### 7.1.1 eSignature operation

| Name               | Type      | Description                                                                                                  |
| ------------------ | --------- | ------------------------------------------------------------------------------------------------------------ |
| SignatureId        | String    | Unique Signature Token for signature operations. This can be a random String as well.                        |
| SignatureType      | Enum      | Can be ONETIME or SCD                                                                                        |
| SignatureFormat    | Enum      | Signature format that should be applied. Can be XAdES, CAdES, ASIC, JWS, PAdES                               |
| Hash               | String    | Hash to be signed in hex characters or base64                                                                |
| HashType           | Enum      | Hash type - SHA2-256, SHA2-384, SHA2-512, SHA3-256, SHA3-384, SHA3-512, BLAKE2B                              |
| DisplayData        | String    | Text string to be shown on user’s device (SCD). Limited to 256 characters.                                   |
| Certificate        | String    | X509 Certificate in PEM format                                                                               |
| RequestTimestamp   | Timestamp | Timestamp of the request                                                                                     |
| Signature          | Signature | Signature in base64 format                                                                                   |
| SignatureTimestamp | String    | rfc3161 asn.1 in base64                                                                                      |
| ResponseTimestmap  | Timestamp | Timestamp of the response                                                                                    |
| Status             | Enum      | Request status enum. Can be OK, ERROR                                                                        |
| StatusDesc         | String    | Description of status                                                                                        |
| CallbackURL        | URL       | URL to call back with results                                                                                |
| Pseudonym          | String    | Unique pseudonym for the user that is bound to the specific SCD/Key id combo. We can call this as Key Handle |

### 7.1.2 eSignature operation header

| Name         | Type   | Description                            |
| ------------ | ------ | -------------------------------------- |
| AuthToken    | String | JWT Token from ID Building Block       |
| PaymentToken | String | Jwt Token from Payments Building Block |

### 7.1.3 User's Device Onboarding

| Name              | Type      | Description                                                                                                                                                                                                     |
| ----------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AuthToken         | String    | JWT Token from ID Building Block                                                                                                                                                                                |
| PaymentToken      | String    | JWT Token from Payments Building Block                                                                                                                                                                          |
| CSR               | String    | Certificate signing request PKCS#10 in PEM format                                                                                                                                                               |
| SCDType           | Enum      | <p>The SCD type that is used by user. Can be of REMOTE_SCD_APP_APPLE, REMOTE_SCD_APP_ANDROID, REMOTE_SCD_APP_SE_APPLE, REMOTE_SCD_APP_SE_ANDROID, REMOTE_SCD_SIM, REMOTE_SCD_ESIM,</p><p>REMOTE_SCD_SMARTID</p> |
| SCDKeyId          | Number    | Key id for case the SCD has multiple certificates                                                                                                                                                               |
| SCDRemoteId       | String    | <p>Remote identifier for the SCD communication, for REMOTE_SCD_APP* devices it is push ID, for REMOTE_SCD_ESIM/ REMOTE_SCD_SIM it is msisdn</p><p>For</p><p>REMOTE_SCD_SMARTID it is citizen id</p>             |
| Pseudonym         | String    | Unique pseudonym for the user that is bound to the specific SCD/Key id combo. We can call this as Key Handle                                                                                                    |
| CertReqTimestamp  | Timestamp | Timestamp for the certificate request                                                                                                                                                                           |
| CertId            | String    | Unique identifier for the certificate, SCD, Key id combo                                                                                                                                                        |
| Certificate       | String    | X509 Certificate in PEM format in ACTIVE status                                                                                                                                                                 |
| CertRespTimestamp | Timestamp | Timestamp for the Certificate response                                                                                                                                                                          |
| Status            | Enum      | Request status. Can be of  of OK, ERROR                                                                                                                                                                         |
| StatusDesc        | String    | Description of status                                                                                                                                                                                           |
