
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

**4.	Email**
The fields and tags in the Email data model 


| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action	|string	|Action taken by the reporting device.|It MUST be: delivered, blocked, quarantined, deleted|recommended: delivered, blocked, quarantined, deleted| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|delay  | Number | Total sending delay in milliseconds. |  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest	|string	|The endpoint system to which the message was delivered. You can alias this from more specific fields, such as dest_host, dest_ip, or dest_name.|MUST be written as per the industry standard	|derived from where log is collected.	| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|duration  | Number | The amount of time for the completion of the messaging event, in seconds. |  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_hash	|string	|The hashes for the files attached to the message, if any exist.|Same as what we have in the raw|148dddb522b126f3f918f5f77e61cee48153c6b57c643c877fcc6003e8e33ded| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_name	|string	|The names of the files attached to the message, if any exist.|Same as what we have in the raw|image001.png| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|file_size	|string	|The size of the files attached the message, in bytes.|It MUST be numeric in bytes.|20 bytes| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|internal_message_id  | Number | Host-specific unique message identifier. |  | Other: Such as aid in sendmail, IMI in Domino, Internal-Message-ID in Exchange, and MID in Ironport.|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|message_id	|string	|The globally-unique message identifier.|Same as what we have in the raw.|9FB1AF09-1709-4554-A1D7-44ABDE167A45@awsmail.easyvista.net|
|<span style="color:orange;font-weight:bold">Optional Field </span>|message_info  | string | Additional information about the message. |  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|orig_dest	|string	|The original destination host of the message. The message destination host can change when a message is relayed or bounced.|Same as dest format when a message is relayed or bounced.|| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|orig_recipient	|string	|The original recipient of the message. The message recipient can change when the original email address is an alias and has to be resolved to the actual recipient.|Must be in standard email addresses, the message recipient can change when the original email address is an alias and has to be resolved to the actual recipient.|| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|orig_src	|string	|The original source of the message.|Same as src format, if available||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process	|string	|The name of the email executable that carries out the message transaction.|Same as what we have in the raw, if we have a process involved in email|other: sendmail, postfix, or the name of an email client|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|process_id	|Number	|The numeric identifier of the process invoked to send the message.|Must be numeric, if we have a process involved in email|| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|protocol	|string	|The email protocol involved, such as SMTP or RPC.|Must be in upper case. Ex: SMTP|prescribed values: smtp, imap, pop3, mapi| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|recipient	|string	|A field listing individual recipient email addresses.|must be in Statdard email address format. Ex: bob@deloitte.com| Other: recipient="foo@splunk.com", recipient="bar@splunk.com"| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|recipient_count	|Number	|The total number of intended message recipients.|Must be in numeric, Calculated field for recipient. Ex: 5|| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|recipient_domain	|string	|The domain name contained within the recipient email addresses.|Must be domain name. Calculated field for recipient. Ex: deloitte.com||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|recipient_status|string	|The recipient delivery status, if available.|Must be either success or failure and mapped (1-1) with "status_code"|| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|response_time  | Number | The amount of time it took to receive a response in the messaging event, in seconds.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|retries  | Number | The number of times that the message was automatically resent because it was bounced back, or a similar transmission error condition.|  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|return_addr|string|The return address for the message.|Standard email address|| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|size  | Number | The size of the message, in bytes.|  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src|string|The system that sent the message. You can alias this from more specific fields, such as src_host, src_ip, or src_name.|Src of actor due to which alert got triggered.	| 199.91.136.26
 | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src_user|string|The email address of the message sender.|Standard email address	| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src_user_domain|string|The domain name contained within the email address of the message sender.|Must be domain name. Calculated field for src_user. Ex: deloitte.com| GTSCTOCloudEmailServices@deloitte.com | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|status_code|string|The status code associated with the message.|Must be numeric value what we have in the raw and mapped (1-1) with "recipient_status"| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|subject|string|The subject of the message.|Same as what we have in raw|'7 ways recognition impacts business success' |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|tag|string|This automatically generated field is used to access tags from within data models. Do not define extractions for this field when writing add-ons.|email > All events content, filter, delivery per event types| email,delivery,content,filter |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|url|string|The URL associated with the message, if any.|Same as what we have in the raw, if avaiable| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user|string|The user context for the process. This is not the email address for the sender. For that, look at the src_user field.|This is not the email address for the sender.| |
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product|string|The vendor and product of the email server used for the email transaction. This field can be automatically populated by vendor and product fields in your data.|Must be as per the industry naming Convention. Ex: IronPort (Cisco ESA)|Cisco - ESA (IronPort)| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|xdelay  | string | Extended delay information for the message transaction. May contain details of all the delays from all the servers in the message transmission chain.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|xref  | string | An external reference. Can contain message IDs or recipient addresses from related messages.|  ||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|filter_action|string|The status produced by the filter.|Same as what we have in raw. Must be within: accepted, rejected, dropped|accepted, rejected, dropped|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|filter_score|Number|Numeric indicator assigned to specific emails by an email filter.|Must be numeric. Ex: 4.5||
|<span style="color:green;font-weight:bold">Mandatory Field </span>|signature|string|The name of the filter applied.|Same as what we have in raw. Ex: Anti-virus email||
|<span style="color:orange;font-weight:bold">Optional Field </span>|signature_extra  | string | Any additional information about the filter.|  ||
|<span style="color:orange;font-weight:bold">Optional Field </span>|signature_id  | string | The id associated with the filter name.|  ||