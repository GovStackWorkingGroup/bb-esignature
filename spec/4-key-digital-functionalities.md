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
* Administrator
  1. Abiity to configure the system without intervening with the signature process.
  2. No API's provided for administrative needs.

### Supported Formats

* XAdES
* CAdES
* ASIC
* JWS (RFC 7515)
* PAdES

Limit the scope of work to the following

* Ability to create and manage keys in remote SCD. Requires Onboarding via ID Building block only once, after that user confirms the signature with PIN code on his/her device
* Ability to create and manage dynamic short-lived keys in local SCD (HSM). Requires Onboarding via ID building block for every eSignature.
* Generic use cases like payroll signing, agreement signing, consent, tax filing, request for registration, etc can be handled





* No administrative APIs are needed to cater to this requirement. So administrative APIs will be left out of the scope
* Client-side libraries to be provided to merge the signature with payload ( PDF, XML & JSON)
