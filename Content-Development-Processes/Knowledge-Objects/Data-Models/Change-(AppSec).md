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

**4.	Change**
The fields and tags in the Change data model 



| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action	|string	|The action attempted on the resource, regardless of success or failure.|The change action value MUST be one of the CRUD values: created, read, updated, deleted   | 	Example: updated	|
|<span style="color:green;font-weight:bold"> Mandatory Field</span> | change_type | string | The type of change |It must be filesystem, group, user, secrets, etc.| file, folder, authentication, authorization, table, view, procedures, schema | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|command  | string | The command that initiated the change.|API call or web url hit to initiate change. |exec [dbo].[sp_DNAV_OCR_REQUESTS_INPROGRESS_FILES_GET],DROP table emp_table (Azure SQL Database)|
|<span style="color:green;font-weight:bold">Mandatory Field </span>| dest |string |The resource where change occurred. You can alias this from more specific fields not included in this data model, such as dest_host, dest_ip, or dest_name.  | Must be a IP address if IP is available to fetch. Else, dest would be treated as identity for destination or remote host. Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might converting IPv4 to IPv6 in near future.|RD000XXXX1B0C1| 
|<span style="color:orange;font-weight:bold"> Optional Field </span> |dvc | string | The device or application that reported the change.|Must be either IP address or endpoint names. dest host and name can optionally be captured under “dvc_host” and “dvc_name” fields respectively.||
|<span style="color:green;font-weight:bold">Mandatory Field </span> | object |string | Name of the affected object on the resource. |Name of the actual entity found in “change_type”|SQL database (Azure SQL Database), file (Unix filesystem), SAP HANA DB (SAP HANA DB)|
|<span style="color:orange;font-weight:bold"> Optional Field</span> | object_attrs  | string | The attributes that were updated on the updated resource object. || N/A   | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|object_category  | string |Generic name for the class of the updated resource object. |Expected values may be specific to an app, for example: registry, directory, file, group, user, bucket, instance.|SQL database (Azure SQL Database), file (Unix filesystem), SAP HANA DB (SAP HANA DB)|
|<span style="color:orange;font-weight:bold">Optional Field </span>|object_id | string | The unique updated resource object ID as presented to the system.|If the object has an id number use that. Otherwise you can use another unique identifier like a path or attribute. |N/A  |
|<span style="color:green;font-weight:bold">Mandatory Field </span>| object_path |string |The path of the modified resource object ||Example"APP_IPF_WH.DS_PROC_1FA444D4F9D0E08A284A1_CV_RDR"|
|<span style="color:green;font-weight:bold"> Mandatory Field </span> |result | string | The vendor-specific result of a change, or clarification of an action status. |For instance, status=failure may be accompanied by result=blocked by policy or result=disk full. | RPC COMPLETED, BATCH COMPLETED |
|<span style="color:orange;font-weight:bold">Optional Field </span> | result_id|string | A result indicator for an action status |ID Should be mapped with result field|N/A |
|<span style="color:green;font-weight:bold">Mandatory Field </span>| src |string |The src involved in the change. Where did the request for change come from? | Must be a IP address if IP is available to fetch. Else, dest would be treated as identity for destination or remote host. Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might converting IPv4 to IPv6 in near future.|“x-forwarded-for” feature must be enabled on the F5 side if source is coming via F5 or equivalent tool. Example: 10.XXX.XX.20|
<span style="color:green;font-weight:bold">Mandatory Field </span>|status | string |was the change successful or not |binary success or failure |Example: success|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user | string |The user or entity performing the change.  |should be able to extract out the username with or without the domain or extraneous characters  |Example: rkumar19 |
|<span style="color:green;font-weight:bold">Mandatory Field </span> | user_agent |string |The user agent through which the request was made, such as Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) or aws-cli/2.0.0 Python/3.7.4 Darwin/18.7.0 botocore/2.0.0dev4. |Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6)|
|<span style="color:orange;font-weight:bold">Optional Field </span> | user_type |string | The type of the user involved in the event or who initiated the event, such as IAMUser, Admin, or System. For account management events, this should represent the type of the user changed by the request. ||N/A|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src_user | string |For account changes, the user or entity performing the change.  |This is only applicable and MUST for Account Change (Account_Management) events| Example: skumar19 |
|<span style="color:orange;font-weight:bold">Optional Field </span> | src_user_type |string | For account management events, this should represent the type of the user changed by the request. |||
|<span style="color:orange;font-weight:bold">optional Field </span>|vendor_account  | string |The account that manages the user that initiated the request.  |Typically derived via the data onboarding method.|N/A|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product  | string |The vendor and product or service that detected the change. This field can be automatically populated by vendor and product fields in your data. |Typically derived via the data onboarding method.|Example: Microsoft Azure SQL|
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|

