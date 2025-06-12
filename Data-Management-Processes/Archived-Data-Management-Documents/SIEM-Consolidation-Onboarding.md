# MF Architecture:
- At least 3 HF/IF per data center in MF
  - 2 utilized for syslog traffic (for masking/mapping capabilities)
  - 1 utilized for custom apps, DBConnect, etc. (pull ingestion)
(Deploy add on, and use credentials) (Preference is to use a Domain Service Account for stuff like DBConnect. 1 account per MF. Service Accounts Tracker for AMER: [AMER Service Accounts for Data Sources.xlsx](https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/_layouts/15/WopiFrame.aspx?sourcedoc={CD177AD6-F6F7-4343-83D0-738588DF1A4C}&file=AMER%20Service%20Accounts%20for%20Data%20Sources.xlsx&action=default)  DO NOT CAPTURE PASSWORD HERE! Passwords maintained in Thycotic)
- Deploy UF packages to MFs using SCCM if they have it. Test connection to our syslog servers and 

# Assign ports for log sources:
  - Port tracker on Sharepoint: (Splunk: Ports Assigned): https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/_layouts/15/xlviewer.aspx?id=/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/Shared%20Documents/30-Build%20Splunk%20Environment/Splunk%20Ports%20Assigned.xlsx&Source=https%3A%2F%2Famericas%2Einternal%2Edeloitteonline%2Ecom%2Fsites%2Fctoteams%2FEnterpriseOperations%2FPlatformDelivery%2Fsplunk%2FSitePages%2FHome%2Easpx%3FRootFolder%3D%252Fsites%252Fctoteams%252FEnterpriseOperations%252FPlatformDelivery%252Fsplunk%252FShared%2520Documents%252F30%252DBuild%2520Splunk%2520Environment%26FolderCTID%3D0x012000AECBCD2BC82623459329C6A3B4413DD7%26View%3D%257BD7D7F96B%252DDD57%252D47DD%252D81FE%252DC9BA105533F1%257D
  - Port number should remain the same for similar logs for all member firms. 
  - Increment port number by 1 for new port. Though TCP and UDP can have same ports for 2 separate sources, do not reuse port number already assigned

# Implementing Firewall rules:
- Raise request through one of the approved FCR requestors
Link for Firewall rule request: [Firewall Mgmt - Manual Firewall policy change requests (FPCR) - Global Technology Services Self-Service](https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=97038ff31bbd71d0f40b40c1b24bcb9e)
- Active FCRs: https://deloitteglobal.service-now.com/nav_to.do?uri=%2Fsc_req_item_list.do%3Fsysparm_query%3D%26sysparm_first_row%3D1%26sysparm_view%3D 
- Template:
- Verify Firewall rules with the Firewall team. Make sure that the exact rule you need has been implemented by the FW team 

# Data On-boarding:
_All these steps were deprecated due now all on-boardings are managed by Data Management team, here his DL, DT - Cyber Defense Engineering - Data Management <dt-cyberdefenseengineering-datamanagement@deloitte.com>_
- New log source type:
  - Create FIPS for new Log Sources: FIPS Directory: https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/Shared%20Documents/Forms/AllItems.aspx?RootFolder=%2Fsites%2Fctoteams%2FEnterpriseOperations%2FPlatformDelivery%2Fsplunk%2FShared%20Documents%2F40%2DDevice%20feed%20integration&FolderCTID=0x012000AECBCD2BC82623459329C6A3B4413DD7&View=%7BF040D9DD%2D9649%2D4613%2D8BD9%2D17345525F2C1%7D
  - Create data flow diagrams for new data sources: https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/_layouts/15/WopiFrame.aspx?sourcedoc=/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/Shared%20Documents/20-Design%20Splunk%20Environment/Splunk%20Data%20Flow%20Options%20-%20Global.pptx&action=default
- Existing log source type:
  - If an existing log source type is being bought in for a new member firm, make sure that all fields are extracted and normalize exactly as they are done in the other member firms already on-boarded
- Log source to change in the future:
  - If we know that a particular log source is going to change or a tool is going to be switched to another tool (eg. We are currently ingesting SNOW Canada and in the future Global SNOW is going to consolidate all CMDBs, OR if a MF is currently using McAfee and will be moving to Cylance in the future), determine the approximate date of the change.
  - Create a work item for the Run team to re-engage the MF around that time frame to work towards ingesting the new logs/deprecating current logs. 
- Log source from different version of tool/appliance/service/application:
  - If MFs are using different version of the tools for a same log source type, make sure that the source types for the logs that are coming in are same as the other versions. If not, add the version/sourcetype specific extractions and normalizations to props.conf
- Data On-boarding checklist: Make sure that you follow these steps and and complete the checklist on the data on-boarding work item in DevOps
https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/88/Data-Onboarding-Process-Requirements

# Update the following documents:
- DNS Alias Tracker: https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/_layouts/15/WopiFrame2.aspx?sourcedoc=%2Fsites%2Fctoteams%2FEnterpriseOperations%2FPlatformDelivery%2Fsplunk%2FShared%20Documents%2F30%2DBuild%20Splunk%20Environment%2FAMER%20Environment%2FDNS%20Alias%20%2D%20AMER%2Exlsx&action=edit
- MF HF/IF Build Details: https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/_layouts/15/WopiFrame2.aspx?sourcedoc=%2Fsites%2Fctoteams%2FEnterpriseOperations%2FPlatformDelivery%2Fsplunk%2FShared%20Documents%2F30-Build%20Splunk%20Environment%2FAMER%20Environment%2FSIEM%20Buildout%20details%20-%20AMER%2Exlsx&action=edit
- Deloitte Indexes Details/Formats: https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/_layouts/15/xlviewer.aspx?id=/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/Shared%20Documents/30-Build%20Splunk%20Environment/Deloitte%20Indexes%2011-21.xlsx&Source=https%3A%2F%2Famericas%2Einternal%2Edeloitteonline%2Ecom%2Fsites%2Fctoteams%2FEnterpriseOperations%2FPlatformDelivery%2Fsplunk%2FSitePages%2FHome%2Easpx%3FRootFolder%3D%252Fsites%252Fctoteams%252FEnterpriseOperations%252FPlatformDelivery%252Fsplunk%252FShared%2520Documents%252F30%252DBuild%2520Splunk%2520Environment%26FolderCTID%3D0x012000AECBCD2BC82623459329C6A3B4413DD7%26View%3D%257BD7D7F96B%252DDD57%252D47DD%252D81FE%252DC9BA105533F1%257D
