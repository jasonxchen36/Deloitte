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

**4.	Alerts**
The fields and tags in the Alerts data model 



| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|app	|string	|The system, service, or application that generated the alert event. Examples include, but are not limited to the following: GuardDuty, SecurityCenter, 3rd party services, win:app:trendmicro, vmware, nagios.|MUST be written as per the industry standard | 	GuardDuty|
|<span style="color:orange;font-weight:bold">Optional Field </span>|description  | string | The description of the alert event |  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest	|string	|The object that is the target of the alert event. Examples include an email address, SNMP trap, or virtual machine id. You can alias this from more specific fields, such as dest_host, dest_ip, or dest_name.|Must be a IP address if IP is available to fetch. Else, dest would be treated as identity for destination or remote host. Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might convert IPv4 to IPv6 in near future.	 || 
|<span style="color:orange;font-weight:bold">Optional Field </span>|dest_type  | string | The type of the destination object, such as instance, storage, firewall.|  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|id	|string	|The unique identifier of the alert event.| || 
|<span style="color:orange;font-weight:bold">Optional Field </span>|mitre_technique_id  | string | The MITRE ATT&CK technique ID of the alert event, searchable at https://attack.mitre.org/techniques| This is useful information. Do we have information already there in raw logs? MITRE# should be there by Splunk Alert using ES in near future.||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|severity	|string	|The severity of the alert event. Note: This field is a string. Specific values are required. Use the severity_id field for severity ID fields that are integer data types. Specific values are required. Use vendor_severity for the vendor's own human-readable strings (such as Good, Bad, Really Bad, and so on).|Must be in (critical, high, medium, low, informational, unknown)“vendor_severity” can also be normalized optionally if it is available.| |
|<span style="color:orange;font-weight:bold">Optional Field </span>|severity_id  | string | The numeric or vendor specific severity indicator corresponding to the event severity.| 1, 2, 3, 4, 5 ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|signature|string|The human-friendly title of the alert event, such as 'API GetAccountPasswordPolicy was invoked using root credentials.' Split by signature_id when aggregating alert events by types.|Vendor specific alert title| |
|<span style="color:orange;font-weight:bold">Optional Field </span>|signature_id  | string | The vendor specific policy or rule that generated the alert event, such as 'Policy:IAMUser/RootCredentialUsage.'| ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src|string|The object that is the actor of the alert event. You can alias this from more specific fields, such as src_host, src_ip, or src_name.|Src of actor due to which alert got triggered. Must be a IP address if IP is available to fetch.  Could be either IPv4 or IPv6, lower case for IPv6 Deloitte might convert IPv4 to IPv6 in near future.	| |
|<span style="color:orange;font-weight:bold">Optional Field </span>|src_type  | string | The type of the source object, such as instance, storage, firewall.| ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|tag  | string | This automatically generated field is used to access tags from within data models. Do not define extractions for this field when writing add-ons.|  Same as CIM
|<span style="color:orange;font-weight:bold">Optional Field </span>|type  | string | The alert event type.| ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user  | string | The user involved in the alert event.|should be able to extract out the username without the domain or extraneous characters ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|user_name  | string | The name of the user involved in the alert event.| ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_account  | string | The account associated with the alert event.| ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_region  | string |The data center region involved in the alert event, such as us-west-2.| ||
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|  ||