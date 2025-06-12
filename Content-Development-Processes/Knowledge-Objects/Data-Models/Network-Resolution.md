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

**4.	Network Resolution**
The fields and tags in the Network Resolution data model 



| Priority | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
| <span style="color:orange;font-weight:bold"> Optional Field </span> | additional_answer_count | numeric | Number of entries in the "additional" section of the DNS message. | OPTIONAL |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | answer | string | Resolved address for the query | Required <br><br>Could be IPv4 or IPv6 |
| <span style="color:orange;font-weight:bold"> Optional Field </span> | answer_count | numeric | Number of entries in the answer section of the DNS message <br> Event will have only one IP with TTL (Time to Live) | OPTIONAL |
| <span style="color:orange;font-weight:bold"> Optional Field </span> | authority_answer_count | numeric | Number of entries in the 'authority' section of the DNS message. <br> Event will have only one IP with TTL (Time to Live | OPTIONAL |
| <span style="color:green;font-weight:bold"> Mandatory Field </span> | dest | string | The destination of the network resolution event. You can alias this from more specific fields, such as dest_host, dest_ip, or dest_name | 10.92.30.42 |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | dest_port | numeric | The destinatio port number | 9998 |
| <span style="color:orange;font-weight:bold"> Optional Field </span> | duration | numeric | The time taken by the network resolution event, in seconds | OPTIONAL |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | message_type | string | Type of DNS Message | Query <br> Response |
| <span style="color:orange;font-weight:bold"> Optional Field </span> | name | string | The name of the DNS event | OPTIONAL |
| <span style="color:orange;font-weight:bold">Optional Field </span> | query_count | numeric | Number of entries that appear in the "Questions" section of the DNS query. | OPTIONAL |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | query | string | The domain which needs to be resolved. Applies to messages of type "Query". | | Must be in lowercase |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | query_type | string | The field may contain DNS OpCodes or Resource Record Type codes. For details, see the Domain Name System Parameters on the Internet Assigned Numbers Authority (IANA) web site. If a value is not set, the DNS.record_type field is referenced | | Query <br> IQuery<br>Status<br>Status<br>Update |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | record_type | string | The DNS resource record type. For details, see the List of DNS record types on the Wikipedia web site | | DNAME <br> MX <br> NS <br> PTR |
| <span style="color:orange;font-weight:bold"> Optional Field </span> | reply_code | string | The return code for the response. For details, see the Domain Name System Parameters on the Internet Assigned Numbers Authority (IANA) web site <br><br> NoError<br>FormErr<br>NotImp<br>NotZone | OPTIONAL |
| <span style="color:orange;font-weight:bold">Optional Field </span> | reply_code_id | numeric | The numerical id of a return code. For details, see the Domain Name System Parameters on the Internet Assigned Numbers Authority (IANA) web site <br><br>0 - NoError<br>1 - FormErr<br>2 - ServFail<br>3 - NXDomain| OPTIONAL |
| <span style="color:orange;font-weight:bold">Optional Field </span> | response_time | numeric | The amount of time it took to receive a response in the network resolution event, in seconds if consistent across all data sources, if applicable. | OPTIONAL |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | src | string | The source of the network resolution event. You can alias this from more specific fields, such as src_host, src_ip, or src_name. | | 10.28.0.32 |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | src_port | numeric | The port number of the source | | 3322 |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | tag | string | This automatically generated field is used to access tags from within datamodels. Do not define extractions for this field when writing add-ons | |
| <span style="color:orange;font-weight:bold"> Optional Field </span> | transaction_id | numeric | The unique numerical transaction id of the network resolution event | OPTIONAL |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | transport | string | The transport protocol used by the network resolution event | | TCP |
| <span style="color:orange;font-weight:bold"> Optional Field </span> | ttl | numeric | The time-to-live of the network resolution event.| OPTIONAL |
| <span style="color:green;font-weight:bold">Mandatory Field </span> | vendor_product | string | The vendor product name of the DNS server. The Splunk platform can derive this field from the fields vendor and product in the raw data, if they exist. |
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|