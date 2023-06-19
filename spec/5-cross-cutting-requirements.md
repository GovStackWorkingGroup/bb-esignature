# 5 Cross-Cutting Requirements

## 5.1 HSM Compliance (REQUIRED)

HSM MUST be compliant to a minimum of FIPS 140-2 Level 3. This guarantees the protection of private keys. HSM/Key Management application shall not print any information about the end-use details. Keys should be created only within the HSM.&#x20;

## 5.2 Key Deletion (REQUIRED)

Keys created during One Time Signature should be deleted as soon as the signature process is over. Logs SHOULD be kept in a database of the details of the deletion. Logs MUST include timestamps and identify the user and affiliation that performed the transaction.

## 5.3 Audit (REQUIRED)

All audit logs SHALL be integrity protected against tampering. The Consent BB shall follow the data policy and audit logging requirements as laid out in the Govstack architecture.

## 5.4 SCD Compliance (REQUIRED)

The SCD SHOULD be qualified with at least one of the following FIPS 14-2 Level 3 or Annex II of [Regulation (EU) No 910/2014 (eIDAS)](https://en.wikipedia.org/wiki/EIDAS) or equivalent common criteria certification.

## 5.5 Privacy (OPTIONAL)

Signing using a single key can compromise the user's privacy in the longer run. Privacy-preserving techniques can be used in the signature schemes to protect the user's privacy.
