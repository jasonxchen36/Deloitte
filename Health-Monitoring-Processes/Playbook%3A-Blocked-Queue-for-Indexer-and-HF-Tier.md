**Playbook: Blocked Queue for Indexer Tier**

•	A panel is created on the HM-Admin Dashboard to display blocked queues on the Indexing and Intermediate Tier, which goes by name "Indexer Queue Full Events" and “HF/IF Queue Full events”. 
•	As blocked queues might cause latency. HM Team should identify any blocked queues from Dashboard panel and create WI# on DevOps and assign it to queue "Deloitte SIEM Health Monitoring" to start working on them.

**Playbook: How to identify blocked queue from the dashboard panels and create a WI#**


1.	When requires_attention (1) column  states "not unusual" or "no need to worry but keep an eye on it", HM team can ignore them.
2.	If the requires_attention column(1) contains the phrases "fix highly recommended!" or "you better check..," it signifies that the indexer queue is getting filled, and HM Team must troubleshoot the indexer to identify the problem and resolve it as it might pause the data flow.

The Blocked ratio (blocked_ratio) measures the proportion of blocked queues with the total number of queues coming up at the specified time (5 minutes). When the blocked_ratio is more than 40, then message will display in the requires_attention box in the blocked queue panel. Message displayed will be: “Fix, Highly recommended"

3.	On the host queue (3), The team will see the names of the indexers instances that have blocked queues. Next to the instance name on the right, they will see information about the layer of the queue that has been blocked (4). 
4.	 ![image.png](/.attachments/image-e57beacf-11d6-47b8-b9fc-aaf5fc6b9e26.png)
5.	Go to DevOps and click on Boards>Work Items>New Work item>Health Monitoring Team Task. On the details tab, add indexer details along with screenshots as required.
6.	Assign it to "Deloitte SIEM Health Monitoring Team" queue.
7.	HM Team can then troubleshoot and work on releasing blocked spaces based on the layer of the queue that is blocked.


**Sample scenarios for blocked Queues:**

1. High CPU Utilization on the instance. 

               1. index=_internal host=<server> source=*metrics.log group=pipeline | timechart span=1h sum(cpu_seconds) by processor
   
 ![image.png](/.attachments/image-1257f625-74f3-48e0-9a8b-360dfe9fda86.png)
 
View the results of this search as a stacked column chart to see how much CPU is being used by the aggregator process compared to the others. Fine tune the line merging and time extractions settings in props.conf to help Splunk run faster.
 
2. Identify the high volume data source sending data into Splunk during blocked queues for volume analysis.
Go to DMC>Monitoring Console>Indexing>Performance>Indexing Performance and choose the instance (indexer) from the drop-down menu.
 ![image.png](/.attachments/image-63f70e4b-d731-4446-86db-fb7d9d512e74.png)
 
**Troubleshooting steps:**

The four major queues in the data input pipeline are parsing, merging, typing, and index. Data flows through the queues in the following order and each one contains different processes that take place within them.

![image.png](/.attachments/image-bf62df1d-652b-47aa-94ce-51162ba5856e.png)

              1. Parsing queue
                              ○ UTF-8 – character encoding
                              ○ Line Breaker – breaks down the events into separate lines
                              ○ Header – rewrites index-time fields if prompted
               2. Merging queue
                              ○ Aggregator – includes line merging and time stamp extraction
               3. Typing queue
                              ○ Regex replacement – performs any regular expression replacements called on in props.conf/tranforms.conf
                              ○ Annotator – extracts the punct field
               4. Index queue
                              ○ TCP/Syslog out – sends data to a remote server
                              ○ Indexer – writes the data to disk
 
Run the following search, replacing <server> with the name of the faulty server you want to query, to see if any queues are indeed blocked:
 
index=_internal host=<server> source=*metrics.log group=queue blocked=true


               1. index=_internal host=<server> source=*metrics.log group=queue blocked=true

![image.png](/.attachments/image-0e64a79c-0ef4-4e0a-b1c8-3c47dda104dd.png)

**Advanced Troubleshooting:** 

- [ ] While performing the above troubleshooting steps if HM Team faces any restriction like permission related issue please reach out to SIEM Engineering Team for the advanced troubleshooting purposes. 
- [ ] The best practice for troubleshooting blocked queues is to check the left most filled queue from the above snapshot as that shall be a potential reason why the next subsequent queues are getting blocked.
- [ ] Based on the queue, The team can do a deeper dive and troubleshoot accordingly:
Note: For any changes to the CPU size or a queue stated below, they will have to thoroughly discuss and create PR if needed.
- [ ] If the team is unable to find a root cause, then open Splunk Support case for further troubleshooting 


 
### **Agg Queue:**
aggQueue is where time extraction and line merging happens. More number of agg queue blocks means that a lot of strange time stamps & the aggQueue has to work hard to match them. Best thing to do is check for time stamp differences and clean/fix them.
               
1. Check for any magical parameters on props stanza by going the indexer instances. Validate Max_Timestamp_lookahead, LINE_BREAKER are set correctly for the sourcetypes which ingest huge amount of logs through the Indexer.
 
 
### **Typing Queue:**
Typing queue performs regex replacement called on props/transforms.conf. It also helps in annotator - extraction of punt fields.
               
1. Check and set the size limit under [metrics] stanza in limits.conf for the affected instance.
               maxseries = 50
               2. Below query will help understand which sourcetype is taking most of the CPU time per event.
               index=_internal host= source=*metrics.log group=per_sourcetype_regex_cpu |timechart max(cpu) by series
               3. You can the check the sourcetype and identify which regex parameters are buggy and would require a rework
 
### **TCP IN Queue:**
It is the first level of Queue 
               
1. Increase the Thruput by going to etc/system/local/limits.conf
               [thruput]
maxKBps = 500
               2. Increase the size limit of splunk TCP by going to etc/system/local/inputs.conf
               [splunktcp://9997]
               queueSize = XMB

### **Index queue:**
From parsing queue, It then moves into the indexQueue and on to the indexing pipeline, where the Splunk software stores the events on disk
               
1. Check if the resource where the indexer queue is blocked are sufficient for the work and you can do this using the Monitoring Console , especially see the CPU load.
               2. Check if the Indexer instance is using parallel pipelines.
               Under etc/system/local/server.conf
               Set parallelIngestionPipelines to maximum as per CPU core of instances

 
### **Parsing queue:** 
Incoming data goes first to the parsingQueue and from there to the parsing pipeline, where it undergoes event processing
               
1. Optimize the regex in your parsing queue (props.conf transform.conf), starting with your largest sourcetypes             
2. Example: see if Max_timestamp_lookahead is set correctly so Splunk can parse timestamp easily
3. Increase the size limit of your queue buffer which will allow more time for your CPU to process backlogs.
   Under etc/system/local/server.conf
   [queue=parsingQueue] increase the maxSize to a reasonable size
   Before making any changes to size of the queue, please check if increasing the thruput or increasing the pipelines (parallelIngestionPipelines) helps you achieve your goals. Changing the size of queue comes with a lots of limitations and hence should be avoided.
