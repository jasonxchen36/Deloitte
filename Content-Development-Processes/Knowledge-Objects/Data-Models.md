
**[Overview of Content in Volume Testing and Production that leverages Data Model Searches](https://dev.azure.com/GlobalSOC/Splunk/_dashboards/dashboard/380c0658-c2eb-460a-839b-c627b222e9ee)**


**How to Write a Data Model Search:**
Things you need to include:
- |tstats pipe that includes \`summariesonly\` macro, fields that are needed in the form ofvalues(<Data Model>.field),  _time field in some sense i.e latest(_time), earliest(_time) or _time span=<time>, and a groupby clause that includes the index field
- | convert ctime(_time) in order to get your time field to a readable format
- The last pipe of your search query should be a | fields pipe of all the column names you see in your results
- it is best to refine your search results in your | tstats pipe after the where clause as it improves efficiency

| tstats template:

| tstats \`summariesonly\` count values(<Data Model>.fields) values(sourcetype) from datamodel=<Data Model> where (nodename=Node_<Data Model>)(<Data Model>.field=<refining clause>) groupby index <Data Model>.field, _time span=<time>

Example Query:
| tstats \`summariesonly\` count values(All_Changes.result_id) values(All_Changes.user) values(All_Changes.action) values(All_Changes.src) values(All_Changes.change_type) from datamodel=Change where (nodename = All_Changes) (All_Changes.result_id=4739) (All_Changes.action=success) (All_Changes.change_type="Lockout Policy modified") groupby index All_Changes.user _time span=1s
| rename values(All_Changes.*) to *
| convert ctime(_time)
| fields index _time user src result_id action change_type
 

**Data Models:**

**[Authentication](https://docs.splunk.com/Documentation/CIM/4.14.0/User/Authentication)** 

_The Authentication Data Model fields describe login activities from any data source._ 

Log Sources: WinEventLog:Application, WinEventLog:Security, auth-too_small, cisco:acs, cisco_switch, f5:bigip:apm:syslog, gesgaportal:iiastc, linux_secure, messages, ms:aad:signin, o365:management:activity, opsec:audit, protocol, qualys-cloud-agent-too_small, qualys-cloud-agent.log-2, sendmail_syslog, syslog, thycotic:secretserver

Content Leveraged: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/e1b931cf-97b8-49e7-81b3-5c29fed92fc2/

**[Change ](https://docs.splunk.com/Documentation/CIM/4.14.0/User/change)**

_The Change Data Model fields describe create, read, update, and delete activities from any data source._ 

Log Sources: WinEventLog:Security, WinEventLog:System, linux_audit, WinEventLog:AD FS/Admin, WinEventLog:Application, linux_audit, ms:aad:audit, o365:management:activity, opsec:audit, thycotic:secretserver, syslog, XmlWinEventLog:MSExchange Management

Content Leveraged: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/2726a211-212f-4f32-b839-c9f51975d3cf/

**[Data Loss Prevention (DLP)](https://docs.splunk.com/Documentation/CIM/4.14.0/User/DataLossPrevention)**

_The Data Loss Prevention Data Model fields describe events gathered from DLP tools used to identify, monitor and protect data._

Log Sources: netskope:alert, netskope:application, symantiec:dlp:oracle

Content Leveraged: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/ff74845e-887f-4645-9b8a-7d58dac214f2/

**[Email](https://docs.splunk.com/Documentation/CIM/4.14.0/User/email)**

_The Email Data Model fields describe email traffic whether server:server and client:server._

Log Sources: cisco:esa:summary, cisco:esa:textmail

Content Leveraged: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/ff4eb64b-f509-4354-9d94-d2fa632ba989/

**[Intrusion Detection](https://docs.splunk.com/Documentation/CIM/4.14.0/User/IntrusionDetection)**

_The Intrusion Detection Data Model (IDS) fields describe attack detection events by network monitoring devices and apps._

Log Sources: cisco:estreamer:data, cisco:stealthwatch:alert, cp_smartdefense, eEstreamer, fe_json, fe_xml_syslog, opsec:anti_malware, opsec:anti_virus, opsec:smartdefense, symantec:ep:mobile:syslog

Content Leveraged: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/ff4eb64b-f509-4354-9d94-d2fa632ba989/

**[Malware](https://docs.splunk.com/Documentation/CIM/4.14.0/User/malware)**

_The Malware Data Model fields describe malware protection and endpoint protection management._

Log Sources: mcafee:epo, symantec:ep:mobile:syslog, *cylance*

Content Leveraged: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/c87e87c6-c9c4-4d39-8265-3b5a89d36eef/

**[Network Resolution (DNS)](https://docs.splunk.com/Documentation/CIM/4.14.0/User/NetworkResolutionDNS)**

_The Network Resolution (DNS) Data Model fields describe DNS traffic, both server:server and client:server._

Log Sources:opendns:dnslogs, stream:dns

Content Leveraged: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/76a60c22-c967-4792-a99d-5d3d1f6740d7/ 

**[Network Sessions](https://docs.splunk.com/Documentation/CIM/4.14.0/User/NetworkSessions)**

_The Network Sessions Data Model fields describe Dynamic Host Configuration Protocol (DHCP) and VPN Traffic, whether server:server or client:server and network infrastructure inventory and topology._

Log Source: DhcpSrvLog, cp_vpn, f5:bigip:apm:syslog, f5:bigip:syslog, opsec:vpn

Content Leveraged: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/06ac9a2c-08b4-40a8-96ac-b18926e3534f/

**[Network Traffic](https://docs.splunk.com/Documentation/CIM/4.14.0/User/NetworkTraffic)**

_The Network Traffic Data Model fields describe flows of data across network infrastructure components._

Log Sources: cisco:estreamer:data, cisco:ios, cp_fw, opsec:vpn, pan:traffic, stream:dns, stream:http, stream:ip, stream:tcp, stream:udp

Content Leveraged: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/b0cce5aa-7925-4dba-beb5-8be0d8d8d791/

**[Web](https://docs.splunk.com/Documentation/CIM/4.14.0/User/Web)**
 _The Web Data Model fields describe web server and/or proxy server data in a security or operational context._

Log Sources: cp_web, f5:bigip:proxy, gesgaportal:iis, mcafee:wg:kv, opsec, stream:http, symantec:websecurityserver:scwss-poll

Content Leveraged: https://dev.azure.com/GlobalSOC/Splunk/_queries/query-edit/1410854b-2b74-4cad-928c-87e6be375df6/