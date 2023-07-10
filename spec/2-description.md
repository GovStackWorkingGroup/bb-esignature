# 2 Description

eSignature building block provides the necessary functionality to bring handwritten signatures to the digital world. Handwritten signatures have served as a way to agree/witness a given document. But in today's digital world, most of the documents are in digital form. The digital form varies between structured (XML, JSON ) and unstructured documents(PDF, Word, Image, CSV, Spreadsheet).  eSignatures can be added to digital documents similar to handwritten signatures achieving the same functionality.

Also, eSignatures improve user experience in managing the signing process as the same can be embedded directly in e-Services, leaving out the need to print out forms, sign on paper, scan & upload/send.

eSignature provides a huge advantage over handwritten signatures. They offer verification at any point in time. This allows for remote validation of signatures, content (Content same as that during signing), identity and time. This assurance gives us the ability to trust a signed document remotely and can be used for legally binding agreements. Sample use cases include:

* Submitting applications to Government agencies (Child care, Residence Registration, Marrying, etc)
* Purchase and use banking services (Making transfers, Adding transfer limits, Applying for loans)
* Purchasing telecom services (Purchase SIM / eSIM, Change contract, Add TV subscription)
* Purchase Utility services (new contract for electricity, gas)
* Purchase insurance contract

With eSignature there is no need to print documents on paper anymore, saving a lot of paper and promoting a green lifestyle. This can also save money and can be calculated at [https://blog.dokobit.com/news/e-signature-calculator-check-out-how-much-you-could-save/](https://blog.dokobit.com/news/e-signature-calculator-check-out-how-much-you-could-save/)

## 2.1 Current scope

The current scope is to solve the following&#x20;

* Ability to support eSignature for everyone.
* Ability to support eSignature through a specialized user device/card.
* The ability for 3rd party services (including other building blocks) to interact, sign & verify the eSignatures in a standardized model.

### 2.1.1 Actors

* Users - People or Applications (delegated by a User) who use the eSignature Building Block to give eSignatures.
* Services - 3rd party services that require user eSignature to provide the service
* Auditor - Individual or Organization that reviews the platform for any misuse (Intentional & Unintentional)
* Administrator - Individual Or Team that configures the eSignature building block and is responsible to ensure the functioning of the building block.
* Certification Authority - A certification authority that can issue a certificate as X509.
* Timestamp Authority - A trusted third-party who can provide certified time.&#x20;

## 2.2 eSignature Lifecycle

There are two lifecycles available for the eSignature building block. Both the mechanism has its own unique advantages. Its recommended to follow both approaches for an inclusive approach&#x20;

### 2.2.1 One Time Signature Approach

One-time signatures are one of the easiest ways to get large-scale adoption of eSignatures. This approach does not require any device to be owned by the end user.  This approach relies on the work done by the ID Building block to authenticate an end user.

<figure><img src=".gitbook/assets/LifeCycle1.jpg" alt=""><figcaption><p>One Time Signature</p></figcaption></figure>

* User authenticates against the ID BB
* The user is redirected to the eSignatures BB
* A new key pair is created in the HSM (Hardware Security Module)
* An X509 Certificate is issued with the details from the ID Building block (Name, Age, Gender, Location)&#x20;
* The new key is used to timestamp & sign the document.
* The X509 certificate is set to expire 1 minute from the time of creation. &#x20;
* The Signed document is sent.&#x20;
* The private key is deleted from the HSM.

### 2.2.2 SCD based approach

The SCD (Signature Creation Device) is a personal device of the user. It could be a Mobile Phone, Sim Card, Smart Card, Secure SD Card, USB Storage device, NFC Card etc. The SCD device can be used to store the keys for long-term usage. This allows the user to interact with ID BB once and create a key on the SCD. This key then can be used for signing any document without interacting with the ID Building block.

<div data-full-width="true">

<figure><img src=".gitbook/assets/Onboard.jpg" alt=""><figcaption><p>SCD Onboard</p></figcaption></figure>

</div>

The binding of the private key with the user is called On-boarding. In this process, a user is authenticated and his key is created on the SCD.&#x20;

* User authenticates against the ID BB
* The user is redirected to the eSignature page where his SCD device is detected.
* The user is asked to select a valid SCD device and enter its security PIN / Biometric / OTP.
* The eSignature BB interacts with the SCD (Protocols are left open for implementation) to create a  Key Pair.
* A CSR (Certificate Signing Request) is created&#x20;
* This request is sent to the eSignature building block.
* The building block verified the ID BB token and the data in the CSR.
* If they match then the CSR is converted to an X509 certificate and the same is issued back to the device.

<figure><img src=".gitbook/assets/SCDSign.jpg" alt=""><figcaption><p>SCD Based Signature</p></figcaption></figure>

The key created on the SCD device can be used by the user to digitally sign any of the documents.

* The Third-Party who needs to sign the document will redirect to the eSignature building block.
* The eSignature BB will ask for the pseudonym (his eSignature handle) from the user.
* The user provides the pseudonym to the eSignature BB.
* The eSignature BB sends a notification to the SCD (Internal Protocol)
* The user is shown his choice to sign or not to sign.
* Once the user signs the SCD will send the signature to the Third-Party.
* The Digital Signature will then be attached to the given document in one of the supported formats as described by the eSignature BB.

## 2.3 Current Scope

### 2.3.1 This building block must enable user to

* View & Provide consent to the document that is about to be signed
* Register the user's Signature Creation Device (SCD)&#x20;
* Confirm the signature with PIN code on the user's SCD&#x20;
* View user's SCD-s and certificates
* Digitally sign the documents (PDF, Word, Excel, JSON, XML, Image)
* Use a personal device to store the keys safely.
* Ability to sign the document where the user has no device.&#x20;
* Ability to sign a document without the involvement of ID BB
*   Ability to sign a document using only the ID issued by the ID building block

    User
* Ability to view the list of signings performed.

### 2.3.2 This building block must enable other eServices  to

* Invoke eSignatures to obtain a digital signature
* Sign the digital document in desired eSignature format
* Allows safe async way to obtain signatures
* A simple-to-use library to validate the eSignature

### 2.3.3 This building block must enable auditor to

* Retrieve and review specific audit data.
* Validate and get signatures on any audit data.
* Audit cryptographic functioning and compliance for auditing & key security

### 2.3.4 This building block must enable the administrator to

* Configure the system without intervening with the signature process.
* Administer without modification or tampering with the data or key security.

## 2.4 eSignature library

eSignature BB will provide a helper library for the Services. The helper library could be used to integrate eSignatures faster.&#x20;

* Get digital document digest to be sent to eSignature BB.  Obtaining just the hash reduces the storage overhead and also avoids the privacy concern of sending the original document.
* Embedding received eSignature back into the document or attaching it in case of detached signatures.&#x20;
* Validate digitally signed documents and the validity of the certificate.

## 2.5 eSignature formats

Supports the following signature formats:

* [XAdES -  XML signatures](https://www.w3.org/TR/XAdES/)
* [PAdES - PDF signatures](https://www.iso.org/standard/67937.html)
* [CAdES - CMS Signatures](https://www.rfc-editor.org/rfc/rfc5126)
* [ASIC - Interoperable signatures](https://www.etsi.org/deliver/etsi\_en/319100\_319199/31916201/01.01.01\_60/en\_31916201v010101p.pdf)
* [JWS (RFC 7515)](https://www.rfc-editor.org/rfc/rfc7515)

## 2.6 Authentication and Security

In order for eSignatures to be secure and adhere to privacy regulations the eSignature BB uses the following levels of authentication

* Authentication via ID BB - The service that uses eSignature will have to authenticate the user against ID BB.
* Unique pseudonym - The service is redirected to a webpage on eSignature portal where the user can enter a unique pseudonym known only to the user to start the signing process. Of course without a pin the signing will not be complete.
* Asking for PIN code on the user's device - eSignature BB will send a request to the user's device so that the user can confirm the signing request with a PIN.
* The signature will be returned using an internal API protected by the Information Mediation Block

## 2.7 Audit Trail and Compliance

eSignature BB must log all signing transactions to be compliant with current regulations. The minimum details to be logged are

* User's identity without revealing personally identifiable information.
* Document digest.
* Timestamp of the signing.

## 2.8 Out of Scope

* Document storage - no documents will be accepted or stored in the service
* Communication with the SCD is left out of scope it's up to the eSignature service provider.
* Biometric signatures - no support for biometric devices
* Handwritten signatures - no support for handwritten signatures that are scanned or on paper.&#x20;
* No embedded handwritten signature pictures
* No Administrative APIs
* No support for Signing queues, i.e waiting for multiple parties to sign
* No user interface (except for the pseudonym entry page)
* No notification or remainders about pending signatures













