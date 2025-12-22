---
description: Terminology used within this specification.
---

# 3 Terminology

We recognise there are common terms across all ID related Building Blocks (Identity, E-Signature, Consent, Wallet).  We define these [here](/broken/pages/G8wr9foLwthyK0hPnuG9).

In addition the following terms are specific to the e-Signature Building Block.

### e-Signature

_(also known as eSignature, electronic signature, digital signature)_

A data unit which is used by a Signatory to indicate his or her link to a Document

### Certificate

Data that links a public key to a natural person and confirms the name of that person

### Signatory/User

A natural person or an application delegated by the user who can create a digital signature

### eSignature creation device (SCD)

Configured software and/or hardware used to create an eSignature. Two types of eSignature creation devices are supported:

* Local - Private keys are stored locally on mobile devices.
* Remote - Private keys are stored on the remote secure storage.

### Signing application, Signature requestor, Third-Party

An application that has the Document that needs the Signatory's signature

### Document (to be signed)

Data that needs to be signed by the Signatory. It can be any data file in an arbitrary format. Document to be signed is usually handled by a third party and made available to Signatory after signing.

### Onboarding

The process of identifying Signatory, issuing a Certificate, and binding it to an eSignature Creation Device.\
User identification is performed using Govstack's [Identity Building Block](https://identity.govstack.global).

### Hardware Security Module (HSM)

Hardware Security Module - a device or software that can store private keys safely.

### Signature Creation Device (SCD)

Signature Creation Device - Can be local or remote based on where the keys are stored.

### X509

A certificate format as defined in [V3](https://www.rfc-editor.org/rfc/rfc5280)

### Timestamp

Compliant to [RFC3161](https://www.rfc-editor.org/rfc/rfc3161)

### Sign

The process of using [SCD](3-terminology.md#signature-creation-device-scd) or One Time signature APIs to encrypt the hash of the document.

### Certificate Signing Request (CSR)

Certificate Signing Request as per [RFC 2986](https://datatracker.ietf.org/doc/html/rfc2986)

### One time Signature

A private key is created upon authentication of the user and expires right after the signature. Should not be confused with OTS or related signature models.

### Revocation

All revocation of certificates will be available over [OCSP](https://www.rfc-editor.org/rfc/rfc8954.html). Follows the respective standards RFC 8954.



