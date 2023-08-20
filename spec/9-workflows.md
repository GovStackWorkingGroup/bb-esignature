# 9 Internal Workflows

### 9.1 Workflow for onetime signing

This internal workflow is used by the eSignature BB to give onetime signature.

In order to make the sequence diagram easier to follow the eSIgnature BB is divided into frontend and backend parts. Frontend constitutes the functionality running in user's internet browser and backend is API running on a server.

Workflow is kicked off by a 3rd party using eSignature client library to get a digest of document to be signed. Using the digest(hash) the redirection request is made towards e-Signature BB frontend.

If required by the BB configuration, it will also check if the Payment token supplied by the request is valid.

In e-Signature BB frontend, user selects the option to use National ID to do onetime signature. Then user is redirected to Identity BB to authenticate and user data is returned back to e-Signature BB backend after completion of all standard interaction API calls.

Then a Host Security Module (HSM) hardware is used to generate a temporary keypair. From that keypair, public part is exported as Certificate Signing Request (CSR)

CSR is the submitted to a CA instance that will generate and publish a short lived (1 minute) certificate based on supplied CA.

After certificate has been created the private key in HSM is used to sign a document digest.

After Digest is signed, timestamp is requested on the signature from timestamping service.

After timestamp is generated and received on a signature, the results are saved into a database and signature id is generated to reference the signature data.

Signature id is then returned to e-Signature frontend, and the User's flow is redirected back to e-Service provider using the callback url and signature id.

After receiving the signature id the e-Service provider can then receive the signature from e-Signature BB backend. As an option e-Signature BB backend can verify the requests coming from correct IP.

After finally receiving the signature, e-Service can merge it with the original document to get a signed version of it using the client side library received from e-Signature BB frontend.

```mermaid
sequenceDiagram
    participant e-Service
    participant e-Signature BB frontend
    participant e-Signature BB backend
    participant HSM
    participant ID BB
    participant CA
    participant TSA
    activate e-Service
    Note right of e-Service: Get document hash with client side library
    e-Service->>e-Signature BB frontend: Browser redirects to /sign/interactive passing document hash
    deactivate e-Service
    activate e-Signature BB frontend
    rect rgb(230, 245, 255)
    alt One time Signature Model
        e-Signature BB frontend->>e-Signature BB frontend: 
        Note right of e-Signature BB frontend: User selects National ID based model
        e-Signature BB frontend->>ID BB: Browser redirects for user authentication
        deactivate e-Signature BB frontend
        activate ID BB
        ID BB->>ID BB: 
        Note right of ID BB: User logins using National ID
        ID BB->>e-Signature BB frontend: Browser redirects to callback URL with authorization code
        deactivate ID BB
        activate e-Signature BB frontend
        e-Signature BB frontend->>e-Signature BB backend: authorization code & document hash
        activate e-Signature BB backend
        e-Signature BB backend->>ID BB: Multiple API exchanges
        activate ID BB
        ID BB-->>e-Signature BB backend: User data
        deactivate ID BB
        e-Signature BB backend->>HSM: Create key with user data
        activate HSM
        HSM-->>e-Signature BB backend: CSR
        deactivate HSM
        e-Signature BB backend->>CA: Create certificate with CSR & publish
        activate CA
        CA-->>e-Signature BB backend: Certificate
        deactivate CA
        e-Signature BB backend-->>HSM: Sign with key & delete
        activate HSM
        HSM-->>e-Signature BB backend: signature
        deactivate HSM
    end
    end
    e-Signature BB backend->>TSA: Get timestamp for signature
    activate TSA
    TSA-->>e-Signature BB backend: Timestamp rfc3161
    deactivate TSA
    e-Signature BB backend-->>e-Signature BB frontend: Signature Id
    deactivate e-Signature BB backend
    e-Signature BB frontend->>e-Service: Browser redirects to callback URL with Signature Id
    deactivate e-Signature BB frontend
    activate e-Service
    e-Service->>e-Signature BB backend: api call /sign/response
    activate e-Signature BB backend
    e-Signature BB backend-->>e-Service: signature&timestamp
    deactivate e-Signature BB backend
    Note right of e-Service: Merge signature using client side library
    deactivate e-Service
```

### 9.2 Workflows for signing with user's device

In case of signing with user's device there are multiple workflows

* Register user's Signature Creation Device (SCD)
* Signing with user's Signature Creation Device (SCD)

#### 9.2.1 Register user's Signature Creation Device (SCD)

Registering start with User authenticating against ID BB and getting the authentication token.

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
    User-->>Remote SCD Service: CSR
    Note right of User: User accepts key creation and choose PIN with a mobile device
    Remote SCD Service-->>e-Signature BB: CSR
    deactivate Remote SCD Service
    e-Signature BB->>CA: Create certificate with CSR & publish
    activate CA
    CA-->>e-Signature BB: Certificate
    deactivate CA
    e-Signature BB-->>User: SCD Onboarded
    deactivate e-Signature BB

```

#### 9.2.2 Use user's Signature Creation Device (SCD) for signing

This internal workflow is for signing with users Signature Creation Device (SCD).

In order to make the sequence diagram easier to follow the eSIgnature BB is divided into frontend and backend parts. Frontend constitutes the functionality running in user's internet browser and backend is API running on a server.

First e-Service fetches the client side library from e-Signature BB frontend. Client library is used to create a digest of the document to be signed.Using the digest(hash) the redirection request is made towards e-Signature BB frontend.&#x20;

In e-Signature BB frontend, user selects the option to use SCD model. Pseudonym entry page is shown and user enters the pseudonym, which is sent to e-Signature BB backend to receive the generated pseudonym token. After receiving a pseudonym token, e-Signature BB backend can be invoked to create the signature.

e-Signature BB backend will then invoke Remote SCD Service to create the signature. Remote SCD service will send a notification to User's SCD with a notification and request to put PIN code. After User enters the PIN code, signature is generated and sent back to the Remote SCD Service. Remote SCD Service will then send the signature back to e-Signature BB backend.

After the Signature is received, e-Signature BB backend will send request to Timestamping Authority for a timestamp on the signature to be created. After timestamp is generated and received on a signature, the results are saved into a database and signature id is generated to reference the signature data.

Signature id is then returned to e-Signature frontend, and the User's flow is redirected back to e-Service provider using the callback url and signature id.

After receiving the signature id the e-Service provider can then receive the signature from e-Signature BB backend. As an option e-Signature BB backend can verify the requests coming from correct IP.

After finally receiving the signature, e-Service can merge it with the original document to get a signed version of it using the client side library received from e-Signature BB frontend.

```mermaid
sequenceDiagram
    participant e-Service
    participant e-Signature BB frontend
    participant e-Signature BB backend
    participant Remote SCD Service
    participant TSA
    activate e-Service
    Note right of e-Service: Get document hash with client side library
    e-Service->>e-Signature BB backend: Browser redirects to /sign/interactive passing document hash
    deactivate e-Service
    activate e-Signature BB backend
    e-Signature BB backend-->>e-Signature BB frontend: Page to display the available eSignature models
    deactivate e-Signature BB backend
    activate e-Signature BB frontend
    rect rgb(230, 245, 255)
    alt SCD Based Signature Model
        e-Signature BB frontend->>e-Signature BB frontend: 
        Note right of e-Signature BB frontend: User selects "Use SCD to Sign" <br> and enters pseodonym
        e-Signature BB frontend->>e-Signature BB backend: API call /sign/pseudonym
        activate e-Signature BB backend
        e-Signature BB backend->>Remote SCD Service: document hash, SCD Remote Id
        activate Remote SCD Service
        Remote SCD Service->>Remote SCD Service: 
        Note right of Remote SCD Service: User enters Security PIN
        Remote SCD Service-->>e-Signature BB backend: Signature
        deactivate Remote SCD Service
    end
    end
    e-Signature BB backend->>TSA: Get timestamp for signature
    activate TSA
    TSA-->>e-Signature BB backend: Timestamp rfc3161
    deactivate TSA
    e-Signature BB backend-->>e-Signature BB frontend: Signature Id
    deactivate e-Signature BB backend
    e-Signature BB frontend->>e-Service: Browser redirects to callback URL with Signature Id
    deactivate e-Signature BB frontend
    activate e-Service
    e-Service->>e-Signature BB backend: API call /sign/response
    activate e-Signature BB backend
    e-Signature BB backend-->>e-Service: signature&timestamp
    deactivate e-Signature BB backend
    Note right of e-Service: Merge signature using client side library
    deactivate e-Service
```
