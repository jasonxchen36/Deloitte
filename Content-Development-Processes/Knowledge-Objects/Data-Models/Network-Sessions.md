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

**4.Network Sessions**
The fields and tags in the Network Sessions data model 
| **Priority** | **Field** | **Data Type** | **Description** | **Expectation** | **Example** | 
|--|--|--|--|--|--|
|<span style="color:green;font-weight:bold">Mandatory Field </span>|action	|string	|The action taken by the reporting device. The Network Sessions are for VPN and DHCP events.|renewed, released, leased, connected, disconnected|renewed, released, leased, connected, disconnected|
|<span style="color:orange;font-weight:bold">Optional Field </span>|dest_dns|string|The domain name system address of the destination for a network session event.	|OPTIONAL|| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest_ip	|string	|The internal IP address allocated to the client initializing a network session. For DHCP and VPN events, this is the IP address leased to the client.|The internal IP address allocated to the client initializing a network session. For DHCP and VPN events, this is the IP address leased to the client.| 10.12.6.5| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|dest_mac|string	|The internal MAC address of the network session client. For DHCP events, this is the MAC address of the client acquiring an IP address lease. For VPN events, this is the MAC address of the client initializing a network session. Note: Always force lower case on this field. Note: Always use colons instead of dashes, spaces, or no separator. |The internal MAC address of the network session client. For DHCP events, this is the MAC address of the client acquiring an IP address lease. For VPN events, this is the MAC address of the client initializing a network session. Note: Always force lower case on this field. Note: Always use colons instead of dashes, spaces, or no separator.| 00:00:5e:00:53:af|
|<span style="color:orange;font-weight:bold">Optional Field </span>|dest__nt_host|string|The amount of time for the completion of the network session event, in seconds.|OPTIONAL|| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|duration|number|The amount of time it took to receive a response in the network session event, if applicable.|OPTIONAL|| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|dest_dns|number|The amount of time it took to receive a response in the network session event, if applicable.|OPTIONAL||  
|<span style="color:green;font-weight:bold">Mandatory Field </span>|signature|string	|An indication of the type of network session event.|MUST be in LOWER case from the raw log coming from different vendor. There is no pre-defined list of signature and can be expanded as per vendor logging.| dhcpack, dhcpna, dhcprelease, webvpn| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|signature_id|string	|The unique identifier or event code of the event signature.| OPTIONAL| | 
|<span style="color:orange;font-weight:bold">Optional Field </span>|src_dns|string|The external domain name of the client initializing a network session. Not applicable for DHCP events.| OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src_ip|string	|The IP address of the client initializing a network session. Not applicable for DHCP events.|The IP address of the client initializing a network session. Not applicable for DHCP events. | 10.19.2.3| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|src_mac|string	|The MAC address of the client initializing a network session.Not applicable for DHCP events. Note: Always force lower case on this field. Note: Always use colons instead of dashes, spaces, or no separator.|The MAC address of the client initializing a network session.Not applicable for DHCP events. Note: Always force lower case on this field. Note: Always use colons instead of dashes, spaces, or no separator. | 00:00:5e:00:53:af| 
|<span style="color:orange;font-weight:bold">Optional Field </span>|src_nt_host|string|The NetBIOS name of the client initializing a network session. Not applicable for DHCP events.| OPTIONAL| | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|tag|string	|This automatically generated field is used to access tags from within datamodels. Do not define extractions for this field when writing add-ons.|"network" and "session" are mandatory for all Network Session events. "dhcp" and "vpn" are for DHCP and VPN traffic respectively. Also, for both DHCP and VPN, "start" and "end" MUST be built respectively. | dhcp, vpn, start | 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|user|string	|The user in a network session event, where applicable. For example, a VPN session or an authenticated DHCP event.|username with domain unlike other datamodels|bobr@deloitte.com| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|vendor_product|string	|The full name of the DHCP or DNS server involved in this event, including vendor and product name. For example, Microsoft DHCP or ISC BIND. Create this field by combining the values of the vendor and product fields, if present in the events.|Must be industry standard naming convention.|Microsoft DHCP| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|lease_duration|number	|The duration of the DHCP lease, in seconds.|The duration of the DHCP lease, in seconds.|86400| 
|<span style="color:green;font-weight:bold">Mandatory Field </span>|lease_scope|string	|The consecutive range of possible IP addresses that the DHCP server can lease to clients on a subnet. A lease_scope typically defines a single physical subnet on your network to which DHCP services are offered.|The consecutive range of possible IP addresses that the DHCP server can lease to clients on a subnet. A lease_scope typically defines a single physical subnet on your network to which DHCP services are offered.|10.21.0.0/32| 
<span style="color:green;font-weight:bold">Mandatory Field </span>|work_country | string |Country from where the logs are originating. |Must be in Upper Case. |Example: work_country of the Netskope logs from US in the index= amer_cloud_netskope_casb  would be work_country=US|
