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

## eSignature Lifecycle

There are two lifecycles available for the eSignature building block. Both the mechanism has its own unique advantages. Its recommended to follow both approaches for better inclusivity&#x20;

Lifecyle Approach 1

\<Attach a simple diagram>

In the above approach, we have assumed that everyone ...

Lifecyle Approach 2

\<Attach a simple diagram>

SCD based approach

### 2.1.1 Users should be able to

* View & give consent to the document that is about to be signed
* register user's Signature Creation Device (SCD)&#x20;
* confirm the signature with PIN code on user's SCD&#x20;
* view users SCD-s and certificates

### 2.1.2 Services should be able to&#x20;

* sign digital document in desired eSignature format
* verification?

### 2.1.3 eSignature library

eSignature BB will provide a helper library to Services requiring to implement the BB.

This library will help to

* get digital document digest to be sent to eSignature BB. This step is used because of keeping storage requirements of eSignature BB low and avoid privacy concents
* embed received eSignature back into document and return standards based and validatable digital document with eSignature

###

### 2.1.5 Authentication and security

In order for eSignatures to be secure and adhere to privacy regulations the eSignature BB uses following levels of authentication

* Authentication via ID BB - Service that uses eSIgnature will have to authenticate the user against ID BB.
* Unique pseudonym - Service is redirected to a webpage where user can enter unique pseudonym known to the user only to start the signing process
* Asking PIN code on user's device - Signature BB will send a request to user's device so that user can confirm the signing request with a PIN code

### 2.1.6 Audit Trail and Compliance

eSignature BB must log all signing transactions to be compliant with current regulations. The minimum details to be logged are

* User's identity
* Document digest
* Timestamp

## 2.2 Out of Scope

* Document storage - no documents will be accepted or stored in the service
* Biometric signatures - no support for biometric devices
* Handwritten signatures - no support for handwritten signatures that are scanned or on paper.&#x20;
* No embedded handwtritten signature pictures
* No Administrative APIs
* No support for Signing queues, i.e waiting for multiple parties to sign
* No user interface (except for pseudonym entry page)
* No notification or remainders about pending signatures













