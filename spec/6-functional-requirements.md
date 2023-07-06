# 6 Functional Requirements

The eSignature BB has several functional layers within it. Some functional layers follow the existing set of protocols and custom protocols, While the other functional requirements are defined within this specification. In this section, we will provide a clear indication to state what blocks follow what kind of protocols.

## 6.1 HSM (REQUIRED)

6.1.1 In case of the One-time signature A HSM MUST be used to create cryptographic keys. (Required)

6.1.2 It MUST be used to sign a certificate. (Required)

6.1.3 Keys SHALL NOT be exported

6.1.4 MUST be protected well with best security practices.

## 6.2 SCD (REQUIRED)

6.2.1 SCD Device SHOULD have secure storage to protect private keys

6.2.2 SCD MAY have proprietary API's with the e-Signature block.

6.2.3 SCD is assumed to be with the user.

6.2.4 User PIN is a MUST for the SCD.

6.2.5 Keys SHALL NOT be exportable.

## 6.3 Timestamp (REQUIRED)

6.3.1 For a valid signature, a Timestamp server is a MUST.

6.3.2 Timestamp server SHALL follow RFC3161&#x20;

## 6.4 Certifying Authority (REQUIRED)

6.4.1 eSignature BB MAY be a certifying authority.

6.4.2 If not the BB SHALL have access to a certifying authority and can issue certificates or can be a Sub CA

## 6.5 eSignature Service (REQUIRED)

6.5.1 Service SHALL support onboarding of SCD

6.5.2 Service SHALL support both the key functionalities of signing using SCD and One-Time Signature.

6.5.3 User SHALL be authenticated through ID BB for Onetime Signature

6.5.4 User SHALL be allowed to perform signature through pseudonym without user login.

6.5.5 OPTIONALLY can support payments through a payment gateway.

6.5.6 SHALL support all the listed signature types.

6.5.7 SHALL support redirection and callback as per the specification.

## 6.6 Certificate Management (REQUIRED)

6.6.1 SHALL provide the ability to list & revoke a certificate.

6.6.2  User SHALL have the ability to revoke his/her keys (API based or through customer care)

6.6.3 Certificates SHALL have any of the following statuses

6.6.3.1 ACTIVE – certificate is active and can be used for signing

6.6.3.2 EXPIRED – certificates are expired and should be renewed

6.6.3.3 SUSPENDED – certificate is suspended. The reason for suspension SHALL be provided together with status information

6.6.3.4 REVOKED – certificate is revoked. The reason for revoking SHALL be provided together with status information

6.6.4 Users SHALL be able to view their own certificates and their statuses

## 6.7 Notification (REQUIRED)

6.7.1 SHALL provide the ability to notify the user over email or sms or app notification or any other equivalent

6.7.2 User SHALL be notified of failed and successful transactions.

## 6.8 Audit (REQUIRED)

&#x20;6.8.1 All user activities SHOULD be available for audit.

6.8.2 MAY have the feature to tamper-proof the audit records.

6.8.3 Auditors SHALL have the ability to get audit-proof of a transaction.

## 6.9 Logging (REQUIRED)

6.9.1 The system SHALL provide traceability across services.

6.9.2 The system SHALL provide logs to help debug the problems.

6.9.3 The system SHALL NOT print sensitive information.

## 6.10 Metrics (REQUIRED)

6.10.1 The system SHALL provide API to get health status

6.10.2 The service MAY expose APIs to provide metrics about the performance of the system &#x20;

**Note:** The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119)

