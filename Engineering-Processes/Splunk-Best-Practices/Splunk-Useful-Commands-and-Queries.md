### Min Max Avg Data Volume

```
index=_internal host=ushdc8887n07 source=*license_usage.log* type="Usage" idx=<INDEX>
| timechart span=1d sum(eval(b/1024/1024/1024)) AS volume_b by pool limit=0
| transpose
| rename column as pool
| search NOT pool="_*"
| foreach row* [eval vals=mvappend(vals, '<<FIELD>>')]
| stats min(vals) as min_vol_b max(vals) as max_vol_b avg(vals) as avg_vol_b by pool
```

### LDAP Queries for MF of USERNAME

```
| ldapsearch domain=deloitte search="(sAMAccountName=<USERNAME>)"
| lad-search domain=deloitte search=“(extensionAttribute10=MF)”
```

### Count of Alerts Over Last Day

```
index=notable search_name!=*Dev* 
| stats count
```

### Average Run Time of Saved Searches

```
index=_internal sourcetype=scheduler status=success
| eval run_time=(run_time/60) 
| stats count avg(run_time) as avg_run min(run_time) as min_run max(run_time) as max_run by app
| sort - avg_run
```

### CPU and Memory Usage per App

```
index=_introspection sourcetype=splunk_resource_usage (host=usatramekj001* OR host=usatramekj002* OR host=usatramekj003* OR host=usatramekj100* OR host=usatramekj101*) component=PerProcess 
| rename data.search_props.app AS app 
| stats sum(data.pct_cpu) AS sum_cpu_usage, sum(data.pct_memory) AS sum_memory_usage by app 
| sort - sum_cpu_usage
```

### Count of Unique Hosts

```
| metadata type=hosts index=* 
| search host=* 
| stats count
```

### License Usage Average Min Max

```
index=_internal host=ushdc8887n07 source=*license_usage.log* type="Usage" 
| timechart span=1d sum(eval(b/1024/1024/1024)) AS volume_b 
| stats avg(volume_b) min(volume_b) max(volume_b)
```

### Ingestion by Index

```
index=_internal host=ushdc8887n07 source=*license_usage.log* type="Usage" 
| stats sum(eval(b/1024/1024/1024)) AS volume_b values(pool) as pool by idx 
| eval DC=case(like(pool,"%US%"),"US Data Center",like(pool,"%AMEA%"),"Global Data Center",like(pool,"%Azure%"),"Azure Indexers") 
| fields idx volume_b pool DC
```

### Ingestion by DC

```
index=_internal host=ushdc8887n07 source=*license_usage.log* type="Usage" 
| stats sum(eval(b/1024/1024/1024)) AS volume_b values(pool) as pool by idx 
| eval DC=case(like(pool,"%US%"),"US Data Center",like(pool,"%AMEA%"),"Global Data Center",like(pool,"%Azure%"),"Azure Indexers") 
| fields idx volume_b pool DC 
| stats sum(volume_b) as total_gb by DC
```

### Ingestion by Index and DC

```
index=_internal host=ushdc8887n07 source=*license_usage.log* type="Usage" 
| stats sum(eval(b/1024/1024/1024)) AS volume_b values(pool) as pool by idx 
| eval DC=case(like(pool,"%US%"),"US Data Center",like(pool,"%AMEA%"),"Global Data Center",like(pool,"%Azure%"),"Azure Indexers") 
| fields idx volume_b pool DC 
| stats sum(volume_b) as total_gb avg(volume_b) as avg_per_dc max(volume_b) as max_per_dc min(volume_b) as min_per_dc by DC
```

### Ingestion by Pool with Average Min Max

```
index=_internal host=ushdc8887n07 source=*license_usage.log* type="Usage"
| timechart span=1d sum(eval(b/1024/1024/1024)) AS volume_b by pool limit=0
| transpose
| rename column as pool
| search NOT pool="_*"
| foreach row* [eval vals=mvappend(vals, '<<FIELD>>')]
| stats min(vals) as min_vol_b max(vals) as max_vol_b avg(vals) as avg_vol_b by pool
```

### Unique Fields for Index

```
<your search> 
| stats dc(*) as * 
| transpose 
| table column
```

### Bucket Analysis

```
| dbinspect index=all_cloud_microsoft_office 
| eval bucket_start_time=strftime(startEpoch,"%m/%d/%y %H:%M:%S")
| eval bucket_end_time=strftime(endEpoch,"%m/%d/%y %H:%M:%S")
| eval bucket_span=tostring((endEpoch-startEpoch), "duration")
| eval bucket_size=sizeOnDiskMB/1024
| table index,splunk_server,id,bucket_start_time,bucket_end_time,bucket_span,bucket_size
```

### Total Count of Non-Internal Events

```
| tstats count WHERE index!=_*
```

### Total Count of Non-Internal Notables

```
index=notable description!=DEV* orig_index!=_* 
| stats count
```

### All Indexes Minus First Part of Name

```
index=* 
| rex field=index "(?<index_types>\_(.*))"
| stats count by index_types
```

### MBps and Mbps for Index

```
index=<INDEX>
|eval size=len(_raw)
|timechart span=1s sum(eval(size/1024/1024)) AS MBps
|eval Mbps=(MBps*8)
|stats avg(MBps) min(MBps) max(MBps) avg(Mbps) min(Mbps) max(Mbps)
```

### Firewall Hostnames

```
index=*checkpoint*
| rex field=originsicname "CN\\\=(?<fwname>[^\\<]+)\,O\\\=(?<orgname>[^\\<]+)"
| stats count by fwname,orgname
```

### Splunk Users Last Login

```
index=_audit action="login attempt" (user=x)
| stats first(_time) AS last_login by host,user 
| convert ctime(last_login)
```

### Ratio of Events to Errors

```
index=*network_f5_vpn 
| eval bool=if(eventtype="err0r",1,0) 
| stats sum(bool) as fail_count count as total by index host 
| eval ratio=round(fail_count/total,2)
```

### Ratio of Windows Events

```
index=*_endpoint_microsoft_windows_*
| stats count latest(Message) as Message latest(signature) as signature by index EventCode
| eventstats sum(count) as index_total by index
| eval index_ratio=count/index_total
| sort - index_ratio
| lookup windows_signatures.csv signature_id as EventCode OUTPUT signature as Windows_Event_Description
| eval Windows_Event_Description=coalesce(Windows_Event_Description,signature,Message)
| rename EventCode as Windows_Event_Code
| fields index Windows_Event_Code Windows_Event_Description count index_ratio index_total
```

### All Lookups

```
| rest /services/data/lookup-table-files 
| table title eai:acl.app
```

###Indexes Oldest/Newest Events

```
| tstats min(_time) as oldest_event_time max(_time) as newest_event_time min(_indextime) as oldest_indexed_time max(_indextime) as newest_indexed_time WHERE index=* by index
| eval now=now()
| eval oldest_event_days=tostring(round((now-oldest_event_time)/60/60/24)." day(s)")
| eval newest_event_days=tostring(round((now-newest_event_time)/60/60/24)." day(s)")
| eval oldest_indexed_days=tostring(round((now-oldest_indexed_time)/60/60/24)." day(s)")
| eval newest_indexed_days=tostring(round((now-newest_indexed_time)/60/60/24)." day(s)")
| convert timeformat="%Y-%m-%d %H:%M:%S" ctime(oldest_event_time) ctime(newest_event_time) ctime(oldest_indexed_time) ctime(newest_indexed_time)
| table index, oldest_event_time, oldest_event_days, newest_event_time, newest_event_days, oldest_indexed_time, oldest_indexed_days, newest_indexed_time, newest_indexed_days
```

