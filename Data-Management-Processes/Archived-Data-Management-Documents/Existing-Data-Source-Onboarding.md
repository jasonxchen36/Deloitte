#Onboarding steps for existing data source 

##- Dev Environment:
  - Create regional index in the master index app on the Indexer Cluster Master (ICM)
    - Index Naming Convention: region/mf\_category\_vendor\_product
[Index Naming Convention Documentation](https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/_layouts/15/xlviewer.aspx?id=%2Fsites%2Fctoteams%2FEnterpriseOperations%2FPlatformDelivery%2Fsplunk%2FShared%20Documents%2F30-Build%20Splunk%20Environment%2FDeloitte%20Indexes%2011-21.xlsx&amp;Source=https%3A%2F%2Famericas%2Einternal%2Edeloitteonline%2Ecom%2Fsites%2Fctoteams%2FEnterpriseOperations%2FPlatformDelivery%2Fsplunk%2FSitePages%2FHome%2Easpx%3FRootFolder%3D%252Fsites%252Fctoteams%252FEnterpriseOperations%252FPlatformDelivery%252Fsplunk%252FShared%2520Documents%252F30%252DBuild%2520Splunk%2520Environment%26FolderCTID%3D0x012000AECBCD2BC82623459329C6A3B4413DD7%26View%3D%257BD7D7F96B%252DDD57%252D47DD%252D81FE%252DC9BA105533F1%257D)
    - Use existing sourcetypes / default sourcetypes from Splunkbase app
  - Push the new index out before going live with any data ingestion (if required)
  - Verify that data is extracted properly by Splunk
  - Verify that timestamps are accurate
  - Determine daily ingestion size
  - Review if log has user full name. If so, take a screenshot and send to your respective lead (Daisy Gallegos, Ryan Wick, or Daniel Azrak) for direction on whether masking is required. 
  - Verify CIM normalization from existing app on SHC (refer to checklist on CIM validation work item in Devops for CIM normalization steps)
    - Add index name to macros.conf in Splunk CIM app
  - Create Distributed Monitoring Console (DMC) health monitoring alert
    - Create by index if only one sourcetype exists in index, else if multiple sourcetypes exist, create by sourcetype
    - Test DMC alert by bringing the feed down
##- Production Environment:
  - Create regional index in the master index app on the Indexer Cluster Master (ICM)
    - Index Naming Convention: region/mf\_category\_vendor\_product
    - Use existing sourcetypes / default sourcetypes from Splunkbase app
  - Push the new index out before going live with any data ingestion (if required)
  - Verify that data is extracted properly by Splunk
  - Verify that timestamps are accurate
  - Verify CIM normalization from existing app on SHC (refer to checklist on CIM validation work item in Devops for CIM normalization steps)
    - Verify CIM normalization with Deloitte Global FC Engineering Content Run Team