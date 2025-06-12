The steps below describe how to integrate the Splunk servers in AWS and Azure into DevOps.

**Note:** You must submit a firewall request to allow the connection to ssh.dev.azure.com on port 22 over the internet before starting the process.

## **Generate RSA Key Pair**
			
	1. Install git using root privleges (type "y" when it ask if it this ok):
		sudo yum install git
		
	2. Sudo to the Splunk service account:
		Production servers
		sudo su - dtt_sc_splunk_prd

		Development servers
		sudo su - dtt_sc_splunk_qa
		
	3. Generate RSA key pairs (hit enter to skip the file path location and passphrase):
		ssh-keygen -t rsa
		
	4. Change to the .ssh directory:
		cd .ssh

	5. Verify public key is generated and to copy "authorized_keys" by using the command:
		cat id_rsa.pub > authorized_keys
		
	6. Share and distribute the key pairs:
		eval "$(ssh-agent -s)"
		
	7. Add the SSH private key:
		ssh-add ~/.ssh/id_rsa
		
	8. Change the permissions of the ".ssh" directory and files:
		chmod 700 ~/.ssh
		chmod 644 ~/.ssh/authorized_keys
		chmod 600 ~/.ssh/id_rsa
		chmod 644 ~/.ssh/id_rsa.pub
	
    9. View the public key and add it to DevOps using the GUI (under User icon > Security > SSH public key):
		cat id_rsa.pub

    10. Email the public keys to Antonio Rojas so he can add them to DevOps.
		

---
## **Clone Repo and Create Branches**
    1. Verify the SSH connection to DevOps is working by using this debug/verbose command:
		ssh -vT git@ssh.dev.azure.com

    2. Add the DevOps public key to the "known_host" file:
		ssh-keyscan -t rsa ssh.dev.azure.com >> ~/.ssh/known_hosts

	3. Navigate to the home directory:
		Production servers
		cd /home/dtt_sc_splunk_prd

		Development servers
		cd /home/dtt_sc_splunk_qa

	4. Clone the DevOps repository to the server:
		Cluster Master
		git clone git@ssh.dev.azure.com:v3/GlobalSOC/Splunk/IndexerCM
	 
		Cluster Master (Backup)
		git clone git@ssh.dev.azure.com:v3/GlobalSOC/Splunk/ICM_Backup

		Search Head Cluster
		git clone git@ssh.dev.azure.com:v3/GlobalSOC/Splunk/SHC

		Deployment Server
		git clone git@ssh.dev.azure.com:v3/GlobalSOC/Splunk/DS

		Deployment Server (Backup)
		git clone git@ssh.dev.azure.com:v3/GlobalSOC/Splunk/DS_Backup

		Heavy Forwarder (Cloud)
		git clone git@ssh.dev.azure.com:v3/GlobalSOC/Splunk/HF_Cloud

	5. Change to the DevOps branch directory:
		Cluster Master
		cd IndexerCM

		Search Head Cluster
		cd SHC

		Deployment Server
		cd DS

		Heavy Forwarder (Cloud)
		cd HF_Cloud

	6. Create a new local branch and check it out:
		Cluster Master
		git checkout -b ICM_AMER_AZURE
		git checkout -b ICM_AMER_AWS
		git checkout -b ICM_EMEA_AZURE
		git checkout -b ICM_EMEA_AWS
		git checkout -b ICM_APAC_AZURE
		git checkout -b ICM_APAC_AWS

		Deployment Server
		git checkout -b DS_AMER_AZURE
		git checkout -b DS_AMER_AWS
		git checkout -b DS_EMEA_AZURE
		git checkout -b DS_EMEA_AWS
		git checkout -b DS_APAC_AZURE
		git checkout -b DS_APAC_AWS

		Heavy Forwarder (Cloud)
		git checkout -b HF_AMER_AZURE_<HOSTNAME>
		git checkout -b HF_AMER_AWS_<HOSTNAME>
		git checkout -b HF_EMEA_AZURE_<HOSTNAME>
		git checkout -b HF_EMEA_AWS_<HOSTNAME>
		git checkout -b HF_APAC_AZURE_<HOSTNAME>
		git checkout -b HF_APAC_AWS_<HOSTNAME>

	7. Remove the README file:
		rm -rf README.md

	8. Update apps in the new local branch (e.g. copying Deployment Apps to local branch for DS branch).
 		Deployment Server
		cp -r /opt/splunk/etc/deployment-apps/* /home/dtt_sc_splunk_prd/DS/

		Heavy Forwarder (Cloud)
		cp -r /opt/splunk/etc/apps/* /home/dtt_sc_splunk_prd/HF_Cloud/

	9. Add apps, commit and push the new local branch to DevOps.
		git add -A
		git commit -m "Initial baseline apps."
		git push origin <LOCAL_BRANCH>

	10. Set local branch to track remote branch:
		Cluster Master
		git branch --set-upstream-to=origin/ICM_AMER_AZURE ICM_AMER_AZURE                                                                                              
		git branch --set-upstream-to=origin/ICM_AMER_AWS ICM_AMER_AWS
		git branch --set-upstream-to=origin/ICM_EMEA_AZURE ICM_EMEA_AZURE
		git branch --set-upstream-to=origin/ICM_EMEA_AWS ICM_EMEA_AWS
		git branch --set-upstream-to=origin/ICM_APAC_AZURE ICM_APAC_AZURE
		git branch --set-upstream-to=origin/ICM_APAC_AWS ICM_APAC_AWS

		Deployment Server
		git branch --set-upstream-to=origin/DS_AMER_AZURE DS_AMER_AZURE                                                                                              
		git branch --set-upstream-to=origin/DS_AMER_AWS DS_AMER_AWS
		git branch --set-upstream-to=origin/DS_EMEA_AZURE DS_EMEA_AZURE
		git branch --set-upstream-to=origin/DS_EMEA_AWS DS_EMEA_AWS
		git branch --set-upstream-to=origin/DS_APAC_AZURE DS_APAC_AZURE
		git branch --set-upstream-to=origin/DS_APAC_AWS DS_APAC_AWS

		Heavy Forwarder (Cloud)
		git branch --set-upstream-to=origin/HF_AMER_AZURE_<HOSTNAME> HF_AMER_AZURE_<HOSTNAME>                                                                                              
		git branch --set-upstream-to=origin/HF_AMER_AWS_<HOSTNAME> HF_AMER_AWS_<HOSTNAME>
		git branch --set-upstream-to=origin/HF_EMEA_AZURE_<HOSTNAME> HF_EMEA_AZURE_<HOSTNAME>
		git branch --set-upstream-to=origin/HF_EMEA_AWS_<HOSTNAME> HF_EMEA_AWS_<HOSTNAME>
		git branch --set-upstream-to=origin/HF_APAC_AZURE_<HOSTNAME> HF_APAC_AZURE_<HOSTNAME>
		git branch --set-upstream-to=origin/HF_APAC_AWS_<HOSTNAME> HF_APAC_AWS_<HOSTNAME>

	11. Navigate to the home directory:
		cd /home/dtt_sc_splunk_prd

	12. Add .sh file that refreshes the repository:
		vi update_repo.sh

            Indexers:
		---------------------------------------------
		#!/bin/bash
		date
		echo "Refreshing repository from Azure DevOps"
		cd /home/dtt_sc_splunk_prd/IndexerCM
		git pull --all
		/home/dtt_sc_splunk_prd/IndexerCM/AutomatedScripts/automated-apply-script.sh
		---------------------------------------------

            Heavy Forwarders:
  		---------------------------------------------
		#!/bin/bash
		GIT_DIR=/home/dtt_sc_splunk_prd/HF_Cloud
		APP_DIR=/opt/splunk/etc/apps
		HOSTNAME=`cat /etc/hostname`
		REGION="AMER_AZURE"
		date
            echo "checking for configuration updates"
            cd "$GIT_DIR"
            git checkout HF_${REGION}_${HOSTNAME}
            rm -fr "$GIT_DIR"/*
            cp -r "$APP_DIR"/* "$GIT_DIR"
            git add -A
            git diff --cached --quiet --exit-code
            if [ $? -eq 1 ] #if there is a change, commit it.
            then
                   echo "test: there is a change"
                   git commit -m "committing new changes"
                   git push origin HF_${REGION}_${HOSTNAME}
            else
                   echo "No changes"
                   git reset
            fi
		---------------------------------------------

	13. Change the permissions of the .sh file so it can execute:
		chmod u+x update_repo.sh

	14. Verify the permissions were changed successfully:
		ls -l
		
		---------------------------------------------
		-rwxr--r-- 1 dtt_sc_splunk_prd DTTL Service Accounts 193 Mar 23 17:10 update_repo.sh
		---------------------------------------------

	15. Schedule the cron job using root privileges:
		sudo crontab -e -u dtt_sc_splunk_prd

		Note: Crontab is 15 minutes after the start of the production change window.

	 	AMER (04:15AM UTC Tuesday/Friday):
		15 4 * * 2,5 /home/dtt_sc_splunk_prd/update_repo.sh 2>&1 | tee /home/dtt_sc_splunk_prd/last_run.log >> /home/dtt_sc_splunk_prd/sync.log

	 	EMEA (19:15PM UTC Monday/Thursday):
		15 19 * * 1,4 /home/dtt_sc_splunk_prd/update_repo.sh 2>&1 | tee /home/dtt_sc_splunk_prd/last_run.log >> /home/dtt_sc_splunk_prd/sync.log

	 	APAC (03:15PM UTC Monday/Thursday):
		15 15 * * 1,4 /home/dtt_sc_splunk_prd/update_repo.sh 2>&1 | tee /home/dtt_sc_splunk_prd/last_run.log >> /home/dtt_sc_splunk_prd/sync.log

	16. Generate a pull request to add the automated-apply-script.sh file to the new branch.
		git checkout ICM_EMEA_AZURE
		git pull
		git checkout -b ICM_EMEA_AZURE_automation_script
		git checkout ICM_EMEA_AZURE AutomatedScripts/automated-apply-script.sh
		git status
		vi AutomatedScripts/automated-apply-script.sh
		Modify file by changing LOCATION="EMEA_AZURE"
		git add AutomatedScripts/
		git status
		git commit -m "Initial EMEA Azure automated script"
		git push --set-upstream origin ICM_EMEA_AZURE_automation_script

	17. Confirm the automated-apply-script.sh file is in the local branch:
		cd IndexerCM/AutomatedScripts

		pwd                                                                                              
		---------------------------------------------
		/home/dtt_sc_splunk_prd/IndexerCM/AutomatedScripts
		---------------------------------------------

		ls -l
		---------------------------------------------
		-rwxr-xr-x 1 dtt_sc_splunk_prd DTTL Service Accounts 3956 Mar 23 17:32 automated-apply-script.sh
		---------------------------------------------

	18. Add the DevOps server private key (check with Allen to obtain it):
		vi server_key.pem

	19. Run the tag creation shell script in /home/dtt_sc_splunk_prd/IndexerCM/AutomatedScripts:
		./tag-creation-script.sh

	20. Create a directory called previous_push in /home/dtt_sc_splunk_prd:
		mkdir previous_push

	21. Run the update_repo file shell script in /home/dtt_sc_splunk_prd:
		./update_repo.sh


	
## **Deploy Pull Request Process**
	1. Confirm Pull Requests are approved and marked as completed

	2. Checkout Splunk admin password before running script
		
	3. Run tag creation script on Git Bash
		
	4. Run update repo script on Indexer Cluster Master
		./update_repo.sh
		
	5. Confirm changes were successfully applied by checking the build version on Indexers
		cat /opt/splunk/etc/slave-apps/AutomatedScripts/default/app.conf



## **Troubleshooting**	

Validate that the hosts file does not contain any DevOps IP addresses because the URL is dynamic and will change overtime. We do not want to force the URL ssh.dev.azure.com to use a certain IP address.
`sudo cat /etc/hosts`

**Example Output:**

```
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
10.222.86.4  az1436l012.atrame.deloitte.com az1436l012
```



**Note:** All IP addresses in the "name": "AzureDevOps" section of [this downloadable file](https://www.microsoft.com/download/details.aspx?id=56519) (updated weekly) named: Azure IP ranges and Service Tags - Public Cloud


**Expand Disk Size**
For Azure hosts, some directories are pre-mounted and do not utilized the full disk size capacity. The `home directory` that is mounted may need to be increased. Use the following commands to resize the mounted directory.
```
lsblk
df -h
sudo lvextend -L +2G /dev/mapper/<vg_name>
sudo xfs_growfs -d /dev/mapper/<vg_name>
```