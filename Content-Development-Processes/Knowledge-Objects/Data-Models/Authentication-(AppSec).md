**Purpose & Considerations** 



**1.	Purpose** 
This document lists out the approved Splunk Data Model fields which is required for making logs Compliance per Common Information model (CIM) as well as Application Security Content Development.

**2. Field Type & their Definition**
<span style="color:green;font-weight:bold">Mandatory Field </span> : Fields which have direct or indirect impact on existing or in-pipeline AppSec contents. Lack of these fields will lead to data non-compliance. We will put forward our best efforts to extract or normalize these fields. Respective BISO’s approval will be required if any of these fields are missing.


 <span style="color:orange;font-weight:bold"> Optional Field </span>: Fields which have NO direct or indirect impact on existing or in-pipeline AppSec contents. We recommend extracting or normalizing these fields if it’s easily available. No BISO’s approval will be required if any of these fields are missing.

**3. Key Points - CIM Normalization**
- Please DO NOT use “unknown”, “NULL”, etc. while extraction for the fields which have not 100% coverage. It MUST be just empty.
- All the mandatory fields which have <100% coverage, MUST be documented with the justification.
- Eventtypes and Tags MUST be built carefully as these two are vital components for datamodel.
- Splunk_SA_CIM MUST be appended with required index(es) as appropriate.

**4.	Authentication**
The fields and tags in the Authentication data model 

| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action	|string	|The action performed on the resource.|Prescribed fields: success, failure. Can be derived from signature or signature_id| success, failure	|
|<span style="color:green;font-weight:bold"> Mandatory Field</span> | app | string | The application involved in the event (such as ssh, splunk, win:local, signin.amazonaws.com).|The application involved in the event|  |
|<span style="color:green;font-weight:bold">Mandatory Field </span>| authentication_method|string |The method used to authenticate the request such as SAML, FIDO, MFA, Kerberos, NTLM, LM, NTLMv2, PSK, Password. | Must be in upper case. |SAML, MFA|
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |authentication_service|string  |The service used to authenticate the request such as Okta, ActiveDirectory, AzureAD. |Must follow industry standard naming convention.| Okta, AD|
|<span style="color:green;font-weight:bold">Mandatory Field </span> | dest|string |The target involved in the authentication. You can alias this from more specific fields, such as dest_host, dest_ip, dest_nt_host.|Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might converting IPv4 to IPv6 in near future.|Must be either IP address or endpoint names. dest host and ip can optionally be captured under “dest_host”and dest_ip fields respectively. |
|<span style="color:orange;font-weight:bold">Optional Field </span>|duration | Number | The amount of time for the completion of the authentication event, in seconds. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|reason | string | The human-readable message associated with the authentication action (success or failure). |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|response_time | string | The hash of the certificate |||
|<span style="color:green;font-weight:bold">Mandatory Field </span>| signature|string |A human-readable signature name. |Must map 1-1 to "signature" field. |UserLoginFailed|
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |signature_id | string |The unique identifier or event code of the event signature. |Must map 1-1 to "signature_id" field. ||
|<span style="color:green;font-weight:bold">Mandatory Field </span> | src|string | The source involved in the authentication. In the case of endpoint protection authentication the src is the client. You can alias this from more specific fields, such as src_host, src_ip, or src_nt_host. Do not confuse src with the event source or sourcetype fields.|Must be and IP address. src_ip can optionally be captured.| “x-forwarded-for” feature must be enabled on the F5 side if source is coming via F5 or equivalent tool.|
|<span style="color:green;font-weight:bold">Mandatory Field </span> | src_user|string | In privilege escalation events, src_user represents the user who initiated the privilege escalation. This field is unnecessary when an escalation has not been performed.| This is only applicable and MUST for privilege escalation events. |Example: skumar19|
|<span style="color:orange;font-weight:bold">Optional Field </span> | src_user_role|string |The role of the user who initiated the privilege escalation. This field is unnecessary when an escalation has not been performed.|||
|<span style="color:orange;font-weight:bold">Optional Field </span> | src_user_type|string |The type of the user who initiated the privilege escalation. This field is unnecessary when an escalation has not been performed.|||
|<span style="color:green;font-weight:bold">Mandatory Field </span> | user|string |The actual string or identifier that a user is logging in with. This is the user involved in the event, or who initiated the event. For authentication privilege escalation events, this must represent the user string or identifier targeted by the escalation.|Username with or without domain. Must be in lower case.|Example: rkumar19|
|<span style="color:green;font-weight:bold">Mandatory Field </span> | user_agent|string |The user agent through which the request was made, such as Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) or aws-cli/2.0.0 Python/3.7.4 Darwin/18.7.0 botocore/2.0.0dev4.|Only applicable for Web-based Authentication and OPTIONAL for others.|Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) |
|<span style="color:orange;font-weight:bold">Optional Field </span> | user_role|string |The role of the user involved in the event, or who initiated the event. For authentication privilege escalation events, this must represent the user role targeted by the escalation.|||
|<span style="color:orange;font-weight:bold">Optional Field </span> | user_type|string |The type of the user involved in the event or who initiated the event, such as IAMUser, Admin, or System. For authentication privilege escalation events, this must represent the user type targeted by the escalation.||Example: IAMUser, Admin, or System|
|<span style="color:orange;font-weight:bold">Optional Field </span> | vendor_account|string |The account that manages the user that initiated the request. This includes the ID of a Cloud account (i.e. a cloud customer) or the ID of the organization.||Cloud account or organization ID.|
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|