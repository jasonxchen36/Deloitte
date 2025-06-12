**Purpose & Considerations** 



**1.	Purpose** 
This document lists out the approved Splunk Data Model fields which is required for making logs Compliance per Common Information model (CIM) as well as Infrastructure/Cloud Security Content Development.

**2. Field Type & their Definition**
<span style="color:green;font-weight:bold">Mandatory Field </span> : Fields which have direct or indirect impact on existing or in-pipeline InfraSec or CloudSec contents. Lack of these fields will lead to data non-compliance. We will put forward our best efforts to extract or normalize these fields. Respective BISO’s approval will be required if any of these fields are missing.


 <span style="color:orange;font-weight:bold"> Optional Field </span>: Fields which have NO direct or indirect impact on existing or in-pipeline InfraSec or CloudSec contents. We recommend extracting or normalizing these fields if it’s easily available. No BISO’s approval will be required if any of these fields are missing.

**3. Key Points - CIM Normalization**
- Please DO NOT use “unknown”, “NULL”, etc. while extraction for the fields which have not 100% coverage. It MUST be just empty.
- All the mandatory fields which have <100% coverage, MUST be documented with the justification.
- Eventtypes and Tags MUST be built carefully as these two are vital components for datamodel.
- Splunk_SA_CIM MUST be appended with required index(es) as appropriate.

**4.	Certificates**
The fields and tags in the Certificates data model 



| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest	|string	|The target host/machine in certificate management event|10.0.62.32 2001:0db8:85a3:0000:0000:8a2e:0370:7334 | 		|
|<span style="color:green;font-weight:bold"> Mandatory Field</span> | dest_port | number | The port number of the target host/machine|Numeric port# such as 80, 43, etc|  |
|<span style="color:orange;font-weight:bold">Optional Field </span>|duration | number | The amount of time for the completion of the certificate management event, in seconds. ||Optional|
|<span style="color:green;font-weight:bold">Mandatory Field </span>| src|string |The source involved in the certificate management event. You can alias this from more specific fields, such as src_host, src_ip, or src_nt_host. | Must be a IP address if IP is available to fetch. Else, dest would be treated as identity for destination or remote host. Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might converting IPv4 to IPv6 in near future.|
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |src_port | number |The port number of the source. |Numeric port# Could be custom|
|<span style="color:green;font-weight:bold">Mandatory Field </span> | transport|string | The transport protocol of the Network Traffic involved with this certificate.|Upper case such as TCP/IP, UDP| |
|<span style="color:green;font-weight:bold"> Mandatory Field</span> | ssl_end_time | string | The expiry time of the certificate. Needs to be converted to UNIX time for calculations in dashboards.|Needs to be converted to UNIX time|  |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|ssl_engine | string | The name of the signature engine that created the certificate. |||Optional|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|ssl_hash | string | The hash of the certificate |||Optional|
|<span style="color:green;font-weight:bold">Mandatory Field </span>| ssl_is_valid|string |Indicator of whether the ssl certificate is valid or not. | True, false|
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |ssl_issuer | string |The certificate issuer's RFC2253 Distinguished Name. |DN Name as available in the raw data|
|<span style="color:green;font-weight:bold">Mandatory Field </span> | ssl_issuer_common_name|string | The certificate issuer's common name.|CN Name as available in the raw data| |
|<span style="color:green;font-weight:bold">Mandatory Field </span> | ssl_issuer_email|string | The certificate issuer's email address.|Email address of SSL Issuer available in the log| |
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_issuer_email_domain | string | The domain name contained within the certificate issuer's email address. |||Optional|
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_issuer_locality | string | The certificate issuer's locality. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_issuer_organization | string | The certificate issuer's organization. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_issuer_state | string | The certificate issuer's state of residence. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_issuer_street | string | The certificate issuer's street address. |||
|<span style="color:green;font-weight:bold">Mandatory Field </span> | ssl_name|string |The name of the ssl certificate.|As available in the raw data| 
|<span style="color:green;font-weight:bold">Mandatory Field </span> | ssl_policies|string |The Object Identification Numbers's of the certificate's policies in a comma separated string.| | |TBD|
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_publickey | string | The certificate's public key. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_publickey_algorithm | string | The algorithm used to create the public key. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_serial| string |The certificate's serial number. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_session_id | string | The session identifier for this certificate.|||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_signature_algorithm | string | The algorithm used by the Certificate Authority to sign the certificate.|||
|<span style="color:green;font-weight:bold">Mandatory Field </span> | ssl_start_time|string |This is the start date and time for this certificate's validity. Needs to be converted to UNIX time for calculations in dashboards.|Needs to be converted to UNIX time| 
|<span style="color:green;font-weight:bold">Mandatory Field </span> | ssl_subject|string |The certificate owner's RFC2253 Distinguished Name.|DN of certificate owner available in the raw| 
|<span style="color:green;font-weight:bold">Mandatory Field </span> | ssl_subject_common_name|string |This certificate owner's common name.|CN of certificate owner available in the raw| 
|<span style="color:green;font-weight:bold">Mandatory Field </span> | ssl_subject_email|string |The certificate owner's e-mail address.|Email address of SSL Issuer available in the log| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_subject_email_domain | string | The domain name contained within the certificate subject's email address. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_subject_locality | string | The certificate owner's locality. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_subject_organization | string | The certificate owner's organization. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_subject_state | string | The certificate owner's state of residence|||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_subject_street | string | The certificate owner's street address. |||
|<span style="color:orange;font-weight:bold">Optional Field </span>|ssl_subject_unit | string | The certificate owner's organizational unit. |||
|<span style="color:green;font-weight:bold">Mandatory Field </span> | ssl_validity_window|string |The length of time (in seconds) for which this certificate is valid.|Can be eval using substraction of “ssl_end_time” and “ssl_start_time”| 
|<span style="color:green;font-weight:bold">Mandatory Field </span> | ssl_version|string |The ssl version of this certificate.|Version of SSL/TLS|
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US| 