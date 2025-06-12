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

**4.	Web**
The fields and tags in the Change data model 



| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action	|string	|The action taken by the server or proxy.|Must be either allowed, blocked, informational, redirected, client error, server error in lower case.    | 	Example: allowed	|
|<span style="color:green;font-weight:bold"> Mandatory Field</span> | app | string | The application detected or hosted by the server |Name of the application for which web traffic is being generated. Must be in Deloitte <region>/<mf> <fss> <app-name> format.| Example: Deloitte US Tax GES GA Portal | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|bytes | number | The total number of bytes transferred.|Must be numeric and without unit, which can be either integer or decimal, it's bytes by default.|Example: 4009|
|<span style="color:green;font-weight:bold">Mandatory Field </span>| bytes_in |number |The number of inbound bytes transferred.  | Must be numeric and without unit, which can be either integer or decimal, it's bytes by default.|Example: 2009| 
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |bytes_out | number | The number of outbound bytes transferred.|Must be numeric and without unit, which can be either integer or decimal, it's bytes by default.|Example: 2000|
|<span style="color:green;font-weight:bold">Mandatory Field </span> | dest |string | The destination of the network traffic (the remote host). |Must be either IP address or host/server names. dest host and ip can optionally be captured under “dest_host”, and dest_ip” fields respectively.|Example: 10.0.1.2, ushdc8712|
|<span style="color:green;font-weight:bold"> Mandatory Field</span> | dest_port  | number | The destination port of the web traffic. |Generally, port 80 is used for HTTP, and port 443 is used for HTTPS protocol. | Example: 8000  | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|http_method  | string |The HTTP method used in the request. |Must be in upper case.|Example: GET|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|http_user_agent| string | The user agent used in the request.|Must be as it is what we have in the raw logs. |Example: Mozilla/5.0+(Windows+NT+10.0;+Win64;+x64)+AppleWebKit/537.36+(KHTML,+like+Gecko)|
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |http_user_agent_length | number | The length of the user agent used in the request. |Calculated field derived from "http_user_agent" field. Must be numeric and without unit, it's number of characters. | Example: 118 |
|<span style="color:orange;font-weight:bold">Optional Field </span> | cookie|string | The cookie file recorded in the event.|N/A |
|<span style="color:green;font-weight:bold">Mandatory Field </span>| src |string |The source of the network traffic (the client requesting the connection). |Must be and IP address. |“x-forwarded-for” feature must be enabled on the F5 side if source is coming via F5 or equivalent tool. Example: 10.XXX.XX.20|
<span style="color:green;font-weight:bold">Mandatory Field </span>|status | string |The HTTP response code indicating the status of the proxy request. |Must be numeric and a valid HTTP response code. |Example: success|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user | string |The user that requested the HTTP resource.  |username with or without domain. Must be in lower case.  |Example: rkumar19 |
|<span style="color:green;font-weight:bold">Mandatory Field </span> | uri_path |string |The path of the resource served by the webserver or proxy. |Must be as it is what we have in row logs.|Example: /AppPortal/Deloitte/Deloitte
|<span style="color:green;font-weight:bold">Mandatory Field </span> | uri_query |string | The path of the resource requested by the client |Must be as it is what we have in row logs.|Example: ?v=tHVOMjlhlHhqlIyGgIviC8CUiEDEzl1I_p1XJQzDzSw1|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|url | string |The URL of the requested HTTP resource.  |Must be as it is what we have in the row logs| Example: https://app.deloitte.com/AppPortal/Deloitte/Deloittev=tHVOMjlhlHhqlIyGgIviC8CUiEDEzl1I_p1XJQzDzSw1|
|<span style="color:green;font-weight:bold">Mandatory Field </span> | url_domain|string | The domain name contained within the URL of the requested HTTP resource. |Must be in lower case.|Example: deloitte.com|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|url_length  | number |The length of the URL.  |Calculated field derived from "url" field. Must be numeric and without unit, it's number of characters.|Example: 54|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product  | string |The vendor and product or service that detected the change. This field can be automatically populated by vendor and product fields in your data. |Typically derived via the data onboarding method.|Example: Microsoft Azure SQL|
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|