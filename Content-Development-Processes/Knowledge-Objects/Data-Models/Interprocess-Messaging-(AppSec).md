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

**4.	Interprocess Messaging**
The fields and tags in the Change data model 



| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest	|string	|The destination of the message.|Must be either IP address or host/server names   | 	Example: 10.0.1.2, ushdc8712	|
|<span style="color:green;font-weight:bold"> Mandatory Field</span> | duration | number | The number of seconds from message call to message response |Must be numeric without unit. By default, it is in seconds. | Example: 53 | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|endpoint | string | The endpoint that the message accessed during the RPC (remote procedure call) transaction.|Must be as it is what we have in raw logs. |Example: deleteFileafterDownload|
|<span style="color:orange;font-weight:bold">Optional Field </span>| endpoint_version |string |The version of the endpoint accessed during the RPC (remote procedure call) transaction, such as 1.0 or 1.22.  |Must be in lower case alphanumeric.|Example: v1| 
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |message | string | A command or reference that an RPC (remote procedure call) reads or responds to.|Must be full path or command.|Example: /api/v1/deleteFileafterDownload|
|<span style="color:green;font-weight:bold">Mandatory Field </span> | message_type |string | The type of message, such as call or reply. |Must be call or reply in lower case.|Example: call|
|<span style="color:green;font-weight:bold"> Mandatory Field</span> | parameters  | string| Arguments that have been passed to an endpoint by a REST call or something similar.|Must be in lower case.  | Example: method=trash  | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|payload | string |The message payload. |Shouldn't be content of the payload and just the file name or similar.|Example: listofdeletion.txt|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|payload_type| string | The type of payload in the message.|Calculated field derived from "payload" field. It's file extension or similar of payload. |Example: txt|
|<span style="color:green;font-weight:bold">Mandatory Field </span>| response_code |string |The response status code sent by the receiving server. Ranges between 200 and 404|Must be in numeric and between ranges between 200 and 404.|Example: 200|
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |rpc_protocol | string| The protocol that the message server uses for remote procedure calls |Must be in upper case.  | Example: HTTP REST, SOAP|
|<span style="color:orange;font-weight:bold">Optional Field </span> | message_id|string | The message identification.|N/A |
|<span style="color:green;font-weight:bold">Mandatory Field </span>| status |string |The status of the message response. |Must be either pass or fail in lower case. |Example: pass|
<span style="color:green;font-weight:bold">Mandatory Field </span>|status | string |The HTTP response code indicating the status of the proxy request. |Must be numeric and a valid HTTP response code. |Example: success|
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|