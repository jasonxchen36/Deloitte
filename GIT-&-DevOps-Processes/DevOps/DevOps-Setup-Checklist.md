
[[_TOC_]]


#Setup Process for DevOps Deployment Configuration (Indexer Cluster Master, Search Head Cluster Deployer, DMC)
##The Prerequisites
1. Open the firewall to communicate with the DevOps servers (port 22 to the domain: ssh.dev.azure.com, although typically we need to request an any rule [Port 22 on any destination host] as our FWs usually only support IP filtering) 
2. Install git (on RHEL, use sudo yum install git)
3. create an ssh key for the Splunk service account (generally dtt_sc_splunk_prd) and add it to the DevOps service account (dtt_sc_splunk_devops). 

##Setup DevOps on the server
1. As the service account, clone the repository from DevOps using the SSH URL. Typically, the repository is cloned to the /opt/splunk/git directory. 
2. Navigate into the newly cloned repository, and use git checkout to check out the appropriate branch (e.g. for the Americas search head cluster deployer, checkout SHC_AMER). Perform a "git pull" to make sure the local copy of the branch is up to date. 
3. Review the automated-apply-script.sh script in the Automation-Scripts folder, and make sure that the type, region, email recipients, and other configuration details are correct for the current environment. To make any needed updates, submit a PR to the branch. 
4. Install the repository sync script (see the subpage) and add it to the crontab for the server. Schedule the cron job so it runs during the proscribed change window for the environment you're configuring. This script should do a "git pull" followed by an execution of the automated-apply-script reviewed above. 
5. If the sync script is configured to use encryption (if the automated apply script references openssl), copy the private server key to the /opt/splunk/git directory as server_key.pem, and restrict permissions on the key to the service account. 
6. If the sync script is not configured to use encryption, create an auth.txt file in /opt/splunk/git that contains the required credentials. This file will  have to be updated whenever the admin password is rotated. 

#Setup Process for DevOps Backup Configuration (Deployment Servers, Universal Forwarders, Heavy Forwarders)
##The Prerequisites
1. Open the firewall to communicate with the DevOps servers (port 22 to the domain: ssh.dev.azure.com, although typically we need to request an any rule [Port 22 on any destination host] as our FWs usually only support IP filtering) 
2. Install git (on RHEL, use sudo yum install git)
3. create an ssh key for the Splunk service account (generally dtt_sc_splunk_prd) and add it to the DevOps service account (dtt_sc_splunk_devops). 

##Setup DevOps on the server
1. As the service account, clone the repository from DevOps using the SSH URL. Typically, the repository is cloned to the /opt/splunk/git or /opt/splunkforwarder/git directory. 
2. Navigate into the newly cloned repository, 
3. Use git checkout to check out the appropriate branch (e.g. for the Americas HF, checkout HF_AMER_hostname). Perform a "git pull" to make sure the local copy of the branch is up to date. 
4. Install the repository sync script (see the subpage) and add it to the crontab for the server. 

#Required Approvers
On production branches, we require approval before allowing changes to be made to production systems. Because of the complexity of the environment, several different teams with different expertise is required. A summary of required approvers for each production and staging environment is below: 

##Search Head Cluster

|Approver|Triggering Files/Applications|
|--|--|--|
|Global FC Build Content Team| Any savedsearches.conf changes, All SA-* and DA-ESS Apps, SplunkEnterpriseSecuritySuite, TA-threatconnect, Content Apps, Global_FC Apps|
|Global FC Build Deployment Approvers|All applications that aren't owned by the Build Content Team|
|Global FC Metrics and Analytics Team |All Metrics Apps|
| US SOC Engineering Administrators | All US MF owned applications |
| US Securinox Team | del_prod_audit_SPinsite |
| Global Oversight and Decisions within Splunk | Any change |
| CIM Oversight | Any change to props.conf files |
| Permission Monitoring | Any permission changes (e.g. authorize.conf, authentication.conf, *.meta) |

##Indexer Cluster

|Approver|Triggering Files/Applications|
|--|--|--|
|Global FC Build Deployment Approvers|Any changes|
|Global FC Metrics and Analytics Team |All Metrics Apps|
| Global Oversight and Decisions within Splunk | Any change |
| Global FC Health Monitoring | Any change to indexes.conf |
| Permission Monitoring | Any permission changes (e.g. authorize.conf, authentication.conf, *.meta) |

##Staging Environments

|Approver|Triggering Files/Applications|
|--|--|--|
|Global FC Staging Approvers| Any change to the staging environment|
| Permission Monitoring | All permission changes (e.g. authorize.conf, authentication.conf, *.meta) |