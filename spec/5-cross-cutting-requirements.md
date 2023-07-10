# 5 Cross-Cutting Requirements

## 5.1 HSM Compliance (REQUIRED)

HSM MUST be compliant to a minimum of FIPS 140-2 Level 3. This guarantees the protection of private keys. HSM/Key Management application shall not print any information about the end-use details. Keys should be created only within the HSM. This may be applicable to all other building blocks when dealing with cryptographic keys.

## 5.2 Audit (REQUIRED)

All audit logs SHALL be integrity protected against tampering. The eSignature BB shall follow the data policy and audit logging requirements as laid out in the Govstack architecture.

## 5.3 Privacy (OPTIONAL)

Signing using a single key can compromise the user's privacy in the longer run. For eg Single key used to sign consent of health form and agreement of the medical insurance could  reveal that the consent and the agreement is from the same person. Generally available signed documents could be used to perform 360 degree profiling. This is in violation to the Generic Architectural Privacy recommendation. Privacy-preserving techniques can be used in the signature schemes to protect the user's privacy.
