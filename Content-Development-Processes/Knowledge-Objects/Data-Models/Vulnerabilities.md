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

**4.Vulnerabilities**
The fields and tags in the Vulnerabilities data model 


| **Priority** | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:orange;font-weight:bold">Optional Field </span>|bugtraq|string	|Corresponds to an identifier in the vulnerability database provided by the Security Focus website (searchable at http://www.securityfocus.com/).|OPTIONAL Bugtrq database has not decommissioned.| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|Category	|string	The category of the discovered vulnerability, such as DoS.|DoS, Security Misconfiguration, Broken Authentication, etc| DoS, Security Misconfiguration, Broken Authentication, etc| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|cert|string	|MUST be inline with DB provided by US-CERT.|Corresponds to an identifier provided in the Common Vulnerabilities and Exposures index (searchable at http://cve.mitre.org).| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|cve|string	|Corresponds to an identifier provided in the Common Vulnerabilities and Exposures index (searchable at http://cve.mitre.org).|MUST be inline with Common Vulnerabilities and Exposures index  | CVE-2022-34169| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|cvss|number	|Numeric indicator of the common vulnerability scoring system.|Must be numeric. CVSS Score  <li>Qualitative = Rating </li> <li> 0.0  =  None</li><li> 0.1 – 3.9  =  Low </li><li>4.0 – 6.9  =  Medium</li><li>7.0 – 8.9  =  High</li><li>9.0 – 10.0  =  Critical </li> | 8.9|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest|string	|The host with the discovered vulnerability. You can alias this from more specific fields, such as dest_host, dest_ip, or dest_name.|Must be either IP address or endpoint names. dest host and name can optionally be captured under “dest_host” and “dest_name” fields respectively.|10.21.23.4|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dvc|string	|The system that discovered the vulnerability. You can alias this from more specific fields, such as dvc_host, dvc_ip, or dvc_name.|Must be either IP address or endpoint names. dest host and name can optionally be captured under “dvc_host” and “dvc_name” fields respectively. |10.23.29.2| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|msft|string	|Corresponds to a Microsoft Security Advisory number (http://technet.microsoft.com/en-us/security/advisory/).|MUST be inline with Microsoft Security Advisory number| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|mskb|string	|Corresponds to a Microsoft Knowledge Base article number (http://support.microsoft.com/kb/).|MUST be inline with Microsoft Knowledge Base article number| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|severity|string	|The severity of the network protection event.|Must be one of them: critical, high, medium, low, informational  | high| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|severity_id|string	|The numeric or vendor specific severity indicator corresponding to the event severity.|OPTIONAL|  | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|signature|string	|The name of the vulnerability detected on the host, such as HPSBMU02785 SSRT100526 rev.2 - HP LoadRunner Running on Windows, Remote Execution of Arbitrary Code, Denial of Service (DoS).|Must be String and name of the vulnerability what we have in the raw event. |Remote Execution of Arbitrary Code| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|signature_id|string	|The unique identifier or event code of the event signature.|OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|tag|string	|This automatically generated field is used to access tags from within datamodels. Do not define extractions for this field when writing add-ons.|All event must have "report" and "vulnerability" tags with it. | vulnerability | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|url|string	|The URL involved in the discovered vulnerability.|Must be in URL format (If found in raw, might be less than 100% depending upon the discovery)|https://example.com/redirect?externalPage=3 | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user|string	|The user involved in the discovered vulnerability.|username without domain. Must be in lower case.|rkumar| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product|string	|The vendor and product that detected the vulnerability. This field can be automatically populated by vendor and product fields in your data.|Must be same what we have in raw.|5501461002 | 
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|
