---
description: >-
  This section will highlight important requirements or describe any additional
  cross-cutting requirements that apply to this Building Block.
---

# 5 Cross-Cutting Requirements

The Cross-cutting requirements described in this section are an extension of the cross-cutting requirements defined in the architecture specification document.

## 5.1 HSM Compliance (REQUIRED)

HSM must be compliant to a minimum of FIPS 140-2 Level 3. This guarantees the protection of private keys. HSM/Key Management application shall not print any information about the end-use details. Keys should be created only within the HSM. This may be applicable to all other Building Blocks when dealing with cryptographic keys.

## 5.2 Audit (REQUIRED)

All audit logs shall be integrity-protected against tampering. The eSignature Building Block shall follow the data policy and audit logging requirements as laid out in the GovStack architecture.

## 5.3 Privacy (REQUIRED)

Signing using a single key can compromise the user's privacy in the long run. For example, a single key used to sign the consent of health form and agreement of the medical insurance could reveal that the consent and the agreement are from the same person. Generally available signed documents could be used to perform 360-degree profiling. This is in violation of the Generic Architectural Privacy recommendation. Privacy-preserving techniques can be used in signature schemes, document storage, or reducing the key's lifespan to protect the user's privacy.
