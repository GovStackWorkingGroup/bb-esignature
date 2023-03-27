# 4 Key Digital Functionalities

Generally eSignature Building Block SHALL:

* onboard the Signatories using the ID Building Block
* enable unique identification of the Signatory in whose name the signature is given
* create eSignatures by using private key in eSignature creation device to which the public key uniquely correspond.
* enable determination of the time when the signature is given
* enable linking the eSignature to data in such a manner as to preclude the possibility of changing the data undetectably after the signature is given.
* enable verification of eSignatures

### Phase 1

Limit the scope of work to the following

* Ability to create and manage keys in remote SCD. Requires Onboarding via ID Building block only once, after that user confirms the signature with PIN code on his/her device
* Ability to create and manage dynamic short-lived keys in local SCD (HSM). Requires Onboarding via ID building block for every eSignature.
* Generic use cases like payroll signing, agreement signing, consent, tax filing, request for registration, etc can be handled
* Support for the following signature formats:
  * XAdES
  * CAdES
  * ASIC
  * JWS (RFC 7515)
  * PAdES
* No administrative APIs are needed to cater to this requirement. So administrative APIs will be left out of the scope
* Client-side libraries to be provided to merge the signature with payload ( PDF, XML & JSON)
