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

**4.	Updates**
The fields and tags in the Updates data model 



| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span> |dest | string | The system that is affected by the patch change. You can alias this from more specific fields, such as dest_host, dest_ip, or dest_name.| Must be either IP address or endpoint names. <br/> <br/> dest host and name can optionally be captured under “dest_host” and “dest_name” fields respectively.| USHDC6979 |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | dvc | string | The device that detected the patch event, such as a patching or configuration management server. <br/> You can alias this from more specific fields, such as dvc_host, dvc_ip, or dvc_name. | Must be either IP address or endpoint names. <br/> <br/> dest host and name can optionally be captured under “dvc_host” and “dvc_name” fields respectively. | USHDC3950 |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | file_hash | string | The checksum of the patch package that was installed or attempted. | SHA256 File hash value or equivalent. <br/> <br/>Tip: “FileHash” could be one field where we must look. Not applicable for all the cases. | 17E771B9DA1EAD7F3F92DC8BA48C064D41DD790D69D7D98B44 |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | file_name | string | The name of the patch package that was installed or attempted. | <b>Must be in lower case.<b> | Security Update for Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package (KB2538243) |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | severity | string | The severity associated with the patch event. | prescribed values: <br/>critical, high, medium, low, informational <br/><br/> <b>Must be in lower case.<b> | high |
| <span style="color:orange;font-weight:bold">Optional Field </span> | severity_id | string | The numeric or vendor specific severity indicator corresponding to the event severity. | <b>Optional<b> | |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | signature | string | The name of the patch requirement detected on the client (the dest), such as MS08-067 or RHBA-2013:0739. <br/><br/>Note: This is a string value. Use signature_id for numeric indicators. | Vendor or application specific patch requirement detected on the dest (above fields). | MS11-025 |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | signature_id | integer | The ID of the patch requirement detected on the client (the src).<br/><br/>Note: Use signature for human-readable signature names. | Unique ID for patch requirement detected on the dest, coming from vendor tool or application logging. | 4535680 |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | status | string | Indicates the status of a given patch requirement. | prescribed values: <br/>available, installed, invalid, "restart required" | installed |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | tag | string | This automatically generated field is used to access tags from within datamodels. Do not define extractions for this field when writing add-ons | Must be “update”, “status”, and “error”. | update, status, error |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | vendor_product |string | The vendor and product of the patch monitoring product, such as Lumension Patch Manager. This field can be automatically populated by vendor and product fields in your data. | Must be camel case. We can eval this as well, if not available in the raw logs | Microsoft SCCM Current Branch |
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|
