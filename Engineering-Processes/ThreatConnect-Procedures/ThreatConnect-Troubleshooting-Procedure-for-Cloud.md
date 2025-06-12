**This Wiki Article has been updated with troubleshooting for our Cloud Instances.**

Below you will find a recording explaining the process behind the TC (ThreatConnect) KVStore lookups with searches and commands in order to troubleshoot.

Recording: [ThreatConnect KT Cloud & troubleshooting.mp4](https://resources.deloitte.com/sites/SPLUNKECC/_layouts/15/stream.aspx?id=%2Fsites%2FSPLUNKECC%2FShared%20Documents%2FKT%20Sessions%2FThreatConnect%20KT%20Cloud%20%26%20troubleshooting%2Emp4&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ef2e42da8%2D2e70%2D4140%2D9aef%2Db2afe908b1a1)

The useful searches used to diagnose and check any problem in the generation process are:


[Check entries AMER] ----> [Search | Splunk 9.2.4](https://amersplunk.atrame.deloitte.com/en-US/app/search/search?q=search%20index%3Dtc_indicator_data&sid=1744182048.45410_8885B25C-D666-473E-8977-BFCC82EA4E54&display.page.search.mode=fast&dispatch.sample_ratio=1&earliest=-15m%40m&latest=now)
[Check entries EMEA] ----> [Search | Splunk 9.2.2406.118](https://es-dt-emea.splunkcloud.com/en-US/app/search/search?q=search%20index%3Dtc_indicator_data&sid=1744182140.1678361_54C0E99A-0006-40BB-8D32-E7A28725447B&display.page.search.mode=verbose&dispatch.sample_ratio=1&earliest=-30m%40m&latest=now)
[Check entries APAC] ----> [Search | Splunk 9.2.2406.117](https://es-dt-apac.splunkcloud.com/en-US/app/search/search?q=search%20index%3Dtc_indicator_data&sid=1744182211.4529125_9245DDCD-D994-4A9A-A528-6DA9E34522AE&display.page.search.mode=verbose&dispatch.sample_ratio=1&earliest=-30m%40m&latest=now)
[Values update on final lookups - AMER (change hosts for other regions)](https://amersplunk.atrame.deloitte.com/en-US/app/search/search?q=search%20index%3D_internal%20(host%3Dusatramekj001%20OR%20host%3Dusatramekj002%20OR%20host%3Dusatramekj003%20OR%20host%3Dusatramekj100%20OR%20host%3Dusatramekj101%20OR%20host%3Dusatramekj149%20OR%20host%3Dusatramekj150%20OR%20host%3Dusatramekj151%20OR%20host%3Dusatramekj152)%20%0A%20%20%20%20status%3D%22Successfully%20updated%20last%20seen%20value%22%20stanza%3D%22*indicators%22%20%0A%7C%20stats%20latest(_time)%20as%20time%20values(status)%20as%20status%20by%20stanza%20%0A%7C%20convert%20ctime(time)&display.page.search.mode=verbose&dispatch.sample_ratio=1&earliest=-4h%40m&latest=now&display.page.search.tab=statistics&display.general.type=statistics&sid=1706718412.76317_F12FEC60-CAE6-4278-9788-4404A30B1C25)
[Jobs status dashboard](https://eu1436l019.atrame.deloitte.com:8000/en-US/app/search/tc_indicator_download)

Finally the standard troubleshooting would consist on checking the KVstore status on the affected region first, since we are on Cloud, we can restore the KVStores using these queries:

**RESTORE EMAIL_INTEL**

  
| inputlookup threatconnect_email_indicators | eval threat_key="threatconnect_email_indicators" | eval _key=threat_key."|".src_user
|  eval time=now() | fields - rating
| outputlookup email_intel

**RESTORE FILE_INTEL**

  
| inputlookup threatconnect_file_indicators | eval threat_key="threatconnect_file_indicators" | eval _key=threat_key."|".file_hash
|  eval time=now() | fields - rating
|  outputlookup file_intel

**NOTE:** For ip_intel it is not possible to restore it using a query, since the _key field has different field values.

To check if the lookup has values again and that new values are being added with:

[Values update on final lookups](https://amersplunk.atrame.deloitte.com/en-US/app/search/search?q=search%20index%3D_internal%20(host%3Dusatramekj001%20OR%20host%3Dusatramekj002%20OR%20host%3Dusatramekj003%20OR%20host%3Dusatramekj100%20OR%20host%3Dusatramekj101%20OR%20host%3Dusatramekj149%20OR%20host%3Dusatramekj150%20OR%20host%3Dusatramekj151%20OR%20host%3Dusatramekj152)%20%0A%20%20%20%20status%3D%22Successfully%20updated%20last%20seen%20value%22%20stanza%3D%22*indicators%22%20%0A%7C%20stats%20latest(_time)%20as%20time%20values(status)%20as%20status%20by%20stanza%20%0A%7C%20convert%20ctime(time)&display.page.search.mode=verbose&dispatch.sample_ratio=1&earliest=-4h%40m&latest=now&display.page.search.tab=statistics&display.general.type=statistics&sid=1706718412.76317_F12FEC60-CAE6-4278-9788-4404A30B1C25)

**OTHER USEFUL QUERIES:**

**To check the quantity of events of a kvstore, the changes made to it, etc.**
  
index="_introspection" sourcetype=kvstore source="/opt/splunk/var/log/introspection/kvstore.log" component=TERM(KVStoreCollectionStats) "data.ns"="*_intel"
|table _time data.ns, data.count
|stats count latest(_time) as time dc(data.ns) as changes latest(data.count) as events by data.ns
|convert ctime(time)
|sort - events

**To check if the owners are being downloaded:**

  
index=_* source=*threatlist.log sourcetype="threatintel:download" *_indicators*

**To check _internal logs related to TC in case a job is failing or some other issue is happening:**

  
index=_internal source=/opt/splunk/var/log/splunk/splunkd.log app=TA_threatconnect_threat_intel
