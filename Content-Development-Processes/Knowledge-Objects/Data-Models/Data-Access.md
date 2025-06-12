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

**4.	Data Access**
The fields and tags in the Data Access data model 

| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action |string|The data access action taken by the user..|MUST be written as per the industry standard prescribed values:      `commented`, `copied`, `created`, `deleted`, `disabled`, `downloaded`, `enabled`, `granted`, `forwarded`, `modified`, `read`, `revoked`, `shared`, `stopped`, `uncommented`, `unlocked`, `unshared`, `updated`, `uploaded`| 	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|app |string|The application involved in the event.| MUST be written as per the industry standard 	|
|<span style="color:orange;font-weight:bold">Optional Field </span>|app_id  | string | Application ID as defined by the vendor|  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest |string|The destination where the data resides or where it is being accessed, such as the product or application. You can alias this from more specific fields not included in this data model, such as `dest_host`, `dest_ip`, `dest_url`, or `dest_name`.| Must be a IP address if IP is available to fetch. Else, dest would be treated as identity for destination or remote host. Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might convert IPv4 to IPv6 in near future. 	|
|<span style="color:orange;font-weight:bold">Optional Field </span>|dest_name  | string | Name of the destination as defined by the vendor.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|dest_url  | string | Url of the product, application, or object.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|dvc  | string | The device that reported the data access event.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|email  | string | The email address of the user involved in the event, or who initiated the event.|  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|object |string|Resource object name on which the action was performed by a user| 	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|object_attrs |string|The object's attributes and their values. The attributes and values can be those that are updated on a resource object, or those that are not updated but are essential attributes.| 	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|object_category |string|Generic name for the class of the updated resource object. Expected values may be specific to an app. For example, `collaboration`, `file`, `folder`, `comment`, `task`, `note`, and so on.| 	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|object_id |string|The unique updated resource object ID as presented to the system, if applicable. For example, a source_folder_id, doc_id. |	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|object_path  | string | The path of the modified resource object, if applicable, such as a file, directory, or volume.|  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|object_size |string|The size of the modified resource object. |	|
|<span style="color:orange;font-weight:bold">Optional Field </span>|owner  | string | Resource owner ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|owner_email  | string | Email of the resource owner.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|owner_id  | string | ID of the owner as defined by the vendor.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|parent_object  | string | Parent of the object name on which the action was performed by a user. |  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|parent_object_id  | string | Parent object ID|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|parent_object_category  | string | Object category of the parent object on which action was performed by a user.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|signature  | string |A human-readable signature name. |  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|signature_id  | string | The unique identifier or event code of the event signature.|  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src |string|The endpoint client host.|Must be a IP address if IP is available to fetch. Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might convert IPv4 to IPv6 in near future	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_account |string|Account associated with the event. The account represents the organization, or a Cloud customer or a Cloud account.|	|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user |string|The user involved in the event, or who initiated the event. | should be able to extract out the username without the domain or extraneous character|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user_agent |string|The user agent through which the request was made, such as Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) or aws-cli/2.0.0 Python/3.7.4 Darwin/18.7.0 botocore/2.0.0dev4|	|
|<span style="color:orange;font-weight:bold">Optional Field </span>|user_group  | string | The group of the user involved in the event, or who initiated the event.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|user_id  | string |The unique id of the user involved in the event. For authentication privilege escalation events, this should represent the user targeted by the escalation. | ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user_name |string|The user name of the user or entity performing the change. For account changes, this is the account that was changed (see src_user_name).|Use this field for a friendlier name, for example, with AWS events if you do not have Assets and Identities configured in Enterprise Security and are not getting a friendly name from user.|
|<span style="color:orange;font-weight:bold">Optional Field </span>|user_email  | string |The email address of the user or entity involved in the event.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|user_role  | string | The role of the user involved in the event, or who initiated the event|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|user_type  | string | The type of the user involved in the event or who initiated the event, such as IAMUser, Admin, or System. For account management events, this should represent the type of the user changed by the request.|  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product |string|The vendor and product name of the vendor.| MUST be industry standard naming style.|
|<span style="color:orange;font-weight:bold">Optional Field </span>|vendor_product_id  | string | The vendor and product name ID as defined by the vendor.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|vendor_region  | string | The data center region where the change occurred, such as us-west-2.|  ||
