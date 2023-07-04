# 8 Service APIs

A Set of microservices are defined to receive requests from other GovStack-compatible Building Blocks and third party Services with relevant inputs and return processed results from key digital functionalities of this Building Block. This section provides a reference for APIs that should be implemented by this Building Block. The APIs defined here establish a blueprint for how the Building Block will interact with other Building Blocks or third party Services. Additional APIs may be implemented by the Building Block, but the listed APIs define a minimal set of functionality that should be provided by any implementation of this Building Block.

eSignature Building Block must expose its microservices through RESTful API interfaces as defined by OpenAPI v3+ standards.  A summary of the APIS exposed by this Building Block is summarized in the table below.&#x20;

### 8.1 eSignature with one time certificate

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml" path="/{version}/sign/onetime" method="post" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml)
{% endswagger %}

### 8.2 eSignature with user's device (SCD)

#### 8.2.1 Certificate creation

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml" path="/{version}/cert/create" method="post" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml)
{% endswagger %}

#### 8.2.2 List certificates

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml" path="/{version}/cert/list" method="get" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml)
{% endswagger %}

#### 8.2.3 Update certificate

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml" path="/{version}/cert/{certificateId}" method="patch" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml)
{% endswagger %}

#### 8.2.4 eSignature with user's device

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml" path="/{version}/sign/pseudonym" method="post" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml)
{% endswagger %}

#### 8.2.5 Webservice to enter user pseudonym

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml" path="/{version}/sign/interactivePseudonym" method="get" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml)
{% endswagger %}

#### 8.2.6 User pseudonym API

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml" path="/{version}/token/pseodonym/{pseudonym}" method="get" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml)
{% endswagger %}

#### 8.2.7 Get signature response

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml" path="/{version}/sign/response/{signatureId}" method="get" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml)
{% endswagger %}

#### 8.2.8 Callback service API

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml" path="/{version}/esignature/callback" method="get" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml)
{% endswagger %}

### 8.3 Audit log

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml" path="/{version}/audit/log" method="get" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-esignature/main/api/swagger.yaml)
{% endswagger %}

