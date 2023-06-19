# 4 Key Digital Functionalities

eSignature building block provides the following key functionalities.

* User
  1. Digitally sign the documents (PDF, Word, Excell, JSON, XML, Image)
  2. Use a personal device to store the keys safely.
  3. Ability to sign the document where the user has no device.&#x20;
  4. Ability to sign a document without the involvement of ID BB
  5. Ability to sign a document only the ID issued by the ID building block
* Third-party
  1. API to invoke eSignatures
  2. Trust users from the ID Building block
  3. Allows safe async way to obtain signatures
  4. A simple-to-use library to validate the signature.
* Auditor
  1. API to retrieve specific audit data.
  2. API to validate and get signatures on any audit data.
  3. Cryptographic audits and guidelines should be followed for auditing of key secruity
* Administrator
  1. Ability to configure the system without intervening with the signature process.
  2. No APIs are provided for administrative needs.

## 4.1 Supported Formats

* [XAdES](https://www.w3.org/TR/XAdES/)&#x20;
* [CAdES](https://www.rfc-editor.org/rfc/rfc5126)&#x20;
* [ASIC](https://www.etsi.org/deliver/etsi\_en/319100\_319199/31916201/01.01.01\_60/en\_31916201v010101p.pdf)&#x20;
* [JWS](https://www.rfc-editor.org/rfc/rfc7515)&#x20;
* [PAdES](https://www.iso.org/standard/67937.html)

## 4.1  Capture digital Signature for a document

describe this kdf and its sub-topics such as&#x20;

4.1.1 one-time signature: meanw what? what shouldbe considered as functional requirements to create this kdf in this bb?

4.1.2 scd based signature





4.2   verify signature for a document

4.3 get signature

4.4 delete signature

4.5 update signature

## 4.2 One-Time Signature:

One-time signatures are one of the easiest ways to get large-scale adoption of eSignatures. This approach does not require any device to be owned by the end user.  This approach relies on the work done by the ID Building block to authenticate an end user.&#x20;

* User authenticates against the ID BB
* The user is redirected to the eSignatures BB
* A new key pair is created in the HSM (Hardware Security Module)
* An X509 Certificate is issued with the details from the ID Building block (Name, Age, Gender, Location)&#x20;
* The new key is used to timestamp & sign the document.
* The X509 certificate is set to expire 1 minute from the time of creation. &#x20;
* The Signed document is sent.&#x20;
* The private key is deleted from the HSM.

This approach works well for users who do not have handheld devices or cards. There is fewer logistics and solves the problem inclusively.&#x20;

## 4.2 SCD-based Signature:&#x20;

The SCD (Signature Creation Device) is a personal device of the user. It could be a Mobile Phone, Sim Card, Smart Card, Secure SD Card, USB Storage device, NFC Card etc. The SCD device can be used to store the keys for long-term usage. This allows the user to interact with ID BB once and create a key on the SCD. This key then can be used for signing any document without interacting with the ID Building block.&#x20;

### 4.2.1 Onboarding

The binding of the private key with the user is called Onboarding. In this process, a user is authenticated and his key is created on the SCD.&#x20;

* User authenticates against the ID BB
* The user is redirected to the eSignature page where his SCD device is detected.
* The user is asked to select a valid SCD device and enter its security PIN/Biometric/OTP.
* The eSignature BB interacts with the SCD (Protocols are left open for implementation) to create a  Key Pair.
* A CSR (Certificate Signing Request) is created&#x20;
* This request is sent to the eSignature building block.
* The building block verified the ID BB token and the data in the CSR.
* If they match then the CSR is converted to an X509 certificate and the same is issued back to the device.

This completed the Onboarding process and now the Key for signing the request stays on the SCD.

### 4.2.2 Usage

The key created on the SCD device can be used by the user to digitally sign any of the documents.

* The Third-Party who needs to sign the document will redirect to the eSignature building block.
* The eSignature BB will ask for the pseudonym (his eSignature handle) from the user.
* The user provides the pseudonym to the eSignature BB.
* The eSignature BB sends a notification to the SCD (Internal Protocol)
* The user is shown with his choice to sign or not to sign.
* Once the user signs the SCD will send the signature to the Third-Party.
* The eSignature will then be attached to the given document in one of the supported formats.
