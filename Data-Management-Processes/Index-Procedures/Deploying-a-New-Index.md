For the deployment of new indexes into the environment a procedure of updating the [Index_Mapping.csv](https://usatramekj100.atrame.deloitte.com:8000/en-US/app/lookup_editor/lookup_edit?owner=nobody&namespace=DA-ESS-Americas-Lookups&lookup=Index_Mapping.csv&type=csv) will be required.  

This lookup [Index_Mapping.csv](https://usatramekj100.atrame.deloitte.com:8000/en-US/app/lookup_editor/lookup_edit?owner=nobody&namespace=DA-ESS-Americas-Lookups&lookup=Index_Mapping.csv&type=csv) is part of the [Index Mapping dashboard](https://usatramekj100.atrame.deloitte.com:8000/en-US/app/SplunkEnterpriseSecuritySuite/Index_Mapping). Part of the [New Data Source On Boarding Process](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/171/New-Data-Source-On-boarding) will be updating the lookup information pertaining to an index **before** its connected to the environment. It can be edited through the lookup editor found **below** between our two environments. Use your admin credentials while adding entries. Please note that the two environments are mutually exclusive between certain indexes. Please do not hesitate to reach out with any questions. 

[SHC_AMER](https://usatramekj100.atrame.deloitte.com:8000/en-US/app/lookup_editor/lookup_edit?owner=nobody&namespace=DA-ESS-Americas-Lookups&lookup=Index_Mapping.csv&type=csv)

[SHC_EMEA](https://eu1436l012.atrame.deloitte.com:8000/en-US/app/lookup_editor/lookup_edit?owner=nobody&namespace=DA-ESS-EMEA-Lookups&lookup=Index_Mapping.csv&type=csv)

As an example, 

**Index**: amer_network_cisco_stealthwatch
**Region**: Americas
**Member Firm**: amer
**DataCategory**: Network logs
**DataSource**: Stealthwatch
**Vendor**: Cisco
**Product**: Cisco Stealthwatch
**App**: TA-cisco-stealthwatch
**Ingest Method:** Heavy Forwarder
**DMC Alerts:** Yes
**Comments:**
**Live**: Yes


|  Index| Region | Member Firm | DataCategory | DataSource | Vendor | Product | App | Ingest Method | DMC Alert | Comments | Live
|--|--|--|--|--|--|--|--|--|--|--|--|
| amer_network_cisco_stealthwatch |Americas  | amer | Network logs | Stealthwatch | Cisco  | Cisco Stealthwatch | TA-cisco-stealthwatch | Heavy Forwarder | Yes |  | Yes


