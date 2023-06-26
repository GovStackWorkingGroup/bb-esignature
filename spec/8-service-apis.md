# 8 Service APIs

A Set of microservices are defined to receive requests from other GovStack-compatible Building Blocks and third party Services with relevant inputs and return processed results from key digital functionalities of this Building Block. This section provides a reference for APIs that should be implemented by this Building Block. The APIs defined here establish a blueprint for how the Building Block will interact with other Building Blocks or third party Services. Additional APIs may be implemented by the Building Block, but the listed APIs define a minimal set of functionality that should be provided by any implementation of this Building Block.

eSignature Building Block must expose its microservices through RESTful API interfaces as defined by OpenAPI v3+ standards.  A summary of the APIS exposed by this Building Block is summarized in the table below.&#x20;

### 8.1 eSignature with one time certificate



{% swagger src=".gitbook/assets/1606_3.yaml" path="/{version}/sign/onetime" method="post" %}
[1606_3.yaml](.gitbook/assets/1606_3.yaml)
{% endswagger %}

### 8.2 eSignature with user's device (SCD)

#### 8.2.1 Certificate creation

{% swagger src=".gitbook/assets/1606_3.yaml" path="/{version}/cert/create" method="post" %}
[1606_3.yaml](.gitbook/assets/1606_3.yaml)
{% endswagger %}

#### 8.2.2 List certificates

{% swagger src=".gitbook/assets/1606_3.yaml" path="/{version}/cert/list" method="get" %}
[1606_3.yaml](.gitbook/assets/1606_3.yaml)
{% endswagger %}

#### 8.2.3 Update certificate

{% swagger src=".gitbook/assets/1606_3.yaml" path="/{version}/cert/{certificateId}" method="patch" %}
[1606_3.yaml](.gitbook/assets/1606_3.yaml)
{% endswagger %}

#### 8.2.4 eSignature with user's device

{% swagger src=".gitbook/assets/1606_3.yaml" path="/{version}/sign/pseudonym" method="post" %}
[1606_3.yaml](.gitbook/assets/1606_3.yaml)
{% endswagger %}

#### 8.2.5 Webservice to enter user pseudonym

{% swagger src=".gitbook/assets/1606_3.yaml" path="/{version}/sign/interactivePseudonym" method="get" %}
[1606_3.yaml](.gitbook/assets/1606_3.yaml)
{% endswagger %}

#### 8.2.6 User pseudonym API

{% swagger src=".gitbook/assets/1606_3.yaml" path="/{version}/token/pseodonym/{pseudonym}" method="get" %}
[1606_3.yaml](.gitbook/assets/1606_3.yaml)
{% endswagger %}

#### 8.2.7 Get signature response

{% swagger src=".gitbook/assets/1606_3.yaml" path="/{version}/sign/response/{signatureId}" method="get" %}
[1606_3.yaml](.gitbook/assets/1606_3.yaml)
{% endswagger %}

#### 8.2.8 Callback service API

{% swagger src=".gitbook/assets/2306_2.yaml" path="/{version}/esignature/callback" method="get" %}
[2306_2.yaml](.gitbook/assets/2306_2.yaml)
{% endswagger %}

### 8.3 Audit log

{% swagger src=".gitbook/assets/1606_4.yaml" path="/{version}/audit/log" method="get" %}
[1606_4.yaml](.gitbook/assets/1606_4.yaml)
{% endswagger %}

