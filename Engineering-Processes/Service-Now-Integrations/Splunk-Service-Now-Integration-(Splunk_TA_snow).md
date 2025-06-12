The add-on collects incident, event, change, user, user group, location, and CMDB CI information from ServiceNow via ServiceNow REST APIs. The add-on also provides workflow actions that allow users to link directly from events in the Splunk platform search results to relevant ServiceNow incidents, events, and Knowledge Base articles.
When the add-on collects a ServiceNow database table, the add-on assigns a source type for the events, using the schema _snow:database_table_name_. We are collecting the asset list data from the ServiceNow cmdb (change management data base). The database table name is: _u_cmdb_splunk_view_.

The app need to download from Splunk Base: [Splunk Add-on for ServiceNow | Splunkbase](https://splunkbase.splunk.com/app/1928)

The following screenshots describes the setup process:

![image.png](/.attachments/image-200d7aab-6f4d-4545-aea9-c89fd08f437b.png)

![image.png](/.attachments/image-5e9c6a52-47e7-4b2d-b7e3-049954c314aa.png)

Password for user **dtt_sc_app0665_splunk_reporting_prod** is storage in Thycotic
**Record Count** need set to 500, due in the past there were several performance issue related with API in Snow end

![image.png](/.attachments/image-f9133236-4b2a-422f-a096-4e2cd0f95063.png)

![image.png](/.attachments/image-5d18ba81-6639-43e2-84c1-5a4702f7931c.png)

![image.png](/.attachments/image-45cc35cf-7bed-40c5-a7d7-e71fc4e1288a.png)

![image.png](/.attachments/image-77940ffc-f77c-4ed6-a518-0bb88054f01b.png)

![image.png](/.attachments/image-f7d91a9e-0e81-43e0-bfa7-0a60e2b235ce.png)

![image.png](/.attachments/image-22c4d272-93aa-4859-8292-fc53ddb43e1f.png)

With the following btool query we can review the status of inputs in Cloud environment

| makeresults_ 
| eval conf_file = "inputs"
| makemv delim="," conf_file
| mvexpand conf_file
| map search="| btool $conf_file$ list --debug --kvpairs | search "btool.app" IN (Splunk_TA_snow)  | fields _raw btool.app btool.source btool.stanza | rex field=_raw "^(?<path>.*\.conf)\s+(?<value>.*)" |search path=*/local/* "
|rename btool.app as Application,  btool.source as "Conf File", btool.stanza as Stanza, value as Parameter, path as Path
|table Stanza Parameter
|stats values(Parameter) as Parameter by Stanza


![image.png](/.attachments/image-585923e7-73e7-43b7-a4b6-1ac1877d6baa.png)

The actual setup for inputs, now is the following:

**snow://SNOW_Request_Item**    
    account = servicenow
    disabled = 0
    duration = Deprecated - Please use the interval field instead
    id_field = reqitem_sys_id
    index = application_servicenow_ticketing_all
    interval = 60
    since_when = 2024-09-24 13:41:59
    table = u_request_item_splunk_view
    timefield = reqitem_sys_updated_on

**snow://SNOW_Security_Incident_and_Metrics**  
    account = servicenow
    disabled = 0
    duration = Deprecated - Please use the interval field instead
    id_field = si_sys_id
    index = application_servicenow_ticketing_all
    interval = 900
    since_when = 2024-10-01 10:40:21
    table = sn_si_security_incident_metrics_splunk_view
    timefield = si_sys_updated_on


**snow://SNOW_Task_and_SLA**    
    account = servicenow
    disabled = 0
    duration = Deprecated - Please use the interval field instead
    id_field = inc_sys_id
    index = application_servicenow_ticketing_all
    interval = 360
    since_when = 2024-09-24 13:41:14
    table = u_task_sla_splunk_view
    timefield = inc_sys_updated_on

**snow://SNOW_USER_Affected**  
    account = servicenow
    disabled = 0
    duration = Deprecated - Please use the interval field instead
    id_field = si_sys_id
    index = application_servicenow_ticketing_all
    interval = 400
    since_when = 2024-09-24 13:45:38
    table = sn_si_security_incident_affected_users_splunk_view
    timefield = taau_sys_updated_on


**snow://SNOW_incident_metric**
    account = servicenow
    disabled = 0
    duration = Deprecated - Please use the interval field instead
    id_field = inc_sys_updated_on
    index = application_servicenow_ticketing_all
    interval = 360
    since_when = 2024-09-24 13:43:06
    table = u_incident_metric_splunk_view
    timefield = sys_updated_on

**snow://Splunk_SNOW_asset**    
    account = servicenow
    disabled = 0
    duration = Deprecated - Please use the interval field instead
    id_field = cmdb_sys_id
    index = referential_servicenow_asset_all
    interval = 300
    since_when = 2024-09-24 13:46:19
    table = u_cmdb_splunk_view
    timefield = cmdb_sys_updated_on

**snow://cmdb_ci_service**  
    account = servicenow
    disabled = 0
    duration = Deprecated - Please use the interval field instead
    id_field = sys_id
    index = application_servicenow_ticketing_all
    since_when = 2024-09-24 13:44:41
    timefield = sys_updated_on

## Troubleshooting

With the following search we can find issues, review the performance, check record downloads...

![image.png](/.attachments/image-2d2f9cc1-62da-475f-8d2e-958e1216bb9c.png)