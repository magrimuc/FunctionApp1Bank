# FunctionApp1Bank

The Berlin Group - a european standards initiative
made a PSD2 compliant XS2A Interface
describing a NextGenPSD2 XS2A Framework

It covers 
* PISP - payment information (Payment Initiation Service Provider)
* AISP - account information (Account Information Service Provider)
* PIISP - confirmation of funds


This specification uses on a pure protocol level the following HTTP header in all HTTP requests uniformously for the support of the signature function:
Request Header 
Attribute  //  Type  //  Condition  //  Description
Digest //  String  //  Conditional  //  Is contained if and only if the "Signature" element is contained in the header of the request.
Signature  //  cp. Section 12  //  Conditional  //  A signature of the request by the TPP on application level. This might be mandated by ASPSP.
TPP-Signature-Certificate  //  String  //  Conditional  //  The certificate used for signing the request, in base64 encoding. Must be contained if a signature is contained, see above.

For a better readability, the definition of these headers is not repeated throughout this specification. If no other condition describes otherwise, then the definitions here apply to all requests.

Remark: An ASPSP will ignore signatures on application level used by the TPP if signatures are not supported by the ASPSP.
4.3 Optional Usage of OAuth2 for PSU Authentication or Authorisation
The XS2A API will allow an ASPSP to implement OAuth2 as a support for the authorisation of the PSU towards the TPP for the payment initiation and/or account information service. 
In this case, the TPP will be the client, the PSU the resource owner and the ASPSP will be the resource server in the abstract OAuth2 model.
This specification supports two ways of integrating OAuth2. The first support is an authentication of a PSU in a pre-step, translating this authentication into an access token to be used at the XS2A interface afterwards. 
This usage of OAuth2 will be referred to in this specification as "if OAuth2 has been used as PSU authentication". 
Further details shall be defined in the documentation of the ASPSP of this XS2A interface.
The second option to integrate OAuth2 is an integration as an OAuth2 SCA Approach to be used for authorisation of payment initiations and consents. 
In both services, PIS and AIS, OAuth2 will in this option be used in an integrated way, by using the following steps:

However this will never ever going to be near 10% completed. Sad.

4.4 XS2A Interface API Structure
The XS2A Interface is resource oriented. Resources can be addressed under the API endpoints
https://{provider}/v1/{service}{?query-parameters}


4.6 Authorisation Endpoints
The NextGenPSD2 API is supporting dedicated authorisation endpoints for payment initiation transactions and establish consent transactions in order to handle transaction authorisation by PSUs. These authorisation endpoints are supported from version 1.2 of this specification for supporting the following new features in a common structured way
* multiple level SCA, where a transaction needs an authorisation by more than one PSU, e.g. in a corporate context,
* signing of a group of transactions with one SCA, as it is offered by ASPSPs today in online banking,
* signing of a group of transactions with multi-level SCA, where this group of transactions need an authorisation by more than one PSU, e.g. in a corporate context.
To support this, the resources resulting from the submission of payment data or consent data are separated from authorisation (sub-)resources. A payment which needs to be signed n times then will end up in a payment resource with n SCA (sub-)resources in a normal successful process.
