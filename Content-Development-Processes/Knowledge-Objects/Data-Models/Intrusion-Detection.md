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

**4.Intrusion Detection**
The fields and tags in the Intrusion Detection data model 


| **Priority** | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action	|string	|The action taken by the intrusion detection system (IDS).|Must be either blocked or allowed.|allowed|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|category	|string	|The vendor-provided category of the triggered signature, such as spyware.|Must be as it is what we have in the raw log.| spyware| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest|string	|The destination of the attack detected by the intrusion detection system (IDS). You can alias this from more specific fields not included in this data model, such as dest_host, dest_ip, or dest_name.|Must be a IP address if IP is available to fetch. Else, dest would be treated as identity for destination or remote host. Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might convert IPv4 to IPv6 in near future.| 10.111.4.5|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dvc|string	|The device that detected the intrusion event. You can alias this from more specific fields not included in this data model, such as dvc_host, dvc_ip, or dvc_name.|Must be either IP address or endpoint names. dest host and name can optionally be captured under “dvc_host” and “dvc_name” fields respectively. | 10.24.22.32| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_hash|string	|A cryptographic identifier assigned to the file object affected by the event.|Must be as it is what we have in the raw log.. | |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_name|string	|The name of the file, such as notepad.exe.|Must be as it is what we have in the raw log. | notepad.exe|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_path|string	|The path of the file, such as C:\\Windows\\System32\\notepad.exe.|Must be as it is what we have in the raw log. | C:\\Windows\\System32\\notepad.exe| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|ids_type|string	|The type of IDS that generated the event.|Must be one of them: network, host, application, wireless. | network| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|severity|string	|The severity of the network protection event.|Must be one of them: critical, high, medium, low, informational  | high| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|severity_id|string	|The numeric or vendor specific severity indicator corresponding to the event severity.|| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|signature|string	|The name of the intrusion detected on the client (the src), such as PlugAndPlay_BO and JavaScript_Obfuscation_Fre.|Must be as it is what we have in the raw log. | PlugAndPlay_BO| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|signature_id|string	|The unique identifier or event code of the event signature.|| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src|string	|The source involved in the attack detected by the IDS. You can alias this from more specific fields not included in this data model, such as src_host, src_ip, or src_name.|Must be IP address or endpoint name.Source host and name can optionally be captured under “src_host” and “src_name” fields respectively.Note: “x-forwarded-for” feature must be enabled on the F5 side if source is coming via F5 or equivalent tool. | 10.19.2.3| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src_port|number	|The port number of the source|Must be a numeric value.Do not translate the values of this field to strings (tcp/80 is 80, not tcp)Port# must be extracted separately | 80| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|tag|string	|This automatically generated field is used to access tags from within datamodels. Do not define extractions for this field when writing add-ons.|Must be ids and attack. | | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|transport|string	|The OSI layer 4 (transport) protocol of the intrusion, in lower case.|Standard OSI transport protocol.Must be in upper case|TCP/IP, UDP | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user|string	|The user involved with the intrusion detection event.|username without domain. Must be in lower case.|xyz  Note: username must be able to traced when it comes to incident investigation | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product|string	|The vendor and product name of the IDS or IPS system that detected the vulnerability, such as HP Tipping Point. This field can be automatically populated by vendor and product fields in your data.|Must be string.Could be used industry standard naming style.|SolarWindsP  | 
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|
