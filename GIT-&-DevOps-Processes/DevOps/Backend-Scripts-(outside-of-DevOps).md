#Indexer Sync Script
`#!/bin/bash`
`date`
`echo "Refreshing repository from Azure DevOps"`
`cd /opt/splunk/git/IndexerCM`
`git pull --all`
`/opt/splunk/git/IndexerCM/AutomatedScripts/automated-apply-script.sh`

#Search Head Cluster Sync Script
`#!/bin/bash`
`date`
`echo "Refreshing repository from Azure DevOps"`
`cd /opt/splunk/git/SHC/ `
`git pull --all`
`/opt/splunk/git/SHC/Automation-Scripts/automated-apply-script.sh`

#Search Head BCP copy script
`#!/usr/bin/bash`
`GIT_PATH="/opt/splunk/git/ICM_Backup"`
`BACKUP_PATH="/opt/splunk/git/previous_backup/"`
`DEST_PATH="/opt/splunk"`
`SOURCE_BRANCH="ICM_APAC_ap1436l015"`
`declare -A BCP_COPY_ARRAY=( `	`["${GIT_PATH}/apps"]="${DEST_PATH}/etc/apps"`
`["${GIT_PATH}/master-apps"]="${DEST_PATH}/etc/master-apps"`			
`["${GIT_PATH}/system/local"]="${DEST_PATH}/etc/system/local"`
`)`
`cd ${GIT_PATH}`
`git checkout ${SOURCE_BRANCH}`
`pwd`
`git pull`
`#backup`
`for LOCATION in "${!BCP_COPY_ARRAY[@]}"`
`do`
`	cp -rf "${BCP_COPY_ARRAY[${LOCATION}]}" "${BACKUP_PATH}"`
`done`
` `
`#overwrite`
`for LOCATION in "${!BCP_COPY_ARRAY[@]}"`
`do`
	`rm -rf "${BCP_COPY_ARRAY[${LOCATION}]}"`
	`cp -rf "${LOCATION}" "${BCP_COPY_ARRAY[${LOCATION}]}"`
`done`

#Deployment Server Sync Script
`#!/bin/bash`
`GIT_DIR="/opt/splunk/git/DS"`
`APP_DIR="/opt/splunk/etc/deployment-apps"`
`SERVER_CLASS_PATH="/opt/splunk/etc/system/local/serverclass.conf"`
`TYPE="DS"`
`REGION="EMEA"`
`date`
`echo "checking for configuration updates"`
`cd "${GIT_DIR}"`
`git checkout ${TYPE}_${REGION}`
`rm -fr "${GIT_DIR}"/*`
`cp -r "${APP_DIR}"/* "${GIT_DIR}"`
`mkdir "${GIT_DIR}/ServerClass/"`
`cp "${SERVER_CLASS_PATH}" "${GIT_DIR}/ServerClass/serverclass.conf"`
`git add -A`
`git diff --quiet --cached --exit-code`
`if [ $? -eq 1 ] #if there is a change, commit it.`
`then`
`        echo "test: there is a change"`
`        git commit -m "committing new changes"`
`        git push origin ${TYPE}_${REGION}`
`else`
`        echo "No changes"`
`        git reset`
`fi`


#Heavy Forwarder Sync Script
`#!/bin/bash`
`GIT_DIR=/opt/splunk/git/HF`
`APP_DIR=/opt/splunk/etc/apps`
``HOSTNAME=`cat /etc/hostname` ``
`REGION="APAC"`
`date`
`echo "checking for configuration updates"`
`cd "$GIT_DIR"`
`git checkout HF_${REGION}_${HOSTNAME}`
`rm -fr "$GIT_DIR"/*`
`cp -r "$APP_DIR"/* "$GIT_DIR"`
`git add -A`
`git diff --cached --quiet --exit-code`
`if [ $? -eq 1 ] #if there is a change, commit it.`
`then`
`        echo "test: there is a change"`
`        git commit -m "committing new changes"`
`        git push origin HF_${REGION}_${HOSTNAME}`
`else`
`        echo "No changes"`
`        git reset`
`fi`

#Universal Forwarder Sync Script
`#!/bin/bash`
`GIT_DIR=/opt/splunkforwarder/git/UF`
`APP_DIR=/opt/splunkforwarder/etc/apps`
`REGION="APAC"`
``HOSTNAME=`hostname` ``
`declare -A SYSTEM_CONFIG_ARRAY=(      ` `["/etc/rsyslog.conf"]="${GIT_DIR}/RSyslog/"`
`["/etc/rsyslog.d/remote.conf"]="${GIT_DIR}/RSyslog/"`                                       `["/etc/logrotate.d/"]="${GIT_DIR}/LogRotate"`
`                        	)`
`date`
`echo "checking for configuration updates"`
`cd "$GIT_DIR"`
`git checkout UF_${REGION}_${HOSTNAME}`
`rm -fr "$GIT_DIR"/*`
`cp -r "$APP_DIR"/* "$GIT_DIR"`
`for CONFIG in "${!SYSTEM_CONFIG_ARRAY[@]}"`
`do`
`	mkdir -p "${SYSTEM_CONFIG_ARRAY[${CONFIG}]}"`
`	cp -rf "${CONFIG}" "${SYSTEM_CONFIG_ARRAY[${CONFIG}]}"`
`done`
`git add -A`
`git diff --cached --quiet --exit-code`
`if [ $? -eq 1 ] #if there is a change, commit it.`
`then`
`        echo "test: there is a change"`
`        git commit -m "committing new changes"`
`        git push origin UF_${REGION}_${HOSTNAME}`
`else`
`        echo "No changes"`
`        git reset`
`fi`


#Deployment Server Backup Script
`#!/bin/bash`
`GIT_DIR=/opt/splunk/git/DS_Backup`
`PATH_DIR=/opt/splunk/etc/`
``HOSTNAME=`hostname` ``
`REGION="APAC"`
`date`
`echo "checking for configuration updates"`
`cd "$GIT_DIR"`
`git checkout DS_${REGION}_${HOSTNAME}`
`rm -fr "$GIT_DIR"/*`
`cp -r "$PATH_DIR"/* "$GIT_DIR"`
`git add -A`
`git diff --cached --quiet --exit-code`
`if [ $? -eq 1 ] #if there is a change, commit it.`
`then`
`        echo "test: there is a change"`
`        git commit -m "committing new changes"`
`        git push origin DS_${REGION}_${HOSTNAME}`
`else`
`        echo "No changes"`
`        git reset`
`fi`

#Indexer Cluster Master Server Backup Script
`#!/bin/bash`
`GIT_DIR=/opt/splunk/git/ICM_Backup`
`PATH_DIR=/opt/splunk/etc/`
``HOSTNAME=`hostname` ``
`REGION="APAC"`
`date`
`echo "checking for configuration updates"`
`cd "$GIT_DIR"`
`git checkout ICM_${REGION}_${HOSTNAME}`
`rm -fr "$GIT_DIR"/*`
`cp -r "$PATH_DIR"/* "$GIT_DIR"`
`git add -A`
`git diff --cached --quiet --exit-code`
`if [ $? -eq 1 ] #if there is a change, commit it.`
`then`
`        echo "test: there is a change"`
`        git commit -m "committing new changes"`
`        git push origin ICM_${REGION}_${HOSTNAME}`
`else`
`        echo "No changes"`
`        git reset`
`fi`

#Search Head Server Backup Script
`#!/bin/bash`
`GIT_DIR=/opt/splunk/git/SH`
`PATH_DIR=/opt/splunk/etc/`
``HOSTNAME=`hostname` ``
`REGION="APAC"`
`date`
`echo "checking for configuration updates"`
`cd "$GIT_DIR"`
`git checkout SH_${REGION}_${HOSTNAME}`
`rm -fr "$GIT_DIR"/*`
`cp -r "$PATH_DIR"/* "$GIT_DIR"`
`git add -A`
`git diff --cached --quiet --exit-code`
`if [ $? -eq 1 ] #if there is a change, commit it.`
`then`
`        echo "test: there is a change"`
`        git commit -m "committing new changes"`
`        git push origin SH_${REGION}_${HOSTNAME}`
`else`
`        echo "No changes"`
`        git reset`
`fi`

#Cron Time Change Update Script

`#!/bin/bash`
`CRON_DAY="1,3,5"`
`CRON_MINUTE=15`
`CRON_HOUR_STANDARD=5`
`let CRON_HOUR_SAVINGS=${CRON_HOUR_STANDARD}+1`
`SCRIPT_PATH="/opt/splunk/git/update_repo.sh"`
`LOG_PATH="/opt/splunk/git/sync.log"`
`STANDARD_TIME="EST"`
``CURRENT_TIME=`TZ="America/New_York" date | awk -F " " '{print `$5}'` ``
`if [[ "${STANDARD_TIME}" == "${CURRENT_TIME}" ]]`
`then `
`	CRON_HOUR=${CRON_HOUR_STANDARD}`
`else `
`	CRON_HOUR=${CRON_HOUR_SAVINGS}`
`fi`
`CRON_LINE="${CRON_MINUTE} ${CRON_HOUR} * * $CRON_DAY $SCRIPT_PATH >> ${LOG_PATH} 2>&1" `
`(crontab -l | grep -v "${SCRIPT_PATH}"; echo "${CRON_LINE}") | crontab - `

##Search Head Member Scripts

#Metadata Clearing Script 
This script wipes the metadata data in the specified applications before each change window. 
`#!/bin/bash`
`APPS_DIR="/opt/splunk/etc/apps"`
`while read LINE; do`
`sed -i '/^access.*/d' $APPS_DIR/$LINE/metadata/local.meta`
`done < /opt/splunk/etc/apps/Automation-Scripts/local_metadata_clear_app_list.txt`

#Saved Search Clearing Script
This script wipes the local saved search configuration in the specified applications before each change window, preserving only stanza names and enabled/disabled status. 
`#!/bin/bash`
`APPS_DIR="/opt/splunk/etc/apps"`
`while read LINE; do`
`mv $APPS_DIR/$LINE/local/savedsearches.conf $APPS_DIR/$LINE/local/savedsearches.conf.bak`
`grep '^\(\[.*\]\|disabled.*\)' $APPS_DIR/$LINE/local/savedsearches.conf.bak > $APPS_DIR/$LINE/local/savedsearches.conf`
done < /opt/splunk/etc/apps/Automation-Scripts/local_savedsearches_clear_app_list.txt`

#Whitelisted Custom Savedsearch Reaper
Removes all custom saved searches from user directories except for those in the launcher, search, or Splunk ESS apps. 
`#!/bin/bash`
`SPLUNK_USER_DIR=/opt/splunk/etc/users`
`cd $SPLUNK_USER_DIR`
`find . -regex ".*savedsearches.conf" -print0 | xargs -0 -I filepath cp --parents filepath ~/user_backups`
`if [ $? -eq 0 ]`
`then`
`find . -regex ".*savedsearches.conf" | grep "/search/\|SplunkEnterpriseSecuritySuite\|launcher" | grep -v "a-" | xargs -d '\n' -I filepath rm filepath`
`else`
`            echo "could not copy, did not remove old files"`
`fi`

#All Custom Savedsearch Reaper
Removes all custom saved searches from user directories including those in the launcher, search, and Splunk ESS apps. 
`#!/bin/bash`
`SPLUNK_USER_DIR=/opt/splunk/etc/users`
`cd $SPLUNK_USER_DIR`
`find . -regex ".*savedsearches.conf" -print0 | xargs -0 -I filepath cp --parents filepath ~/user_backups`
`if [ $? -eq 0 ]`
`then`
`find . -regex ".*savedsearches.conf" | grep -v "a-" | xargs -d '\n' -I filepath rm filepath`
`else`
`            echo "could not copy, did not remove old files"`
`fi`

#Restart firewalld on AWS/Azure IP Forwarders
The script will restart firewalld every 12 hours and after a reboot to fix the issues with the UF data ingests going down in the Azure/AWS environments due to firewalld not properly running on the IP Forwarders. 
`#!/bin/sh`
`systemctl restart firewalld`

See #101052 for more details. 