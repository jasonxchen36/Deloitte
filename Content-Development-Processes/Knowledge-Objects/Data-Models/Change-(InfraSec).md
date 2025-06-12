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

**4.	Change**
The fields and tags in the Change data model 



| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action	|string	|What action was taken in the change?|The change action value MUST be one of the CRUD values: created, read, updated, deleted   | 	derived from action field 	|
|<span style="color:green;font-weight:bold"> Mandatory Field</span> | Change_type | string | The type of change |It must be filesystem, group, user, secrets, etc.| derived from object  | 
|<span style="color:orange;font-weight:bold">Optional Field </span>|command  | string | The command that initiated the change.|API call or web url hit to initiate change. |N/A |
|<span style="color:green;font-weight:bold">Mandatory Field </span>| dest |string |The resource where change occurred. You can alias this from more specific fields not included in this data model, such as dest_host, dest_ip, or dest_name.  | Must be a IP address if IP is available to fetch. Else, dest would be treated as identity for destination or remote host. Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might converting IPv4 to IPv6 in near future.|derived from where log is collected.| 
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |dvc | string | The device or application that reported the change.|Must be either IP address or endpoint names. dest host and name can optionally be captured under “dvc_host” and “dvc_name” fields respectively.|derived from where log is collected |
|<span style="color:green;font-weight:bold">Mandatory Field </span> | object |string | Name of the affected object on the resource. |Name of the actual entity found in “change_type”|tax_home.xml  |
|<span style="color:orange;font-weight:bold"> Optional Field</span> | object_attrs  | string | The attributes that were updated on the updated resource object. || Not applicable for this log   | 
|<span style="color:orange;font-weight:bold">Optional Field </span>|object_category  | string |Generic name for the class of the updated resource object. ||isdir  |
|<span style="color:orange;font-weight:bold">Optional Field </span>|object_id | string | The unique updated resource object ID as presented to the system.|If the object has an id number use that. Otherwise you can use another unique identifier like a path or attribute. |derived from path |
|<span style="color:green;font-weight:bold">Mandatory Field </span>| object_path |string |The path of the modified resource object ||path|
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |result | string | The vendor-specific result of a change, or clarification of an action status. |For instance, status=failure may be accompanied by result=blocked by policy or result=disk full. | N/A |
|<span style="color:orange;font-weight:bold">Optional Field </span> | result_id|string | A result indicator for an action status |ID Should be mapped with result field|N/A |
|<span style="color:green;font-weight:bold">Mandatory Field </span>| src |string |The src involved in the change. Where did the request for change come from? | Must be a IP address if IP is available to fetch. Else, dest would be treated as identity for destination or remote host. Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might converting IPv4 to IPv6 in near future.|derived from host .|All|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|status | string |was the change successful or not |binary success or failure |derived from log generaion  |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user | string |The user or entity performing the change.  |should be able to extract out the username without the domain or extraneous characters  |user  |
|<span style="color:orange;font-weight:bold">Optional Field </span> | user_agent |string |The user agent through which the request was made, such as Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) or aws-cli/2.0.0 Python/3.7.4 Darwin/18.7.0 botocore/2.0.0dev4. ||
|<span style="color:orange;font-weight:bold">Optional Field </span> | user_type |string | The type of the user involved in the event or who initiated the event, such as IAMUser, Admin, or System. For account management events, this should represent the type of the user changed by the request. |||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src_user | string |For account changes, the user or entity performing the change.  ||  |
|<span style="color:orange;font-weight:bold">Optional Field </span> | src_user_type |string | For account management events, this should represent the type of the user changed by the request. |||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_account  | string |The account that manages the user that initiated the request.  |Typically derived via the data onboarding method.||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product  | string |The vendor and product or service that detected the change. This field can be automatically populated by vendor and product fields in your data. |Typically derived via the data onboarding method.||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_region  | string |The data center region where the change occurred, such as us-west-2. |Typically derived via the data onboarding method.||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|image_id  | string |For create instance events, this field represents the image ID used for creating the instance such as the OS, applications, installed libraries, and more. |||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|instance_type  | string |For create instance events, this field represents the type of instance to build such as the combination of CPU, memory, storage, and network capacity.  |||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest_ip_range   | string |For network change events, the outgoing traffic for a specific destination IP address range. Specify a single IP address or an IP address range in CIDR notation.  ||For example, 203.0.113.5 or 203.0.113.5/32.|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest_port_range    | string |For network change events, this field represents destination port or range.  ||For example, 80 or 8000 - 8080 or 80,443.|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|direction    | string |For network change events, this field represents whether the traffic is inbound or outbound.  |||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|protocol    | string |For network change events, this field represents the protocol for the network event rule.  |||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|rule_action     | string |For network change events, this field represents whether to allow or deny traffic.   |||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src_ip_range      | string |For network change events, this field represents the incoming traffic from a specific source IP address or range. Specify a single IP address or an IP address range in CIDR notation. ||For example, 203.0.113.5 or 203.0.113.5/32. |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src_port_range      | string |For network change events, this field represents source port or range.   ||For example, 80 or 8000 - 8080 or 80,443.|
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|

