---
description: >-
  This section provides a detailed view of how this Building Block will interact
  with other Building Blocks to support common use cases.
---

# 9 Internal Workflows

## 9.1 Workflow for onetime signing

This internal workflow is used by the eSignature BB to deliver the onetime signature service. In order to make the sequence diagram easier to follow the eSIgnature BB is divided into frontend and backend parts. Frontend constitutes the functionality running in the user's internet browser and backend is the API running on a server.

Workflow is kicked off by an eService (3rd party service) using the eSignature client library to get a digest of the document to be signed. Using the digest(hash) the redirection request is made towards the eSignature BB frontend. If configured the BB will check that the Payment token supplied by the request is valid, If valid will continue with the workflow if not it should follow the specification set by the payment build block.

In the eSignature BB frontend, the user selects the option to use National ID to perform one-time signature. Then the user is redirected to the Identity BB to authenticate. Upon successful authentication, the user is returned back to the eSignature BB backend.&#x20;

Now the eSignature BB will use a Hardware Security Module (HSM) to generate a temporary keypair. From that keypair, the public part is used to generate a certificate and publish a short-lived (1 minute) certificate based on the supplied CA.

This private part of the key is used to sign  & timestamp the document's digest. The results are saved into a database/cache and a signature token is generated to reference the signature. The signature token is then returned to the eSignature frontend, and the User's flow is redirected back to the eService provider using the callback URL and signature token.

After receiving the signature token the eService provider can exchange the signature token for the actual signature from the eSignature BB backend. After finally receiving the signature, eService can merge it with the original document (Note: The format of the signature is important to merge) to get a signed version of it using the client side library received from the eSignature BB frontend.

```mermaid
sequenceDiagram
    participant eService
    participant eSignature BB frontend
    participant eSignature BB backend
    participant HSM
    participant ID BB
    participant CA
    participant TSA
    activate eService
    Note right of eService: Get document hash with client side library
    eService->>eSignature BB frontend: Browser redirects to /sign/interactive passing document hash
    deactivate eService
    activate eSignature BB frontend
    rect rgb(230, 245, 255)
    alt One time Signature Model
        eSignature BB frontend->>eSignature BB frontend: 
        Note right of eSignature BB frontend: User selects National ID based model
        eSignature BB frontend->>ID BB: Browser redirects for user authentication
        deactivate eSignature BB frontend
        activate ID BB
        ID BB->>ID BB: 
        Note right of ID BB: User logins using National ID
        ID BB->>eSignature BB frontend: Browser redirects to callback URL with authorization code
        deactivate ID BB
        activate eSignature BB frontend
        eSignature BB frontend->>eSignature BB backend: authorization code & document hash
        activate eSignature BB backend
        eSignature BB backend->>ID BB: Multiple API exchanges
        activate ID BB
        ID BB-->>eSignature BB backend: User data
        deactivate ID BB
        eSignature BB backend->>HSM: Create key with user data
        activate HSM
        HSM-->>eSignature BB backend: CSR
        deactivate HSM
        eSignature BB backend->>CA: Create certificate with CSR & publish
        activate CA
        CA-->>eSignature BB backend: Certificate
        deactivate CA
        eSignature BB backend-->>HSM: Sign with key & delete
        activate HSM
        HSM-->>eSignature BB backend: signature
        deactivate HSM
    end
    end
    eSignature BB backend->>TSA: Get timestamp for signature
    activate TSA
    TSA-->>eSignature BB backend: Timestamp rfc3161
    deactivate TSA
    eSignature BB backend-->>eSignature BB frontend: Signature Id
    deactivate eSignature BB backend
    eSignature BB frontend->>eService: Browser redirects to callback URL with Signature Id
    deactivate eSignature BB frontend
    activate eService
    eService->>eSignature BB backend: API call /sign/response
    activate eSignature BB backend
    eSignature BB backend-->>eService: signature&timestamp
    deactivate eSignature BB backend
    Note right of eService: Merge signature using client side library
    deactivate eService
```

## 9.2 Workflows for signing with user's device

In the case of signing in with the user's device, there are multiple workflows

* Register the user's Signature Creation Device (SCD)
* Signing with the user's Signature Creation/Seal Device (SCD)

### 9.2.1 Register user's Signature Creation Device (SCD)

Registering starts with the User authenticating against ID BB. It's expected that the ID BB authenticates and provides the necessary eKYC functionality.  A  strong (presence-based) authentication is recommended. After the user is authenticated, a Remote SCD service is called to onboard the user.

Once the eKYC is successful a request is sent to the user's device to create keys. After keys are generated the public part of keypair is sent to eSignature BB as a Certificate Signing Request (CSR). CSR is then submitted to the CA who will generate and publish a certificate. Officially a unique pseudonym (or a handle) is created. The pseudonym could be auto-created or user can set the same.

```mermaid
sequenceDiagram
    actor User
    User->>ID BB: Authenticate with eSignature scope
    activate ID BB
    ID BB-->>User: Access token
    User->>eSignature BB: Provide authentication token
    activate eSignature BB
    eSignature BB->>ID BB: Invoke introspect API with the Access token
    ID BB-->>eSignature BB: user details, user PSUT
    deactivate ID BB
    eSignature BB->>Remote SCD Service: onboard user
    activate Remote SCD Service
    Remote SCD Service->>User: Accept key creation, choose PIN
    User-->>Remote SCD Service: CSR
    Note right of User: User accepts key creation and choose PIN with a mobile device
    Remote SCD Service-->>eSignature BB: CSR
    deactivate Remote SCD Service
    eSignature BB->>CA: Create a certificate with CSR & publish
    activate CA
    CA-->>eSignature BB: Certificate
    deactivate CA
    eSignature BB-->>User: SCD Onboarded and pseudonym is set
    deactivate eSignature BB

```

### 9.2.2 Use the user's Signature/Seal Creation Device (SCD) for signing

This internal workflow is for signing the document with the user Signature/Seal Creation Device (SCD).

In order to make the sequence diagram easier to follow the eSIgnature BB is divided into frontend and backend parts. Frontend constitutes the functionality running in the user's internet browser and backend is the API running on a server.

First, eService fetches the client side library from the eSignature BB frontend. The client library is used to create a digest of the document to be signed. Using the digest(hash) the redirection request is made towards eSignature BB frontend.&#x20;

In the eSignature BB frontend, the user selects the option to use SCD model. The eSignature BB takes the user to the page requesting the pseudonym. The user enters the pseudonym and the same is sent to the eSignature BB backend. After receiving a pseudonym token, the eSignature BB backend can be invoked to create the signature.

eSignature BB backend will then invoke Remote SCD Service to create the signature. The communication between the eSignature BB and its SCD is not defined and is left to the choice of the implementor.  The SCD could be a remote device, a mobile phone, SIM Card or a smartcard etc. Remote SCD service will send a notification to the user. The user can then accept this and will type the PIN to unlock. After the user enters the PIN, the signature is generated and sent back to the Remote SCD service. Remote SCD Service will then send the signature back to eSignature BB backend.

After the Signature is received, eSignature BB backend will send request to Timestamping Authority for a timestamp on the signature to be created. After timestamp is generated and received on a signature, the results are saved into a database and a signature token is generated to reference the signature data.

The signature token is then returned to eSignature frontend, and the User's flow is redirected back to eService provider using the callback url and signature token.

After receiving the signature token the eService provider can then receive the signature from eSignature BB backend. As an option, the eSignature BB backend can verify the requests coming from the correct IP or use an OAUTH bearer token or use the IM BB to protect.

After receiving the signature, eService can merge it with the original document to get a signed version of it using the client side library received from eSignature BB frontend.

```mermaid
sequenceDiagram
    participant eService
    participant eSignature BB frontend
    participant eSignature BB backend
    participant Remote SCD Service
    participant TSA
    activate eService
    Note right of eService: Get document hash with client side library
    eService->>eSignature BB backend: Browser redirects to /sign/interactive passing document hash
    deactivate eService
    activate eSignature BB backend
    eSignature BB backend-->>eSignature BB frontend: Page to display the available eSignature models
    deactivate eSignature BB backend
    activate eSignature BB frontend
    rect rgb(230, 245, 255)
    alt SCD Based Signature Model
        eSignature BB frontend->>eSignature BB frontend: 
        Note right of eSignature BB frontend: User selects "Use SCD to Sign" <br> and enters pseodonym
        eSignature BB frontend->>eSignature BB backend: API call /sign/pseudonym
        activate eSignature BB backend
        eSignature BB backend->>Remote SCD Service: document hash, SCD Remote Id
        activate Remote SCD Service
        Remote SCD Service->>Remote SCD Service: 
        Note right of Remote SCD Service: User enters Security PIN
        Remote SCD Service-->>eSignature BB backend: Signature
        deactivate Remote SCD Service
    end
    end
    eSignature BB backend->>TSA: Get timestamp for signature
    activate TSA
    TSA-->>eSignature BB backend: Timestamp rfc3161
    deactivate TSA
    eSignature BB backend-->>eSignature BB frontend: Signature Id
    deactivate eSignature BB backend
    eSignature BB frontend->>eService: Browser redirects to callback URL with Signature Id
    deactivate eSignature BB frontend
    activate eService
    eService->>eSignature BB backend: API call /sign/response
    activate eSignature BB backend
    eSignature BB backend-->>eService: signature&timestamp
    deactivate eSignature BB backend
    Note right of eService: Merge signature using client side library
    deactivate eService
```
