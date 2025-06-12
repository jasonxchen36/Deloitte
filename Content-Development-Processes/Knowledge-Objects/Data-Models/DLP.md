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

**4.	DLP**
The fields and tags in the DLP data model 


| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
| <span style="color:green;font-weight:bold"> Madatory Field </span> | action | string | The action taken by the DLP device. | Allowed, blocked, modified, alerted, deleted Could be extracted from “dlp_type” to above fields |
|<span style="color:green;font-weight:bold"> Madatory Field </span> | app|string | The application involved in the event.​| The application involved in the event.
|<span style="color:green;font-weight:bold"> Madatory Field </span> | category |string | The category of the DLP event.​| Vendor specific values for “category” field which provides category of the DLP events related to protection for data IN USE, AT REST, & IN Transmission.
|<span style="color:green;font-weight:bold"> Madatory Field </span> | dest |string |The target of the DLP event.| Must be either IP address or endpoint names. dest host and name can optionally be captured under “dest_host” and “dest_name” fields respectively.
|<span style="color:green;font-weight:bold"> Madatory Field </span> | dest_zone |string |The zone of the DLP target.| It could be either of these values: internal, external, DMZ
|<span style="color:green;font-weight:bold"> Madatory Field </span> | dlp_type |string |The type of DLP system that generated the event.| Vendor specific values for “dlp_type” field which provides type of DLP tool covering Cloud DLP, Network DLP, & Endpoint DLP. This will give more information for “action” field on what activity was performed hence the “action” field-values.
|<span style="color:green;font-weight:bold"> Madatory Field </span> | dvc |string |The device that reported the DLP event| Must be either IP address or endpoint names. dest host and name can optionally be captured under “dvc_host” and “dvc_name” fields respectively.
|<span style="color:green;font-weight:bold"> Madatory Field </span> | dvc_zone |string |The zone of the DLP device.| The zone of the DLP device.
|<span style="color:green;font-weight:bold"> Madatory Field </span> | object |string |The name of the affected object.| Vendor specific values for “object” field which provides something happened on what. Example: xyz.pdf
|<span style="color:green;font-weight:bold"> Madatory Field </span> | object_category |string |The category of the affected object.| Category of the object. Could be extracted from “object” field. Example: 1. For “xyz.pdf”, oject_category would be “file”. 2. If DLP tool is detecting some anomaloies pertaining to unauthorized access to database where data is kept stored (Data in rest), object_category would be “database”.
|<span style="color:green;font-weight:bold"> Madatory Field </span> | object_path |string |The path of the affected object.| Example: C://Desktop/Myfolder
|<span style="color:green;font-weight:bold"> Madatory Field </span> | object_path |string |The path of the affected object.| Example: C://Desktop/Myfolder
|<span style="color:green;font-weight:bold"> Madatory Field </span> | severity |string |The severity of the DLP event.| High, Medium, Low, Informational
|<span style="color:green;font-weight:bold"> Madatory Field </span> | severity_id |string |The numeric or vendor specific severity indicator corresponding to the event severity.| 1-High, 2-  Medium, 3- Low, 4- Informational
|<span style="color:green;font-weight:bold"> Madatory Field </span> | signature |string |The name of the DLP event.| Allow Policy - Amazon S3 Block Access - Whatsapp
|<span style="color:green;font-weight:bold"> Madatory Field </span> | signature_id |string |The unique identifier or event code of the event signature.| Vendor provided “signature_id” (could be either numeric or alphanumeric) which maps uniquey to “signature” field.
|<span style="color:green;font-weight:bold"> Madatory Field </span> | src |string |The source of the DLP event.| The source of the network traffic (the client requesting the connection). You can alias this from more specific fields, such as src_host, src_ip, or src_name
|<span style="color:green;font-weight:bold"> Madatory Field </span> | src_user |string |The source user of the DLP event.| Email address for the source entity. The one who is trying to send something out or upload into the drive. Example: firstname_lastname@deloitte.com
|<span style="color:green;font-weight:bold"> Madatory Field </span> | src_zone |string |The zone of the DLP source.| The network zone of the source
|<span style="color:green;font-weight:bold"> Madatory Field </span> | tag |string |This automatically generated field is used to access tags from within datamodels. Do not define extractions for this field when writing add-ons.| Must be Splunk CIM tag which can call “tstats”
|<span style="color:green;font-weight:bold"> Madatory Field </span> | user |string |The target user of the DLP event.| Email address for the target entity. The one who is expected to receive some information. Example: firstname_lastname@gmail.com
|<span style="color:green;font-weight:bold"> Madatory Field </span> | vendor_product |string |The vendor and product name of the DLP system.| Industry standard naming convention for “vendor_product”.Example” Netskpe CASB, Symantec CABS
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US

