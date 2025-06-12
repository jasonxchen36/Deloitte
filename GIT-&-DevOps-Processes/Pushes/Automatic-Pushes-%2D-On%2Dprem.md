**Features**

The following entry purpose is to explain how the automatic pushes process works in Development and Staging environments.

**Process**

It consists on creating a tag and pushing the changes to the respective SHC or ICM.

It could be executed manually by running a custom bash script called **manual_push.sh** located at *Splunk service user*'s home. The prompt result will be logged as well.

[[_TOC_]]

# Automatic Pushes

## 1. Loging events
The process output will be ingested into:

### 1.1. Index
 - Index: *dttl_internal*_***region***

### 1.2. Source
 - Sources: 
   - *tag_creation* 
   or
   - *bundle_push*

## 2. Development
It will be executed every day from Monday to Friday.

## 3. Staging
It will be executed every Monday, Wednesday and Friday.
There is only SHC in Staging.

## 4. Code
There is an app deployed into the Cluster Master and/or Deployer called:
- ***region***_*bundle_push*

The first two inputs will run the tag_creation.sh and bundle_push.sh scripts, the other two will monitor the output of the scripts.

The scripts run are the usual scripts that we use during our manual push.

The frequency of these pushes can be checked in the management servers under:
- */opt/splunk/etc/apps/****region****_bundle_push/local/inputs.conf*

In order to check the outputs of the push, the following search can be run in the according environment SHs:
- *index=dttl_internal*_***region*** *source=bundle_push OR source=tag_creation*

### 4.2. Development
#### - local/inputs.conf (example 1)

> [script://./bin/bundle_push.sh]
disabled = 0
interval = 00 15 * * 1,2,3,4,5
passAuth = admin

>[script://./bin/tag_creation.sh]
disabled = 0
interval = 30 14 * * 1,2,3,4,5
passAuth = admin

>[monitor:///opt/splunk/git/bundle_push.log]
disabled = 0
index = dttl_internal_amer
host = amer_dev_deployer
source = bundle_push

>[monitor:///opt/splunk/git/tag_creation.log]
disabled = 0
index = dttl_internal_amer
host = amer_dev_deployer
source = tag_creation

#### - bin/tag_creation.sh (example 1)

```bash
#!/bin/bash

# Dynamic VARIABLE DECLARATION
TYPE="SHC"                                                  # SHC or ICM
LOCATION="AMER_DEV"                                         # REGION[_DEPLOYMENT][_ENVIRONMENT]
GIT_PATH="/opt/splunk/git/"                                 #

# Static VARIABLE DECLARATION
LOG_FILE="${GIT_PATH}tag_creation.log"                      #
BRANCH_NAME="${TYPE}_${LOCATION}"                           #
TAG_NAME="${BRANCH_NAME}_`date +%Y%m%d`"                    #
CommitID="HEAD"                                             #
[[ $TYPE == "SHC" ]] && GIT_REPO="${GIT_PATH}SHC" || {      # Selects local git repository
[[ $TYPE == "ICM" ]] && GIT_REPO="${GIT_PATH}IndexerCM"; }  #

# MAIN PROGRAM
exec &>> ${LOG_FILE} 2>&1                                   # Logging script
echo ">>> TAG_CREATION on:" `date`                          # Initial log
cd ${GIT_REPO}                                              # Changing to local git directory
CURRENT_BRANCH=`git rev-parse --abbrev-ref ${CommitID}`     # Getting current branch name
echo ">>> Was on branch ${CURRENT_BRANCH}"                  #
echo ">>> Changing to branch:" ${BRANCH_NAME}               #
git checkout ${BRANCH_NAME}                                 # Change to server branch
LOCAL_HASH=`git rev-parse ${CommitID}`                      # Getting current branch hash BEFORE updating

git fetch origin                                             #

echo ">>> LOCAL BRANCH HASH: " ${LOCAL_HASH}                #
REMOTE_HASH=`git rev-parse origin/${BRANCH_NAME}`           # Getting current branch hash AFTER updating
echo ">>> REMOTE BRANCH HASH:" ${REMOTE_HASH}               #
if [[ "$LOCAL_HASH" == "$REMOTE_HASH" ]]; then              # Compare if there are changes
    echo ">>> No changes in REMOTE branch. Tag will not be created."
else
    echo ">>> Changes in REMOTE branch. Tag is going to be created"
    if [[ "$(git tag -l $TAG_NAME)" == "$TAG_NAME" ]]; then   # Check if Tag exist
        echo ">>> Tag already exist."
    else
        echo ">>> Refreshing repository from Azure DevOps"
        git pull
        git tag -a ${TAG_NAME} ${CommitID} -m "automation tag for ${BRANCH_NAME}"
        git push origin ${TAG_NAME} && echo ">>> Tag successfully pushed to DevOps." || echo ">>> Tag Push failed."
    fi
fi
echo ">>> Returning to previous branch: ${CURRENT_BRANCH}."
git checkout -q ${CURRENT_BRANCH}
echo "<<< FINISH"
```
#### - bin/bundle_push.sh (example 1)
```bash
#!/bin/bash

# Dynamic VARIABLE DECLARATION
TYPE="SHC"                                                  # SHC or ICM
LOCATION="AMER_DEV"                                         # REGION[_DEPLOYMENT][_ENVIRONMENT]
GIT_PATH="/opt/splunk/git/"                                 #
TARGET_SERVER="https://usatramekj047.atrame.deloitte.com:8089" # In case of SHC, SH from location

# Static VARIABLE DECLARATION
LOG_FILE="${GIT_PATH}bundle_push.log"                       #
BRANCH_NAME="${TYPE}_${LOCATION}"                           #
TAG_NAME="${BRANCH_NAME}_`date +%Y%m%d`"                    #
CommitID="HEAD"                                             #
[[ $TYPE == "SHC" ]] \
    && { GIT_REPO="${GIT_PATH}SHC/"                         #
    DEST_DIR="/opt/splunk/etc/shcluster/apps/"              #
    SCRIPT_DIR="${DEST_DIR}Automation-Scripts/"              #
    APPLY_COMMAND="/opt/splunk/bin/splunk apply shcluster-bundle --answer-yes -target ${TARGET_SERVER} -preserve-lookups true -push-default-apps true"; }
[[ $TYPE == "ICM" ]] \
    && { GIT_REPO="${GIT_PATH}IndexerCM/"                   #
    DEST_DIR="/opt/splunk/etc/master-apps/"                 #
    SCRIPT_DIR="${DEST_DIR}AutomatedScripts/"               #
    APPLY_COMMAND="/opt/splunk/bin/splunk apply cluster-bundle --answer-yes"; }
BACKUP_DIR="${GIT_PATH}previous_push/"                      #

# Function DECLARATIONS
function Update_Deployed_Version {
    TAG_ID=`git rev-list -n 1 ${TAG_NAME} | cut -c 1-8`     # have to get the ID before we leave the git directory
    echo ">>> Updating tag ID: ${TAG_ID}"                   # put the commitID into the build ID
    sed -i "s|APPLIED_BUILD_ID|${TAG_ID}|g" ${SCRIPT_DIR}default/app.conf
}

function Update_Splunk_Configuration {
    echo ">>> Configuration backup complete, updating live configuration."
    rm -r ${DEST_DIR}*
    if cp -r $GIT_REPO* $DEST_DIR; then
        Update_Deployed_Version
        echo ">>> Configuration updated, applying package..."
        eval SPLUNK_TOK=$tok ${APPLY_COMMAND} || echo ">>> Cannot run  as Splunk Admin"
    else
        echo ">>> Copy command failed, aborting deploy. Your update has not been deployed"
        cp -r ${BACKUP_DIR}* ${DEST_DIR} \
            && echo ">>> Rollback appeared to work. Please double-check your configuration files." \
            || echo ">>> Attempted rollback failed. Please manually repair the configuration directory. Your previous configuration is located at ${BACKUP_DIR}."
    fi
}

# MAIN PROGRAM
exec &>> ${LOG_FILE} 2>&1                                   # Logging script
echo ">>> BUNDLE_PUSH on:" `date`                           # Initial log
cd ${GIT_REPO}                                              # Changing to git directory
CURRENT_BRANCH=`git rev-parse --abbrev-ref ${CommitID}`     # Getting current branch name
echo ">>> Was on branch ${CURRENT_BRANCH}"                  #
echo ">>> Fetching remote branch:" ${BRANCH_NAME}           #
git checkout ${BRANCH_NAME}                                 # Change to server branch
echo ">>> Checking out release tag (${TAG_NAME})"
if [[ "$(git tag -l $TAG_NAME)" == "$TAG_NAME" ]]; then     # Check if Tag exist
    echo ">>> Tag ${TAG_NAME} found successfully."
    echo ">>> Backing up current configuration to ${BACKUP_DIR}"
    rm -r ${BACKUP_DIR}*
    cp -r ${DEST_DIR}* ${BACKUP_DIR} \
        && { read tok; Update_Splunk_Configuration; } \
        || echo ">>> Copy command failed, aborting deploy. Your deployment directory has not been modified."
else
    echo ">>> Tag ${TAG_NAME} not found."
fi
echo ">>> Returning to previous branch: ${CURRENT_BRANCH}."
git checkout -q ${CURRENT_BRANCH}
echo "<<< FINISH"
```
#### - manual_push.sh
```bash
#!/bin/bash
#
# Dynamic VARIABLE DECLARATION
declare -r TYPE="SHC"                                                  # SHC or ICM
declare -r LOCATION="AMER_DEV"                                         # REGION[_DEPLOYMENT][_ENVIRONMENT]
declare -r GIT_PATH="/opt/splunk/git/"                                 #
declare -r TARGET_SERVER="https://usatramekj047.atrame.deloitte.com:8089" # In case of SHC, SH from location 
#
# Static VARIABLE DECLARATION
declare -r LOG_FILE="${GIT_PATH}manual_push.log"                       #
declare -r TAG_LOG_FILE="${GIT_PATH}tag_creation.log"                  #
declare -r BUNDLE_LOG_FILE="${GIT_PATH}bundle_push.log"                #
declare -r BRANCH_NAME="${TYPE}_${LOCATION}"                           #
declare -r TAG_NAME="${BRANCH_NAME}_`date +%Y%m%d`"                    #
declare -r CommitID="HEAD"                                             #
[[ $TYPE == "SHC" ]] \
    && { declare -r GIT_REPO="${GIT_PATH}SHC/"                         #
    declare -r DEST_DIR="/opt/splunk/etc/shcluster/apps/"              #
    declare -r SCRIPT_DIR="${DEST_DIR}Automation-Scripts/"             #
    declare -r APPLY_COMMAND="/opt/splunk/bin/splunk apply shcluster-bundle --answer-yes -target ${TARGET_SERVER} -preserve-lookups true -push-default-apps true"; }
[[ $TYPE == "ICM" ]] \
    && { declare -r GIT_REPO="${GIT_PATH}IndexerCM/"                   #
    declare -r DEST_DIR="/opt/splunk/etc/master-apps/"                 #
    declare -r SCRIPT_DIR="${DEST_DIR}AutomatedScripts/"               #
    declare -r APPLY_COMMAND="/opt/splunk/bin/splunk apply cluster-bundle --answer-yes"; }
declare -r BACKUP_DIR="${GIT_PATH}previous_push/"                      #
#
# Function DECLARATIONS
function getId {
    USER_ID=$(who am i | awk {'print $1'})
}
#
function tagCreation {
    {
        echo ">>> Manual TAG_CREATION by ${USER_ID} on:" `date`     # Initial log
        cd ${GIT_REPO}                                              # Changing to local git directory
        current_branch=`git rev-parse --abbrev-ref ${CommitID}`     # Getting current branch name
        echo ">>> Was on branch ${current_branch}"                  #
        echo ">>> Changing to branch:" ${BRANCH_NAME}               #
        git checkout ${BRANCH_NAME}                                 # Change to server branch
        local_hash=`git rev-parse ${CommitID}`                      # Getting current branch hash BEFORE updating
        git fetch origin                                            #
        echo ">>> LOCAL BRANCH HASH: " ${local_hash}                #
        remote_hash=`git rev-parse origin/${BRANCH_NAME}`           # Getting current branch hash AFTER updating
        echo ">>> REMOTE BRANCH HASH:" ${remote_hash}               #
        if [[ "$local_hash" == "$remote_hash" ]]; then              # Compare if there are changes
            echo ">>> No changes in REMOTE branch. Tag will not be created."
        else
            echo ">>> Changes in REMOTE branch. Tag is going to be created"
            echo ">>> Refreshing repository from Azure DevOps"
            git pull
            git tag -a ${TAG_NAME} ${CommitID} -m "manual tag for ${BRANCH_NAME} by ${USER_ID}" 
            git push origin ${TAG_NAME} && echo ">>> Tag successfully pushed to DevOps." || echo ">>> Tag Push failed."
        fi
        echo ">>> Returning to previous branch: ${current_branch}."
        git checkout -q ${current_branch}
        echo "<<< FINISH"
    } | tee ${TAG_LOG_FILE}
}
#
function bundlePush {
    {
        echo ">>> Manual BUNDLE_PUSH by ${USER_ID} on:" `date`          # Initial log
        cd ${GIT_REPO}                                              # Changing to git directory
        current_branch=`git rev-parse --abbrev-ref ${CommitID}`     # Getting current branch name
        echo ">>> Was on branch ${current_branch}"                  #
        echo ">>> Fetching remote branch:" ${BRANCH_NAME}           #
        git checkout ${BRANCH_NAME}                                 # Change to server branch
        echo ">>> Checking out release tag (${TAG_NAME})"
        if [[ "$(git tag -l $TAG_NAME)" == "$TAG_NAME" ]]; then     # Check if Tag exist
            echo ">>> Tag ${TAG_NAME} found successfully."
            echo ">>> Backing up current configuration to ${BACKUP_DIR}"
            rm -r ${BACKUP_DIR}* 
            cp -r ${DEST_DIR}* ${BACKUP_DIR}
            if [ $? -eq 0 ]; then
                echo ">>> Configuration backup complete, updating live configuration."
                rm -r ${DEST_DIR}*
                if cp -r $GIT_REPO* $DEST_DIR; then
                    TAG_ID=`git rev-list -n 1 ${TAG_NAME} | cut -c 1-8`     # have to get the ID before we leave the git directory
                    echo ">>> Updating tag ID: ${TAG_ID}"                   # put the commitID into the build ID
                    sed -i "s|APPLIED_BUILD_ID|${TAG_ID}|g" ${SCRIPT_DIR}default/app.conf
                    echo ">>> Configuration updated, applying package..."
                    ${APPLY_COMMAND} || echo ">>> Cannot run as Splunk Admin"
                else 
                    echo ">>> Copy command failed, aborting deploy. Your update has not been deployed"
                    cp -r ${BACKUP_DIR}* ${DEST_DIR} \
                        && echo ">>> Rollback appeared to work. Please double-check your configuration files." \
                        || echo ">>> Attempted rollback failed. Please manually repair the configuration directory. Your previous configuration is located at ${BACKUP_DIR}."
                fi
            else
                echo ">>> Copy command failed, aborting deploy. Your deployment directory has not been modified."
            fi
        else
            echo ">>> Tag ${TAG_NAME} not found."
        fi
        echo ">>> Returning to previous branch: ${current_branch}."
        git checkout -q ${current_branch}
        echo "<<< FINISH" 
    } | tee ${BUNDLE_LOG_FILE}
}
#
# MAIN PROGRAM
{
    getId                                                      # Get the name of the user who run it
    tagCreation
    sleep 5
    bundlePush
} | tee ${LOG_FILE}
```

------------

### 4.2. Staging
#### - local/inputs.conf (example 2)
>[script://./bin/bundle_push.sh]
disabled = 0
interval = 00 15 * * 1,2,3,4,5
passAuth = admin

>[script://./bin/tag_creation.sh]
disabled = 0
interval = 30 14 * * 1,2,3,4,5
passAuth = admin

>[monitor:///opt/splunk/git/bundle_push.log]
disabled = 0
index = dttl_internal_amer
host = amer_staging_deployer
source = bundle_push

>[monitor:///opt/splunk/git/tag_creation.log]
disabled = 0
index = dttl_internal_amer
host = amer_staging_deployer
source = tag_creation

#### - bin/tag_creation.sh (example 2)
```bash
#!/bin/bash

#Log file
exec &>> /opt/splunk/git/tag_creation.log 2>&1

#Set the log timestamp
date

#Changing to git directory
GIT_DIRECTORY="/opt/splunk/git/SHC"
cd ${GIT_DIRECTORY}

#VARIABLE DECLARATION
CURRENT_BRANCH=`git rev-parse --abbrev-ref HEAD`
TYPE="SHC"
LOCATION="AMER_STAGING"
BRANCH_NAME="${TYPE}_${LOCATION}"
CommitID="HEAD"
TAG_DATE=`date +%Y%m%d`
TAG_NAME="${BRANCH_NAME}_${TAG_DATE}"

#Get the last local branch commit ID
LOCAL=`git rev-parse HEAD`

#Download the remote branch
git checkout ${BRANCH_NAME}
git pull
echo "Fetched remote branch "$BRANCH_NAME

#Get the last commit ID of local branch after merging the changes of remote branch
REMOTE=`git rev-parse HEAD`

echo "Tag creation"
echo "REMOTE BRANCH:"$REMOTE
echo "LOCAL BRANCH:"$LOCAL
if [[ "$LOCAL" = "$REMOTE" ]];
then
    echo "No changes in REMOTE branch. Tag will not be created"
else
    git tag -a ${TAG_NAME} ${CommitID} -m "automation tag for ${BRANCH_NAME}"
    git push origin ${TAG_NAME}
    if [ $? -ne 0 ]
        then
            echo "Tag Push failed"
        else
            echo "Tag successfully pushed to DevOps."
            echo "Returning you to your previous branch: ${CURRENT_BRANCH}."
            git checkout -q ${CURRENT_BRANCH}
    fi
fi
```

#### - bin/bundle_push.sh (example 2)
```bash
#!/bin/bash
#This script is intended to be run as a post-merge hook during the git pull process
#To do so, put this script in the $GIT_DIRECTORY/.git/hooks directory with the file name
# "post-merge" (no extension), and configure the variables below to suit your needs.

#Log file
exec &>> /opt/splunk/git/bundle_push.log 2>&1

#Set the log timestamp
date

#Changing to git directory
GIT_DIRECTORY="/opt/splunk/git/SHC"
cd ${GIT_DIRECTORY}

#VARIABLE DECLARATION
CURRENT_BRANCH=`git rev-parse --abbrev-ref HEAD`
GIT_DIRECTORY="/opt/splunk/git/SHC"
DEST_DIR="/opt/splunk/etc/shcluster/apps"
SCRIPT_DIR="${DEST_DIR}/Automation-Scripts"
BACKUP_DIR="/opt/splunk/git/previous_push"
TYPE="SHC"
LOCATION="AMER_STAGING"
DATE="`date +%Y%m%d`"
TAG_NAME="${TYPE}_${LOCATION}_${DATE}"
TARGET_SERVER="https://usatramekj034.atrame.deloitte.com:8089"
APPLY_COMMAND="/opt/splunk/bin/splunk apply shcluster-bundle --answer-yes -target ${TARGET_SERVER} -preserve-lookups true -push-default-apps true"

#Function Declarations
function Update_Deployed_Version {
        #have to get the ID before we leave the git directory
        TAG_ID=`git rev-list -n 1 ${TAG_NAME} | cut -c 1-8`
        cd ${SCRIPT_DIR}/default
        #get the commitID
        echo ${TAG_ID}
        #put the commitID into the build ID
        sed -i "s|APPLIED_BUILD_ID|${TAG_ID}|g" app.conf
        cd -
}

function Update_Splunk_Configuration {
        echo "Configuration backup complete, updating live configuration."
        rm -r ${DEST_DIR}/*
        cp -r ${GIT_DIRECTORY}/* ${DEST_DIR}/
        if [ $? -eq 0 ]
        then
                Update_Deployed_Version
                echo "Configuration updated, applying package..."
                eval SPLUNK_TOK=$tok ${APPLY_COMMAND}
                if [ $? -eq 0 ]
                then
                        echo "Configuration applied successfully."
                else
                        echo "Apply failed, check the Splunk logs for more information."
                fi
        else
                echo "Configuration update failed, attempting to roll back."
                echo "Your update has not been deployed."
                cp -r ${BACKUP_DIR}/* ${DEST_DIR}/
                if [ $? -eq 0 ]
                then
                        echo "Rollback appeared to work. Please double-check your configuration files."
                else
                        echo "Attempted rollback failed. Please manually repair the configuration directory."
                        echo "Your previous configuration is located at ${BACKUP_DIR}."
                fi
        fi
}

############## MAIN #############################

#Move to the working folder and check out the tag we want to push out.
read tok
echo "Refreshing repository from Azure DevOps"
git pull --all
echo "Was on branch ${CURRENT_BRANCH}, checking out release tag (${TAG_NAME})"
git pull origin ${TAG_NAME}
git checkout -q ${TAG_NAME}
if [ $? -ne 0 ]
then
        echo "Failed to checkout tag ${TAG_NAME}, aborting"
        exit
else
        echo "Checked out tag (${TAG_NAME}) successfully."
fi

#backup old working files
echo "Backing up current configuration to ${BACKUP_DIR}"
rm -r ${BACKUP_DIR}/*
cp -r ${DEST_DIR}/* ${BACKUP_DIR}/
if [ $? -eq 0 ]
then
        Update_Splunk_Configuration
else
        echo "Copy command filed, aborting deploy. Your deployment directory has not been modified."
fi
echo "Checking out the branch from before the deployment (${CURRENT_BRANCH})"
git checkout -q ${CURRENT_BRANCH}
```

------------

**End**