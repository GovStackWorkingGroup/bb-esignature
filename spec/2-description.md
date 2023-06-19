# 2 Description

eSignature building block provides the necessary functionality to bring handwritten signatures to the digital world. Handwritten signatures have served as a way to agree/witness a given document. But in today's digital world, most of the documents are in digital form. The digital form varies between structured (XML, JSON ) and unstructured documents(PDF, Word, Image, CSV, Spreadsheet).  eSignatures can be added to these digital documents similar to handwritten signatures achieving the same functionality.



Another benefit is improved user experience in managing the signing process as the signing process can be embedded directly in e-Services, leaving out the need to print out forms, sign on paper, scan & upload/send.

eSignature provides a huge advantage over handwritten signatures. They can be used to verify if the signature matches the user & original content(Content same as that during signing). This assurance gives us the ability to trust a signed document remotely.  This allows the eSignature to be used for legally binding agreements. Sample use cases include:

* Submitting applications to Government agencies (Child care, Residence Registration, Marrying, etc)
* Purchase and use banking services (Making transfers, Adding transfer limits, Applying for loans)
* Purchasing telecom services (Purchase SIM/eSIM, Change contract, Add TV subscription)
* Purchase Utility services (new contract for electricity, gas)
* Purchase insurance contract

With eSignature there is no need to print documents on paper anymore, saving a lot of paper and promoting a green lifestyle. This can also save money and can be calculated at [https://blog.dokobit.com/news/e-signature-calculator-check-out-how-much-you-could-save/](https://blog.dokobit.com/news/e-signature-calculator-check-out-how-much-you-could-save/)

## 2.1 Current scope

The current scope is to solve the following&#x20;

* Ability to support eSignature for everyone.
* Ability to support eSignature through a specialized user device/card.
* The ability for 3rd party services (including other building blocks) to interact, sign & verify the eSignatures in a standardized model.

### 2.1.1 Actors

* Users - People who use the eSignature Building Block to give eSignatures.
* Services - 3rd party internet services that require user eSignature to provide the service
* Auditor - Individual or Organization that reviews the platform for any misuse(Intentional & Unintentional)
* Administrator - Individual Or Team that configures the eSignature building block.&#x20;

## 2.2 eSignature Lifecycle

There are two lifecycles available for the eSignature building block. Both the mechanism has its own unique advantages. Its recommended to follow both approaches for better inclusivity&#x20;

Lifecyle Approach 1

\<Attach a simple diagram>

In the above approach, we have assumed that everyone ...

Lifecyle Approach 2

\<Attach a simple diagram>

SCD based approach

### 2.1.1 Users should be able to

* View & give consent to the document that is about to be signed
* Register the user's Signature Creation Device (SCD)&#x20;
* Confirm the signature with PIN code on the user's SCD&#x20;
* View user's SCD-s and certificates
* Digitally sign the documents (PDF, Word, Excell, JSON, XML, Image)
* Use a personal device to store the keys safely.
* Ability to sign the document where the user has no device.&#x20;
* Ability to sign a document without the involvement of ID BB
*   Ability to sign a document only the ID issued by the ID building block

    User

### 2.1.2 Services &#x20;

* API to invoke eSignatures
* Sign the digital document in desired eSignature format
* Allows safe async way to obtain signatures
* A simple-to-use library to validate the eSignature

### 2.1.3 Auditor&#x20;

* API to retrieve specific audit data.
* API to validate and get signatures on any audit data.
* Cryptographic audits and guidelines should be followed for auditing of key security

### 2.1.4 Administrator&#x20;

* Ability to configure the system without intervening with the signature process.
* No APIs are provided for administrative needs.
* Should not be able to modify or alter the data.

## 2.3 eSignature library

eSignature BB will provide a helper library for the Services to use the BB.

This library will help to

* Get digital document digest to be sent to eSignature BB. This step is used because of keeping storage requirements of eSignature BB low and to avoid privacy concerns
* Embedding received eSignature back into the document and validate digital documents with eSignature

## 2.4 eSignature formats

Supports the following signature formats:

* [XAdES -  XML signatures](https://www.w3.org/TR/XAdES/)
* [PAdES - PDF signatures](https://www.iso.org/standard/67937.html)
* [CAdES - CMS Signatures](https://www.rfc-editor.org/rfc/rfc5126)
* [ASIC - Interoperable signatures](https://www.etsi.org/deliver/etsi\_en/319100\_319199/31916201/01.01.01\_60/en\_31916201v010101p.pdf)
* [JWS (RFC 7515)](https://www.rfc-editor.org/rfc/rfc7515)

## 2.5 Authentication and Security

In order for eSignatures to be secure and adhere to privacy regulations the eSignature BB uses the following levels of authentication

* Authentication via ID BB - The service that uses eSignature will have to authenticate the user against ID BB.
* Unique pseudonym - The service is redirected to a webpage where the user can enter a unique pseudonym known to the user only to start the signing process
* Asking for PIN code on the user's device - Signature BB will send a request to the user's device so that the user can confirm the signing request with a PIN code
* The signature will be returned using an internal API protected by the Information Mediation Block

## 2.6 Audit Trail and Compliance

eSignature BB must log all signing transactions to be compliant with current regulations. The minimum details to be logged are

* User's identity
* Document digest
* Timestamp

## 2.2 Out of Scope

* Document storage - no documents will be accepted or stored in the service
* Communication with the SCD is left out of scope it's up to the eSignature service provider.
* Biometric signatures - no support for biometric devices
* Handwritten signatures - no support for handwritten signatures that are scanned or on paper.&#x20;
* No embedded handwritten signature pictures
* No Administrative APIs
* No support for Signing queues, i.e waiting for multiple parties to sign
* No user interface (except for the pseudonym entry page)
* No notification or remainders about pending signatures













