---
description: >-
  This section provides information on the core data structures/data models that
  are used by this Building Block.
---

# 7 Data Structures

## 7.1 Data Structures

### 7.1.1 eSignature operation

| Name                 | Type                                                                               | Description                                               |
| -------------------- | ---------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Signature Id         | string                                                                             | Identifier for signature operations                       |
| Signature type       | String enum ONETIME, SCD                                                           |                                                           |
| Signature format     | String Enum XAdES, CAdES, ASIC, JWS, PAdES                                         | Signature format that should be applied                   |
| Hash                 | String                                                                             | Hash to be signed in hex characters or base64             |
| Hash type            | String Enum of SHA2-256, SHA2-384, SHA2-512, SHA3-256, SHA3-384, SHA3-512, BLAKE2B | Hash type used                                            |
| Data to be displayed | String                                                                             | Text string to be shown on user’s device (SCD)            |
| Certificate          | String                                                                             | X509 Certificate in PEM format                            |
| Request timestamp    | Timestamp                                                                          | Timestamp of the request                                  |
| Signature            | Signature                                                                          | Signature of hex characters or base64 in requested format |
| Signature timestamp  | String                                                                             | rfc3161 asn.1 in base64                                   |
| Response timestmap   | Timestamp                                                                          | Timestamp of the response                                 |
| Status               | Enum of OK, ERROR                                                                  | Request status                                            |
| Status description   | String                                                                             | Description of status                                     |

### 7.1.2 eSignature operation with one-time certificate

| Name                 | Type       | Description                        |
| -------------------- | ---------- | ---------------------------------- |
| Authentication token | String Jwt | Token from ID Building Block       |
| Payment token        | String Jwt | Token from Payments Building Block |
| Signature id         | String     | Reference to eSignature operation  |

### 7.1.3 eSignature operation with user's device

| Name            | Type       | Description                       |
| --------------- | ---------- | --------------------------------- |
| Callback url    | String     | URL to call back with results     |
| Pseudonym token | Jwt String | Pseudonym token used              |
| Signature id    | String     | Reference to eSignature operation |

### 7.1.4 Certificates used with user's device

| Data element                   | Type                                                                                                                                                                              | Description                                                                                                                                                                                         |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authentication token           | String Jwt                                                                                                                                                                        | Token from ID Building Block                                                                                                                                                                        |
| Payment token                  | String Jwt                                                                                                                                                                        | Token from Payments Building Block                                                                                                                                                                  |
| CSR                            | String                                                                                                                                                                            | Certificate signing request PKCS#10 in PEM format                                                                                                                                                   |
| SCD Type                       | <p>String enum of REMOTE_SCD_APP_APPLE, REMOTE_SCD_APP_ANDROID, REMOTE_SCD_APP_SE_APPLE, REMOTE_SCD_APP_SE_ANDROID, REMOTE_SCD_SIM, REMOTE_SCD_ESIM,</p><p>REMOTE_SCD_SMARTID</p> | The SCD type that is used by user                                                                                                                                                                   |
| SCD Key id                     | Number                                                                                                                                                                            | Key id for case the SCD has multiple certificates                                                                                                                                                   |
| SCD Remote id                  | String                                                                                                                                                                            | <p>Remote identifier for the SCD communication, for REMOTE_SCD_APP* devices it is push ID, for REMOTE_SCD_ESIM/ REMOTE_SCD_SIM it is msisdn</p><p>For</p><p>REMOTE_SCD_SMARTID it is citizen id</p> |
| Pseudonym                      | String                                                                                                                                                                            | Unique pseudonym for the user that is bound to the specific SCD/Key id combo                                                                                                                        |
| Certificate request timestamp  | Timestamp                                                                                                                                                                         | Timestamp for the certificate request                                                                                                                                                               |
| CertificateId                  | String                                                                                                                                                                            | Unique identifier for the certificate, SCD, Key id combo                                                                                                                                            |
| Certificate                    | String                                                                                                                                                                            | X509 Certificate in PEM format in ACTIVE status                                                                                                                                                     |
| Certificate response timestamp | Timestamp                                                                                                                                                                         | Timestamp for the Certificate response                                                                                                                                                              |
| Status                         | Enum of OK, ERROR                                                                                                                                                                 | Request status                                                                                                                                                                                      |
| Status description             | String                                                                                                                                                                            | Description of status                                                                                                                                                                               |
