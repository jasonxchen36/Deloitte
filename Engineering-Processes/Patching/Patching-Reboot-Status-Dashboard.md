There are six dashboards, one two per region and environment (AMER/EMEA/APAC).

- **AMER PRO**
- **AMER DEV**
https://amerdsplunk.atrame.deloitte.com/en-US/app/del_reboot_check/reboot?form.t_deployment=*&form.t_instance=*&form.t_type=*&form.t_host=*&form.t_technician=*





The dashboard is built to move between environments, this is the main reason to use the index **"dttl_internal_*"**.

# **Dashboard**

## **Dashboard high view**

The meaning of the tokens/columns:
- Deployment: If the machines/host are on-premise/AWS/Azure
- Instance: Kind of the machine, there are 5 types:
  -  Heavy Forwarders: Can be has installed UF too
  -  Indexers: Clusters Masters and Indexers
  -  Management: License master, Deployment servers, Deployers NOT Clusters Masters
  -  Universal Fowarders: Host only with UF installed
  -  Search Head
- Type: Depends of the Instance, made a sub-filter.
- Host: Full list of host that belongs to this environment.
- Technician: The person assigned to reboot that machines.

The dashboard table are basically based by events collected by script in the app and two lookups:
-  Events from index **dttl_internal_amer/dttl_internal_emea/dttl_internal_apac**
-  **All_machines.csv** this lookup has all information regarding machines (environment, type...) This Lookups need to be update every time a new machine will add to environment or remove. We are using the same lookuip acroos all Regions
-  **reboot_technician.csv** This lookup is mainly use by Spain team, due Spain team split the machines to reboot base in Instances

## **Dashboard look and feel**

Other interesting background need to know about dashbord behavior.

Under token, there is a tittle with Region (AMER/EMEA/APAC) + Environment (Development/Production)

![image.png](/.attachments/image-bcc1ca04-1aa9-46bb-8e49-d7c3b21ee257.png)

Under Title with the information, there are two boutons to Hide/Show chart panel and only see table.

![image.png](/.attachments/image-b06d2353-7605-4147-ad0f-08491bd10392.png)

These button are managed by a JavaScript, del_reboot_hide.js.

![image.png](/.attachments/image-110577df-c723-41ff-950d-fdce7cc2cd5a.png)

This JavaScript is located in the SH, under path **/opt/splunk/etc/apps/del_reboot_check/appserver/static/del_reboot_hide.js**

In case you can filter any value in the pie charts/table you can use the dropdown menus tokejn in the top of the Dashboard, or you can click in the pie charts

![image.png](/.attachments/image-1767790a-e475-43ad-9986-270de8c837c1.png)

In we want to clean/reset the filter, we can do by clicking in any place of the table, or using the tokens in the top

![image.png](/.attachments/image-13fdcd4f-3157-4c22-add4-b3fbdbfafbf5.png)


# Code
The TA deployed which generates events with the status of the Splunk server is named ***del_reboot_check***. It is composed by:

- bin
  - kernel_reboot.sh
- default
  - app.conf
- local
  - inputs.conf
  - props.conf
- metadata
  - default.meta
- README

## Inputs file
It runs the script located in bin, and get the returned data into the index

>[script://./bin/kernel_reboot.sh]
disabled = 0
interval = -1
index = dttl_internal_region
sourcetype = kernel_version

It will be runned every time the Splunk service, where it is installed,  is started. (interval = ***-1***)

Take note that the index must be set up to the region that it belongs. (index = dttl_internal_***region***)

## Script bash file
The script get the las reboot time, the kernel version installed and available, the Splunk Enterprise and Universal Forwarder version, the status of UF service, and the self-TA version.

### ./bin/kernel_reboot.sh
```bash
#!/bin/bash
EpochLastReboot=$(($(date +%s)-$(cat /proc/uptime | cut -f1 -d'.')))
LastKernel=$(rpm -q --last kernel | awk 'NR==1{print $1}' | sed 's/^kernel-//')
KernelVersion=$(uname -r)
SplunkPath=$(find /opt -maxdepth 1 -type d -iname "splunk*" 2> /dev/null)
while read -r line; do
    [[ $line == /opt/splunk ]] && { \
        SplunkVersionSE=$($line/bin/splunk version 2>/dev/null | grep "Splunk" | awk '{print $(NF -2)}'); \
        SplunkBuildSE=$($line/bin/splunk version 2>/dev/null | grep "Splunk" | awk '{print $(NF -0)}' | tr -d ')'); }
    [[ $line == /opt/splunkforwarder ]] && { \
        SplunkVersionUF=$($line/bin/splunk version 2>/dev/null | grep "Splunk" | awk '{print $(NF -2)}'); \
        SplunkBuildUF=$($line/bin/splunk version 2>/dev/null | grep "Splunk" | awk '{print $(NF -0)}' | tr -d ')'); \
        SplunkRunningUF=$($line/bin/splunk status 2>/dev/null | grep "splunkd"); \
        [[ $SplunkRunningUF == *"is running"* ]] && SplunkRunningUF="YES" || { [[ $SplunkRunningUF == *"not running"* ]] && SplunkRunningUF="NO"; }; }
done <<< "$SplunkPath"
[[ -z $SplunkVersionSE ]] && SplunkVersionSE="N/A"; [[ -z $SplunkBuildSE ]] && SplunkBuildSE="N/A"; [[ -z $SplunkVersionUF ]] && SplunkVersionUF="N/A"; [[ -z $SplunkBuildUF ]] && SplunkBuildUF="N/A"; [[ -z $SplunkRunningUF ]] && SplunkRunningUF="N/A"
SplunkAppPath=$(find /opt/splunk*/etc/ -maxdepth 2 -type d -iregex '.*apps\/del_reboot_check' 2> /dev/null)
AppVersion=$(grep ^version $SplunkAppPath/default/app.conf | awk -F" = " {'print $2'})
echo $(date +%s) up_time=$EpochLastReboot last_kernel_available=$LastKernel kernel_installed=$KernelVersion splunk_version_se=$SplunkVersionSE splunk_build_se=$SplunkBuildSE splunk_version_uf=$SplunkVersionUF splunk_build_uf=$SplunkBuildUF splunk_running_uf=$SplunkRunningUF app_version=$AppVersion
```
## Props file
The event has a timestamp head formed as epoch time, which get the time when the event is generated.

After that, the event is formed as a **key=value** pairs, and the fields are extracted natively by Splunk.

Nevertheless, there is a configuration in props file to set the data ingest. That includes the Magic 8 (line breaking and timestamp configuration) and field extractions regex.

>[kernel_version]
TIME_PREFIX = ^\d{10}
TIME_FORMAT = %s
>MAX_TIMESTAMP_LOOKAHEAD = 10
SHOULD_LINEMERGE = false
LINE_BREAKER = ([\r\n]+)
TRUNCATE = 999999
EXTRACT-fields = up_time=(?<up_time>\d+) last_kernel_available=(?<last_kernel_available>\S+) kernel_installed=(?<kernel_installed>\S+) splunk_version_se=(?<splunk_version_se>\S+) splunk_build_se=(?<splunk_build_se>\S+) splunk_version_uf=(?<splunk_version_uf>\S+) splunk_build_uf=(?<splunk_build_uf>\S+) splunk_running_uf=(?<splunk_running_uf>\S+) app_version=(?<app_version>\S+)

## README file
That introduces ands explain the project.

It contains information commonly required to understand it.

It also track changes applied to the TA.
