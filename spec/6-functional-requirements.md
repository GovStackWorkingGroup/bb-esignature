# 6 Functional Requirements

Govstack eSignature BB functional requirements consist of&#x20;

* eSignature with onetime certificate
* eSignature with user's device (SCD)
* Certificates management with user's device (SCD)

The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119

### 6.1 eSignature with one time certificate

6.1.1 Services SHALL be able to request user’s eSignature using one time certificate that is generated on the fly

6.1.2 Prerequisites for eSignature with one time certificate are:

6.1.2.1. User SHALL be authenticated via ID BB

6.1.2.2. User SHOULD have the payment completed via Payments BB

6.1.2.3. Service SHALL provide signature format

6.1.2.4. Service SHALL provide hash to be signed

6.1.3. Service SHALL be notified about error conditions, such as "authentication required", "payment required" or "mandatory parameter is missing"

6.1.4. One time certificate SHALL be created using the temporary keypair generated inside HSM

6.1.5. Service SHALL be notified about signature, certificate and signature timestamp on successful completion of one time signing

### 6.2 eSignature with user's device

#### 6.2.3 Certificate creation

6.2.3.1 Users SHALL be able to create their own signing certificates that are bound to user’s SCD

6.2.3.2 Prerequisites for certificate creation are

6.2.3.2.1 User SHALL be authenticated via ID BB

6.2.3.2.2. User SHOULD have the payment completed via Payments BB

6.2.3.2.3. User SHALL have information required for certificate generation and management provided by SCD

6.2.3.2.4. User SHOULD be able to provide a unique pseudonym that is going to be bound with the certificate

6.2.3.3 User SHALL be notified about error conditions, such as "authentication required", "payment required" or "mandatory parameter is missing"

6.2.3.4 User SHALL be provided with a certificate, certificateId and pseodonym on successful certificate creation

#### 6.2.4 Certificates status check

6.2.4.1. Users SHALL be able to view own certificates and their statuses

6.2.4.2 Legally appointed authorities SHALL be able to view all user’s certificates and their statuses

6.2.4.3 Prerequisites for certificate status check are

6.2.4.3.1 User or legally appointed authority SHALL be authenticated via ID BB

6.2.4.3.2 A filter condition SHOULD be provided by user or legally appointed authority

6.2.4 Certificates SHALL have any of following statuses

6.2.4.1 ACTIVE – certificate is active and can be used for signing

6.2.4.2 EXPIRED – certificates is expired and should be renewed

6.2.4.3 SUSPENDED – certificate is suspended. The reason of suspension SHALL be provided together with status information

6.2.4.4 REVOKED – certificate is revoked. The reason for revoking SHALL be provided together with status information

6.2.5 User SHALL be notified about error conditions, such as "authentication required"

6.2.6 List of all certificates and it’s statuses are returned to user or legally appointed authority on successful status check

#### 6.2.5 eSignature with user’s device (SCD)

6.2.5.1 Services SHALL be able to request user’s eSignature via user’s device (SCD).

6.2.5.2 Prerequisites for eSignature with user's device are:

6.2.5.2.1 Service SHALL provide callback URL

6.2.5.2.2 Service SHALL provide text to be displayed on user’s device (SCD)

6.2.5.2.3 Service SHALL provide signature format

6.2.5.2.4 Service SHALL provide hash to be signed

6.2.5.2.5 Service SHALL provide nonce string to counter replay attacks

6.2.5.2.6 Service SHALL provide state string to match the requests and callbacks

6.2.5.3 Service SHALL be notified about error conditions, such as "mandatory parameter is missing"

6.2.5.4 Service SHALL be notified about redirect URL

6.2.5.4.1 Service MUST redirect user to pseudonym entry webpage provided in redirect URL

6.2.5.4.2 After user enters the pseudonym on pseudonym entry webpage, the signature SHALL be generated

6.2.5.5 To perform the signature operation, the signing parameters (hash, text to be displayed) SHALL be sent to user’s device (SCD).

6.2.5.6. After user confirms the signing with a PIN code, the signature SHALL be sent back to eSignature BB.

6.2.5.7 Response id, nonce and state are returned to callback url on successful completion of signing operation. Service shall verify the nonce and state variables to be matching with the original requests before proceeding.

6.2.5.8 Formatted signature, certificate and signature timestamp are returned via internal API call using Response id

### 6.3 Auditing

6.3.1 Users and auditors SHALL be able to request user’s signing transactions

6.3.2 Prerequisites for auditing are:

6.3.2.1 User or Auditor SHALL be authenticated via ID BB

6.3.2.2 User or Auditor SHOULD set the start and end date

6.3.3 User or Auditor SHALL be notified about error conditions, such as "authentication required" or "mandatory parameter is missing"

6.3.4 User or Auditor SHALL be notified about list of signature, certificate and signature timestamp on successful completion of audit request&#x20;

## 6.5 Revision History (RECOMMENDED)



## 6.6 Change Notification Subscription (RECOMMENDED)



## 6.7 Change Notification (OPTIONAL)



## 6.8 Logging (REQUIRED)

