# 9 Internal Workflows

### 9.1 Workflow for onetime signing

This internal workflow is used by the eSignature BB to give onetime signature.

Workflow is kicked off by a 3rd party using eSignature client library to get a digest of document to be signed

After submitting the call to eSignature BB, it will first check if the authentication token by ID BB is valid

If required by the BB configuration, it will also check if the Payment token supplied by the request is valid.

Then a Host Security Module (HSM) hardware is used to generate a temporary keypair. From that keypair, public part is exported as Certificate Signing Request (CSR)

CSR is the submitted to a CA instance that will generate and publish a short lived (1 minute) certificate based on supplied CA.

After certificate has been created the private key in HSM is used to sign a document digest.

After Digest is signed, timestamp is requested on the signature from timestamping service.

After receiving timestamp original 3rd party replied with signature response.

```mermaid
sequenceDiagram
    activate ID BB
    activate Registration&UI BB
    Note right of Registration&UI BB: Get document hash with client side library
    Registration&UI BB->>e-Signature BB: Sign hash with Access token
    activate e-Signature BB
    e-Signature BB->>ID BB: Invoke introspect API with Access token
    ID BB-->>e-Signature BB: user details, user PSUT
    deactivate ID BB
    alt One time Key
    e-Signature BB->>HSM: Create key with user data
    activate HSM
    HSM-->>e-Signature BB: CSR
    e-Signature BB->>CA: Create certificate with CSR & publish
    activate CA
    CA-->>e-Signature BB: Certificate
    deactivate CA
    e-Signature BB-->>HSM: Sign with key & delete
    HSM-->>e-Signature BB: signature
    deactivate HSM
    end
    e-Signature BB->>TSA: Get timestamp for signature
    activate TSA
    TSA-->>e-Signature BB: Timestamp rfc3161
    deactivate TSA
    e-Signature BB-->>Registration&UI BB: Signature with timestamp
    deactivate e-Signature BB
    Note right of Registration&UI BB: Merge signature using client side library
    deactivate Registration&UI BB

```

### 9.2 Workflows for signing with user's device

In case of signing with user's device there are multiple workflows

* Register user's Signature Creation Device (SCD)
* Signing with user's Signature Creation Device (SCD)

#### 9.2.1 Register user's Signature Creation Device (SCD)

Registering start with Mother authenticating against ID BB and getting the authentication token.

After user is authenticated, a Remote SCD service is called to onboard user.

There is a request sent to user's device to create keys.

After keys are generated the public part of keypair is sent to eSignature BB as a Certificate Signing Request (CSR).

CSR is the submitted to a CA instance that will generate and publish a certificate based on supplied CA.

```mermaid
sequenceDiagram
    actor User
    User->>ID BB: Authenticate with e-signature scope
    activate ID BB
    ID BB-->>User: Access token
    User->>e-Signature BB: Provide authentication token
    activate e-Signature BB
    e-Signature BB->>ID BB: Invoke introspect API with Access token
    ID BB-->>e-Signature BB: user details, user PSUT
    deactivate ID BB
    e-Signature BB->>Remote SCD Service: onboard user
    activate Remote SCD Service
    Remote SCD Service->>User: Accept key creation, choose PIN
    User-->>Remote SCD Service: Acceptance
    Note right of User: User accepts key creation and choose PIN with a mobile device
    Remote SCD Service->>e-Signature BB: OK
    deactivate Remote SCD Service
    e-Signature BB-->>User: SCD Onboarded
    deactivate e-Signature BB

```

#### 9.2.2 Use user's Signature Creation Device (SCD) for signing

```mermaid
sequenceDiagram
    activate Registration&UI BB
    Note right of Registration&UI BB: Get document hash with client side library
    Registration&UI BB->>e-Signature BB: Sign hash with Access token
    activate e-Signature BB
    e-Signature BB->>HSM: Create key with user data
    e-Signature BB->>CA: Create certificate with CSR & publish
    activate CA
    CA-->>e-Signature BB: Certificate
    deactivate CA
    e-Signature BB-->>HSM: Sign with key & delete
    HSM-->>e-Signature BB: signature

    e-Signature BB->>TSA: Get timestamp for signature
    activate TSA
    TSA-->>e-Signature BB: Timestamp rfc3161
    deactivate TSA
    e-Signature BB-->>Registration&UI BB: Signature with timestamp
    deactivate e-Signature BB
    Note right of Registration&UI BB: Merge signature using client side library
    deactivate Registration&UI BB
```
