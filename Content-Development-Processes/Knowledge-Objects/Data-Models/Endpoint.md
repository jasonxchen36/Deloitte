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

**4.Endpoint**
The fields and tags in the Endpoint data model 

     Ports


| **Priority** | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|creation_time|timestamp	|The time at which the network port started listening on the endpoint.|Must be standard timestamp in GMT.|10/3/22 8:23:42.000 AM |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest|string	|Expression: if(isnull(dest) OR dest=\"\",\"unknown\",dest)|The destination of port where it is listening. |10.92.30.42 |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest_port	|number|	Network port listening on the endpoint, such as 53.|Must be Numeric.| 53| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|process_guid|string	|The globally unique identifier of the process assigned by the vendor_product.|OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process_id	|number|The numeric identifier of the process assigned by the operating system.|Must be Numeric.| 14817| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src|string	|The "remote" system connected to the listening port (if applicable). Expression: if(isnull(src) OR src=\"\",\"unknown\",src)|The remote system ip or name connected to port.|10.92.30.42 |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src_port|string	|The "remote" port connected to the listening port (if applicable).Expression: if(isnum(src_port),src_port,0)|Must be Numeric.|9514 |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|state|string	|The status of the listening port, such as established, listening, etc.|Must be in upper case.|LISTENING, ESTABLISHED, etc. |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|tag|string	|This automatically generated field is used to access tags from within data models. Add-on builders do not need to populate it.|Must be "port" and "listening" as per the event.|port, listening|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|transport|string	|The network transport protocol associated with the listening port, such as tcp, udp, etc."|Must be in upper case.|TCP, UDP|
|<span style="color:orange;font-weight:bold">Optional Field </span>|transport_dest_port|string	|Calculated as transport/dest_port, such as tcp/53.|OPTIONAL| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user|string	|The user account associated with the listening port.Expression: if(isnull(user) OR user=\"\",\"unknown\",user)|username without domain. Must be in lower case.|rkumar|

     Processes

| **Priority** | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action|string	|The action taken by the endpoint, such as allowed, blocked, deferred.|Must be allowed, blocked, deferred in small case.|blocked|
|<span style="color:orange;font-weight:bold">Optional Field </span>|cpu_load_percent|number	|CPU load consumed by the process (in percent).|OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest|string	|The endpoint for which the process was spawned.Expression: if(isnull(dest) OR dest=\"\",\"unknown\",dest)|The endpoint destination where process was spawned.|10.92.30.42	|
|<span style="color:orange;font-weight:bold">Optional Field </span>|mem_used|number	|Memory used by the process (in bytes).|OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|original_file_name|string	|Original name of the file, not including path. Sometimes this field is similar to process name but the two do not always match, such as process_name=pwsh and original_file_name=powershell.exe to detect renamed instances of any process executing.|Original name of the file, not including path.|powershell.exe|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|os|string	|The operating system of the resource, such as Microsoft Windows Server 2008r2.|MUST be Industry standard OS name.|Microsoft Windows Server 2008r2.|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|parent_process|string	|The full command string of the parent process.Expression: if(isnull(parent_process) OR parent_process=\"\",\"unknown\", parent_process)|Must be full command.|C:\Users\powershell.exe|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|parent_process_exec|string	|The executable name of the parent process.|Must be just executable name.|powershell.exe|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|parent_process_exec|string	|The executable name of the parent process.|Must be just executable name.|powershell.exe|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|parent_process_id|number	|The numeric identifier of the parent process assigned by the operating system.|Must be just Numeric|14871|
|<span style="color:orange;font-weight:bold">Optional Field </span>|parent_process_guid|string	|The globally unique identifier of the parent process assigned by the vendor_product.|OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|parent_process_name|string	|The friendly name of the parent process, such as notepad.exe. Expression: case(isnotnull(parent_process_name) AND parent_process_name!=\"\",parent_process_name, isnotnull(parent_process) AND parent_process!=\"\",replace(parent_process, \"^\\s*([^\\s]+).*\",\"\\1\"),1=1,\"unknown\")"|The friendly name of the process.|java|
|<span style="color:orange;font-weight:bold">Optional Field </span>|parent_process_path|string	|The file path of the parent process, such as C:\Windows\System32\notepad.exe.|OPTIONAL| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process|string	|The full command string of the spawned process. Such as C:\\WINDOWS\\system32\\cmd.exe \/c \"\"C:\\Program Files\\SplunkUniversalForwarder\\etc\\system\\bin\\powershell.cmd\" --scheme\"". There is a limit of 2048 characters.Expression: if(isnull(process) OR process=\"\",\"unknown\",process)|Must be full command.| C:\Users\bob\notepad.exe|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process_current_directory|string	|The current working directory used to spawn the process.|Must be directory from where process was spwaned.| C:\Users\bob|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process_exec|string	|The executable name of the process, such as notepad.exe. Sometimes this is similar to process_name, such as notepad. However in malicious scenarios, such as Fruitfly, the process_exec is Perl while the process_name is Java.|Must be just executable name.|  notepad.exe|
|<span style="color:orange;font-weight:bold">Optional Field </span>|process_hash|string	|The digests of the parent process, such as <md5>, <sha1>, etc.|OPTIONAL| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|process_guid|string	|The globally unique identifier of the process assigned by the vendor_product.|OPTIONAL| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process_id|string	|The numeric identifier of the process assigned by the operating system.|Must be Numeric.|  14817|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process_integrity_level|string	|The Windows integrity level of the process.|Must be either one of them, applicable for Windows|  1system, high, medium, low, untrusted|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process_name|string	|The friendly name of the process, such as notepad.exe. Sometimes this is similar to process_exec, such as notepad.exe. However in malicious scenarios, such as Fruitfly, the process_exec is Perl while the process_name is Java.Expression: case(isnotnull(process_name) AND process_name!=\"\",process_name,isnotnull (process) AND process!=\"\",replace(process,\"^\\s*([^\\s]+).*\",\"\\1\"),1=1,\"unknown\")|  The friendly name of the process.|java|
|<span style="color:orange;font-weight:bold">Optional Field </span>|process_path|string	|The file path of the process, such as C:\Windows\System32\notepad.exe.|OPTIONAL| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|tag|string	|This automatically generated field is used to access tags from within data models. Add-on builders do not need to populate it.|Must be "process" and "report" as per the event.| process,report|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user|string	|The user account that spawned the process.Expression: if(isnull(user) OR user=\"\",\"unknown\",user)|username without domain. Must be in lower case.| rkumar|
|<span style="color:orange;font-weight:bold">Optional Field </span>|user_id|string	|The unique identifier of the user account which spawned the process.|OPTIONAL| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendore_product|string	|The vendor and product name of the Endpoint solution that reported the event, such as Carbon Black Cb Response. This field can be automatically populated by vendor and product fields in your data."Expression: case(isnotnull(vendor_product),vendor_product, isnotnull(vendor) AND vendor!=\"unknown\" AND isnotnull(product) AND product!=\"unknown\",vendor.\" \".product,isnotnull(vendor) AND vendor!=\"unknown\" AND (isnull(product) OR product=\"unknown\"),vendor.\" unknown\",(isnull(vendor) OR vendor=\"unknown\") AND isnotnull(product) AND product!=\"unknown\",\"unknown \".product,isnotnull(sourcetype),sourcetype, 1=1,\"unknown\")|MUST be string.MUST be industry standard naming style.| Carbob Black|

     Services

| **Priority** | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:orange;font-weight:bold">Optional Field </span>|description|string	|The description of the service.|OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest|string	|TThe endpoint for which the service is installed.Expression: if(isnull(dest) OR dest=\"\",\"unknown\",dest)|The endpoint destination of service |10.92.30.42	|
|<span style="color:orange;font-weight:bold">Optional Field </span>|process_guid|string	|The globally unique identifier of the process assigned by the vendor_product.|OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process_id|string	|The numeric identifier of the process assigned by the operating system.|Must be numeric|14817|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|service|string	|The full service name.Expression: if(isnull(service) OR service=\"\",\"unknown\",service)|as per raw|wscsvc|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|service_dll|string	|TThe dynamic link library associated with the service.|Applicable for Windows.||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|service_dll_path|string	|The file path to the dynamic link library assocatied with the service, such as C:\Windows\System32\comdlg32.dll.|Applicable for Windows.|C:\Windows\System32\comdlg32.dll.|
|<span style="color:orange;font-weight:bold">Optional Field </span>|service_dll_hash|string	|The digests of the dynamic link library associated with the service, such as <md5>, <sha1>, etc.|OPTIONAL| | 
|<span style="color:orange;font-weight:bold">Optional Field </span>|service_dll_signature_exists|string	|Whether or not the dynamic link library associated with the service has a digitally signed signature.|OPTIONAL| | 
|<span style="color:orange;font-weight:bold">Optional Field </span>|service_dll_signature_verified|string	|Whether or not the dynamic link library associated with the service has had its digitally signed signature verified.|OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|service_exec|string	|The executable name of the service.|svchost.exe|svchost.exe|
|<span style="color:orange;font-weight:bold">Optional Field </span>|service_hash|string	|The digest(s) of the service, such as <md5>, <sha1>, etc.|OPTIONAL| |
|<span style="color:orange;font-weight:bold">Optional Field </span>|service_id|string	|The unique identifier of the service assigned by the operating system.Expression: if(isnull(service_id) OR service_id=\"\",\"unknown\",service_id)|OPTIONAL| |
|<span style="color:orange;font-weight:bold">Optional Field </span>|service_name|string	|The friendly service name.Expression: if(isnull(service_name) OR service_name=\"\",\"unknown\",service_name)|OPTIONAL| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|service_path|string	|The file path of the service, such as C:\WINDOWS\system32\svchost.exe.|Complete path of the service.|C:\WINDOWS\System32\svchost.exe|
|<span style="color:orange;font-weight:bold">Optional Field </span>|service_signature_exists|boolean	|Whether or not the service has a digitally signed signature.|OPTIONAL| |
|<span style="color:orange;font-weight:bold">Optional Field </span>|service_signature_verified|boolean	|Whether or not the service has had its digitally signed signature verified.|OPTIONAL| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|start_mode|string	|The start mode for the service.Expression: if(isnull(start_mode) OR start_mode=\"\",\"unknown\",start_mode)|MUST be either of the below in lower case:|disabled, manual, auto|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|status|string	|The status of the service.Expression: if(isnull(dest) OR dest=\"\",\"unknown\",dest)|MUST be either of the below in lower case|critical, started, stopped, warning|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|tag|string	|This automatically generated field is used to access tags from within data models. Add-on builders do not need to populate it|Must be "service" and "report" as per the event.|service, report|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user|string	|The user account associated with the service.Expression: if(isnull(user) OR user=\"\",\"unknown\",user)|username without domain. Must be in lower case.|skumar|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product|string	|The vendor and product name of the Endpoint solution that reported the event, such as Carbon Black Cb Response. This field can be automatically populated by vendor and product fields in your data.Expression: case(isnotnull(vendor_product),vendor_product, isnotnull(vendor) AND vendor!=\"unknown\" AND isnotnull(product) AND product!=\"unknown\",vendor.\" \".product,isnotnull(vendor) AND vendor!=\"unknown\" AND (isnull(product) OR product=\"unknown\"),vendor.\" unknown\",(isnull(vendor) OR vendor=\"unknown\") AND isnotnull(product) AND product!=\"unknown\",\"unknown \".product,isnotnull(sourcetype),sourcetype, 1=1,\"unknown\")|Must be string.MUST be industry standard naming style.|Carbon Black|

     Filesystem

| **Priority** | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action|string	|The action performed on the resource.Expression: if(isnull(action) OR action=\"\",\"unknown\",action)|MUST Be CRUD in small case - created, read, updated, deleted.|created	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest|string	|The endpoint pertaining to the filesystem activity.Expression: if(isnull(dest) OR dest=\"\",\"unknown\",dest)|The endpoint destination where filesystem activity found.|10.92.30.42	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_access_time|timestamp	|The time that the file (the object of the event) was accessed.|Must be standard timestamp in GMT. |10/3/22 8:19:42.000 AM	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_access_time|timestamp	|The time that the file (the object of the event) was created.|Must be standard timestamp in GMT. |10/3/22 8:19:42.000 AM	|
|<span style="color:orange;font-weight:bold">Optional Field </span>|file_hash|string	|A cryptographic identifier assigned to the file object affected by the event.Expression: if(isnull(file_hash) OR file_hash=\"\",\"unknown\",file_hash)|OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_modify_time|timestamp	|The time that the file (the object of the event) was altered.|Must be standard timestamp in GMT. |10/3/22 8:19:42.000 AM	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_name|string	|The name of the file, such as notepad.exe.Expression: if(isnull(file_name) OR file_name=\"\",\"unknown\",file_name|Name of the file wihtout path. |notepad.exe	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_path|string	|The path of the file, such as C:\Windows\System32\notepad.exe.Expression: if(isnull(file_path) OR file_path=\"\",\"unknown\",file_path)|Complete path of the file with file name.|C:\Windows\System32\notepad.exe.|
|<span style="color:orange;font-weight:bold">Optional Field </span>|file_acl|string	|Access controls associated with the file affected by the event.Expression: if(isnull(file_acl) OR file_acl=\"\",\"unknown\",file_acl)|OPTIONAL| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_size|string	|The size of the file that is the object of the event, in kilobytes.Expression: if(isnum(file_size),file_size,null())|Must be Numeric in Kilobytes. |14	|
|<span style="color:orange;font-weight:bold">Optional Field </span>|process_guid|string	|The globally unique identifier of the process assigned by the vendor_product.|OPTIONAL| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process_id|string	|The numeric identifier of the process assigned by the operating system.|Must be Numeric in Kilobytes. |14187	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|tag|string	|This automatically generated field is used to access tags from within data models. Add-on builders do not need to populate it.|Must be "endpoint" and "filesystem". |endpoint, filesystem	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user|string	|The user account associated with the filesystem access.Expression: if(isnull(user) OR user=\"\",\"unknown\",user)|username without domain. Must be in lower case.|skumar	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product|string	|The vendor and product name of the Endpoint solution that reported the event, such as Carbon Black Cb Response. This field can be automatically populated by vendor and product fields in your data.Expression: case(isnotnull(vendor_product),vendor_product, isnotnull(vendor) AND vendor!=\"unknown\" AND isnotnull(product) AND product!=\"unknown\",vendor.\" \".product,isnotnull(vendor) AND vendor!=\"unknown\" AND (isnull(product) OR product=\"unknown\"),vendor.\" unknown\",(isnull(vendor) OR vendor=\"unknown\") AND isnotnull(product) AND product!=\"unknown\",\"unknown \".product,isnotnull(sourcetype),sourcetype, 1=1,\"unknown\")|Must be string.MUST be industry standard naming style.|Carbon Black|

     Registry

| **Priority** | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action|string	|The action performed on the resource.Expression: if(isnull(action) OR action=\"\",\"unknown\",action)|MUST Be CRUD in small case - created, read, updated, deleted.|created	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest|string	|The endpoint pertaining to the filesystem activity.Expression: if(isnull(dest) OR dest=\"\",\"unknown\",dest)|The endpoint destination of registry|10.92.30.42	|
|<span style="color:orange;font-weight:bold">Optional Field </span>|process_guid|string	|The globally unique identifier of the process assigned by the vendor_product.|OPTIONAL| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process_id|string	|The numeric identifier of the process assigned by the operating system.|Must be Numeric in Kilobytes. |14187
|<span style="color:green;font-weight:bold">Mandatory Field </span>|registry_hive|string	|The logical grouping of registry keys, subkeys, and values.|Must be what we have in raw:|HKEY_CURRENT_CONFIG, HKEY_CURRENT_USER, HKEY_LOCAL_MACHINE\\SAM, HKEY_LOCAL_MACHINE\\Security, HKEY_LOCAL_MACHINE\\Software, HKEY_LOCAL_MACHINE\\System, HKEY_USERS\\.DEFAULT	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|registry_path|string	|The path to the registry value, such as \win\directory\directory2\{676235CD-B656-42D5-B737-49856E97D072}\PrinterDriverData.Expression: if(isnull(registry_path) OR registry_path=\"\",\"unknown\",registry_path)|Complete path of the registry.| \win\directory\directory2\{676235CD-B656-42D5-B737-49856E97D072}\PrinterDriverData.|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|registry_key_name|string	|The name of the registry key, such as PrinterDriverData.Expression: if(isnull(registry_key_name) OR registry_key_name=\"\",\"unknown\", registry_key_name)|Name of the registry as given in the raw.|PrinterDriverData	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|registry_value_data|string	|The unaltered registry value.Expression: if(isnull(registry_value_data) OR registry_value_data=\"\",\"unknown\", registry_value_data)|Must be what we have in raw:|	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|registry_value_name|string	|The name of the registry value.Expression: if(isnull(registry_value_name) OR registry_value_name=\"\",\"unknown\", registry_value_name)|Must be what we have in raw:|	|
|<span style="color:orange;font-weight:bold">Optional Field </span>|registry_value_text|string	|The textual representation of registry_value_data (if applicable).|OPTIONAL| |
|<span style="color:orange;font-weight:bold">Optional Field </span>|registry_value_type|string	|The type of registry value. Expression: if(isnull(registry_value_type) OR registry_value_type=\"\",\"unknown\", registry_value_type)|OPTIONAL| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|status|string	|The status of the service.Expression: if(isnull(dest) OR dest=\"\",\"unknown\",dest)|MUST be either of the below in lower case|critical, started, stopped, warning|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|tag|string	|This automatically generated field is used to access tags from within data models. Add-on builders do not need to populate it.|Must be "endpoint" and "registry". |endpoint, registry	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user|string	|The user account associated with the filesystem access.Expression: if(isnull(user) OR user=\"\",\"unknown\",user)|username without domain. Must be in lower case.|skumar	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product|string	|The vendor and product name of the Endpoint solution that reported the event, such as Carbon Black Cb Response. This field can be automatically populated by vendor and product fields in your data.Expression: case(isnotnull(vendor_product),vendor_product, isnotnull(vendor) AND vendor!=\"unknown\" AND isnotnull(product) AND product!=\"unknown\",vendor.\" \".product,isnotnull(vendor) AND vendor!=\"unknown\" AND (isnull(product) OR product=\"unknown\"),vendor.\" unknown\",(isnull(vendor) OR vendor=\"unknown\") AND isnotnull(product) AND product!=\"unknown\",\"unknown \".product,isnotnull(sourcetype),sourcetype, 1=1,\"unknown\")|Must be string.MUST be industry standard naming style.|Carbon Black|
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|












