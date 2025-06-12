**Features**

The following entry purpose is to explain how the KVStore and lookup backups processes works.

_!!! Only works for OnPrem Environments_

**Process**

It consists on creating a KVstore backup from CLI, and creating a Lookup backup of specifics lookups files using shell commands.

It is executed automatically daily and stored locally as files.

[[_TOC_]]

# KVstore backup

## 1. Script
The process executes 6 steps/functions.

Each step return a message logged into a log file.

Eachy step is logged into a log file (**/opt/splunk/var/log/splunk/backup_kvstore.log**).

Backups are stored into **/opt/splunk/var/lib/splunk/kvstorebackup/** directory.

### 1.1. Initial checkings
Check if log file exists. If it not exists, it is created.

Start loggin the output messages into log file.

Check if backup directory exists. If it not exists, it is created.

### 1.2. Backup KVstore
Check if KVstore status and restore status are ready.

If so, it executes a Kvstore backup by using Splunk CLI and assigning it a custom file name (**kvdump_YYYYMMDD.tar.gz**).

In case it fails, it return a failure message.

### 1.3. Clean KVstore backups
This rotates the KVstore backup files.

Retention policy is set to 3 backup files older than 3 days ago.

### 1.4. Backup Lookup
Check if any of the following lookups exists:
 - DA-ESS-**Americas**-Lookups
 - DA-ESS-**APAC**-Lookups
 - DA-ESS-**EMEA**-Lookups
 - DA-ESS-**Global**-Lookups

And it creates a packed and compressed file (**.tar.gz**) stored into backup directory, using a custom file name (**lookup_YYYYMMDD.tar.gz**).

### 1.5. Clean Lookup backups
This rotates the Lookup backup files.

Retention policy is set to 3 backup files older than 3 days ago.

### 1.6. Check volume
Get the size of the backup directory in kB to be monitorized.

## 2. Input
The script is executed by Splunk at  00:01 UTC daily.

Log file is fed by Splunk monitoring the log file, and being ingested at **dttl_internal_** *REGION*.

Source as **backup_kvstore**, and sourcetyped as **kv_bck**.

## 3. Lookup
Where region's SH cluster memebers are included (**kvstore_members.csv**).

This lookup will be used to be crossed with logs to capture if any SHC member has skipped the backups.

## 4. Saved Search
An alert report will notify if  any of the SH cluster has skipped or failed any of the backup processes.

I will be ran 03:00 UTC daily reporting to *eserscybersocmsssiemsplunk@deloitte.com*.

As mentioned, this search cross logs with a lookup where SH cluster members are included.

In case any error log or skipped backup occurrs, an email sibjected as "*KVstore daily backup failed*" will be sent.

## 5. Version
Curent version is v2.0.3.

Version are indicated at default/app.conf file.

Version changes are reflected into **README** file.

## 6. Code
### - bin/backup_kvstore.sh

```bash
#!/bin/bash
#
# GLOGAL VARIABLES
#
LOG_FILE='/opt/splunk/var/log/splunk/backup_kvstore.log'            #
KVSTORE_PREFIX='kvdump_'                                            #
LOOKUP_PREFIX='lookup_'                                             #
BACKUP_DIRECTORY='/opt/splunk/var/lib/splunk/kvstorebackup/'        #
BACKUP_EXT='.tar.gz'                                                #
BACKUP_DAYS='3'                                                     # Calculated later
BACKUP_FILES_DESIRED='3'                                            #
APP_NAMES='DA-ESS-*-Lookups'                                        #
LOOKUP_NAMES="(Americas|APAC|EMEA|Global)"                          #
SPLUNK_HOME_PATH="/opt/splunk"                                      #
#
# FUNCTIONS
#
log_msg () {
     # Log the timestamp and the message
     echo -e "[$(date '+%Y-%m-%dT%H:%M:%S%Z')] $@"
}
#
initial_checkings () {
     # Checking if the log file does not exists
     [[ -f ${LOG_FILE} ]] && { exec &>> ${LOG_FILE} 2>&1; } || { touch ${LOG_FILE}; exec &>> ${LOG_FILE} 2>&1; log_msg "Creating log file (${LOG_FILE})"; }
     # Checking if the backup directory does not exists
     [[ ! -d ${BACKUP_DIRECTORY} ]] && { mkdir ${BACKUP_DIRECTORY}; log_msg "Creating backup directory (${BACKUP_DIRECTORY})"; }
}
#
clean_backups () {
     # Get the KVStore or Lookup backup filenames
     backupFiles=$(find ${BACKUP_DIRECTORY} -maxdepth 1 -name "${1}*${BACKUP_EXT}" -type f | sort)
     # Start the 2 cicle loop (one for kvstore, and one for lookup backups)
     # Count the number of the total backup files
     numBackupFiles=$(echo $backupFiles | awk -F" " '{print NF}')
     # Check if there are more backup files than desired
     if [[ ${numBackupFiles} -gt ${BACKUP_FILES_DESIRED} ]]; then
          # Get the old backup filenames (more than X days old)
          BACKUP_DAYS=$((${BACKUP_DAYS}-1))
          oldBackupFiles=$(find ${BACKUP_DIRECTORY} -maxdepth 1 -name "${1}*${BACKUP_EXT}" -type f -mtime +$BACKUP_DAYS | sort)
          # Count the number of the total old backup files
          numOldBackupFiles=$(echo $oldBackupFiles | awk -F" " '{print NF}')
          # Check if there are any old logs
          if [[ ${numOldBackupFiles} -gt 0 ]]; then
               # Get the difference between all backup files and old backup files
               diffBackupFiles=$((${numBackupFiles}-${numOldBackupFiles}))
               # Check if old backup files are more or less than the desired backup files
               if [[ ${diffBackupFiles} -lt ${BACKUP_FILES_DESIRED} ]]; then
                    # If the difference is less than desired backup files, get the EARLIEST backup files to remove
                    removeOldBackups=$(echo ${oldBackupFiles} | cut -d " " -f 1-$((${numBackupFiles}-${BACKUP_FILES_DESIRED})))
               elif [[ ${diffBackupFiles} -ge ${BACKUP_FILES_DESIRED} ]]; then
                    # If the difference is more than desired backup files, get ALL the old backup files to remove
                    removeOldBackups=$(echo ${oldBackupFiles})
               fi
               # Remove the calculated backup files
               rm ${removeOldBackups} \
                    && { removeOldBackups=$(echo ${removeOldBackups} | sed "s|${BACKUP_DIRECTORY}||g"); log_msg "Backups removed: ${removeOldBackups}"; } \
                    || log_msg "Backups removed FAILED: ${removeOldBackups}"
          fi
     fi
}
#
backup_kvstore (){
     # Read the admin token to execute commands
     read tok
     # Get the kvstore status
     kvstore_status=$(SPLUNK_TOK=${tok} ${SPLUNK_HOME_PATH}/bin/splunk show kvstore-status 2> /dev/null | grep 'status' | awk '{printf $3}')
     # Get the kvstore backup restore status
     kvstore_backup_restore_status=$(SPLUNK_TOK=${tok} ${SPLUNK_HOME_PATH}/bin/splunk show kvstore-status 2> /dev/null | grep 'backupRestoreStatus' | awk '{printf $3}')
     # Check if both services are running
     if [[ ${kvstore_backup_restore_status,,} == "ready" && ${kvstore_status,,} == "ready" ]]; then ################
          # Set the kvstore backup filename, including the date & time
          filename="${KVSTORE_PREFIX}$(date -u +'%Y%m%d')"
          # Backup the kvstore
          SPLUNK_TOK=${tok} ${SPLUNK_HOME_PATH}/bin/splunk backup kvstore -archiveName ${filename} 2> /dev/null \
               && log_msg "KVStore backup file created: ${filename}${BACKUP_EXT}" \
               || log_msg "KVStore backup file FAILED: ${filename}${BACKUP_EXT}"
     else
          # In case it fails, it log it
          [[ ${kvstore_backup_restore_status,,} != "ready" ]] && log_msg "KVstore not ready by Backup Restore Status"
          [[ ${kvstore_status,,} != "ready" ]] && log_msg "KVstore not ready by KVstore Status"
     fi
     # Time to finish backup (10')
     sleep 600
}
#
backup_lookup () {
     # Get the Lookups paths for Americas, APAC, EMEA & Global
     lookup_paths=$(find ${SPLUNK_HOME_PATH}/etc/apps/ -maxdepth 1 -name ${APP_NAMES} -type d | grep -E "${LOOKUP_NAMES}" | sed "s,$,/lookups/,g" | tr '\n' ' ')
     # Check if there are results
     if [[ -z "$lookup_paths" ]]; then
          log_msg "Lookup backup file CANCELLED: no lookups files to backup"
     else
          # Get the Lookups list name
          lookupListNames=$(echo ${lookup_paths} | sed "s,${SPLUNK_HOME_PATH}/etc/apps/,,g" | sed "s,/lookups/,,g" | sed "s/ /, /g")
          # Get a copy of the lookups
          for directory in ${lookup_paths}; do
               # Get the lookup name
               tempNames=$(echo ${directory} | sed "s,${SPLUNK_HOME_PATH}/etc/apps/,,g" | sed "s,/lookups/,,g")
               # Take a lookup copy to backup
               cp -r ${directory} ${BACKUP_DIRECTORY}${tempNames}
          done
          # Generates the backup filename
          filename="${BACKUP_DIRECTORY}${LOOKUP_PREFIX}$(date -u +'%Y%m%d')${BACKUP_EXT}"
          # Tar and compress the lookups
          tar -zcf ${filename} --absolute-names $(find ${BACKUP_DIRECTORY} -maxdepth 1 -name ${APP_NAMES} -type d) \
               && log_msg "Lookup backup file created: $(echo ${filename} | sed "s,${BACKUP_DIRECTORY},,g") - including: ${lookupListNames}" \
               || log_msg "Lookup backup file FAILED: $(echo ${filename} | sed "s,${BACKUP_DIRECTORY},,g") - including: ${lookupListNames}"
          # Time to finish backup (10')
          sleep 600
          # Removing temp lookups
          find ${BACKUP_DIRECTORY} -maxdepth 1 -name ${APP_NAMES} -type d -exec rm -rf {} \; \
               || log_msg "Removing temp directory FAILED."
     fi
}
#
check_volume () {
     # Time to finish compressing backups and removing backup files (2h)
     sleep 7200
     # Get the size of the backup directory in kB
     volume_backupdir=$(du -m ${BACKUP_DIRECTORY} | tail -1 | awk {'print $1'})
     log_msg "Backup directory volume: ${volume_backupdir} MiB"
}
#
# MAIN PROGRAM
#
initial_checkings
backup_kvstore
clean_backups "${KVSTORE_PREFIX}"
backup_lookup
clean_backups "${LOOKUP_PREFIX}"
check_volume
```
### - default/app.conf
>[install]
is_configured = 0

>[ui]
is_visible = 0
label = kv_bck

>[launcher]
author = DT - Cyber Defense Engineering - Health Monitoring <deloittesiemhealthmonitoringteam@deloitte.com>
description = App to backup KVstore and Lookups
version = 2.0.3

### - local/inputs.conf
>[script://./bin/backup_kvstore.sh]
disabled = 0
interval = 1 0 * * *
passAuth = admin

>[monitor:///opt/splunk/var/log/splunk/backup_kvstore.log]
disabled = 0
index = dttl_internal_*region*
source = backup_kvstore
sourcetype = kv_bck

### - local/savedsearches.conf
>[KVstore backup Alert - Report]
>\#### Author: Francisco Sanchez
>\#### Email: fsanchezsuarez@deloitte.es
>action.correlationsearch.enabled = 1
>description = Alerts when Kvstore backup process fails.
>\# Email Action Settings
>action.email = 1
>action.email.to = eserscybersocmsssiemsplunk@deloitte.com
>action.email.subject = KVstore daily backup failed
>action.email.include.results_link = 1
>action.email.include.view_link = 1
>action.email.inline = 1
>action.email.message.alert = KVstore or lookup backup failed for the following hosts:
>action.email.sendresults = 1
>action.email.useNSSubject = 1
>counttype = number of events
>\#dispatch search options
>enableSched = 1
>cron_schedule = 0 3 * * *
>disabled = 0
>dispatch.earliest_time = -1m@m
>dispatch.latest_time = now
>quantity = 0
>relation = greater than
>\#Correlation Search Query
>search = | inputlookup kvstore_members.csv \
>| search NOT \
>    [ search index=dttl_internal_*region* sourcetype=kv_bck "KVStore backup file created" earliest=-4h@h \
>        [| inputlookup kvstore_members.csv] \
>    | table host] \
>OR NOT \
>    [ search index=dttl_internal_*region* sourcetype=kv_bck "Lookup backup file created" OR "Lookup backup file CANCELLED" earliest=-4h@h \
>        [| inputlookup kvstore_members.csv] \
>    | table host] \
>OR \
>    [ search index=dttl_internal_*region* sourcetype=kv_bck "FAILED" earliest=-4h@h \
>        [| inputlookup kvstore_members.csv] \
>    | table host]

### - lookups/kvstore_members.csv
>host
>*member1*
>*member2*
>*member...*

### - metadata/default.meta
>[]
access = read : [ admin, cpblty_gems_user ], write : [ admin, cpblty_gems_admin ]
export = system
owner = nobody

### - README
```
================================================
Overview
================================================

This app makes daily backups from the KVstore and the "Americas|APAC|EMEA|Global" DA-ESS-*-Lookups. And send the result to and nternal index where the changes are logged.


================================================
Monitoring process
================================================

Used by a search, using this simple query: index=dttl_internal_* sourcetype=kv_bck


================================================
Known Limitations
================================================

1) The bash script must have executing permissions.


================================================
Getting Support
================================================

Send an email to the following if you need support:

deloittesiemhealthmonitoringteam@deloitte.com


================================================
Change History
================================================

+---------+------------------------------------------------------------------------------------------------------------------+
| Version |  Changes                                                                                                         |
+---------+------------------------------------------------------------------------------------------------------------------+
| 1.0     | Initial release.                                                                                                 |
|---------|------------------------------------------------------------------------------------------------------------------|
| 2.0.0   | Simplified merging all actions at just one script.                                                               |
|         | Check KVstore status before the backup.                                                                          |
|         | Error logs in case it fails.                                                                                     |
|         | Add directory volume.                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------|
| 2.0.1   | Updated backup_kvstore.sh to discard warning messages after upgrading Splunk to v9.0.6                           |
|---------|------------------------------------------------------------------------------------------------------------------|
| 2.0.2   | Updated Saved Search to fine tuning                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------|
| 2.0.3   | Lookup backup is made from a folder copy at backup directory to avoid errors while compressing,                  |
|         | in case it changes during the process.                                                                           |
|         | Saved search now alerts in case a failed message is generated.                                                   |
+---------+------------------------------------------------------------------------------------------------------------------+
```
**End**