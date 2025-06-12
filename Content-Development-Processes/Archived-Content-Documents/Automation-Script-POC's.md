**Automation Script POC's**

Harsh Mhatre: hmhatre@deloitte.com  
 
Automation Script Overview:

There are two versions of the DevOps content work item to splunk configuration automation script. One is for creating saved search configurations for volume testing of content and another for creating saved searches configuration for production push. 

The latest versions of the scripts are stored in the Project S Content Private Repository here. 

Volume Testing Automation Script: 
The volume testing version of the automation script creates saved search and tags configuration for content to be pushed out for volume testing by the SOC. It creates these configurations for Build Content work items in DevOps in the “Ready for Volume Testing” column of the Global FC Build Content Team Board. As the script creates configurations for volume testing, it sets the ServiceNow Event Creation ARA to disabled. It prefixes “DEV” to the search title and adds “dev” tags to denote that these searches are in the volume testing phase.

Production Push Automation Script:
The volume testing version of the automation script creates saved search and tags configuration for content to be pushed out to production. It creates these configurations for Build Content work items in DevOps in the “Ready for Production” column of the Global FC Build Content Team Board. As the script creates configurations for production, it sets the ServiceNow Event Creation ARA to enabled. It adds “prod” tags to denote that these searches are pushed to production.

Automation Script Setup:

1.	Install Python 3.6 or above and make sure that the PATH environment variable is set, so that python scripts can be executed from any directory on your computer

2.	Download both versions (volume testing and production) of the automation script to a folder of your choice on your computer

3.	Install the Azure DevOps repository: pip install azure-devops

4.	Replace the msrest module installed by the above command in site-packages folder of Python directory, with the custom msrest module from the Project S Content PrivatRepo: A compressed (.zip) version of the custom msrest module can be found here
*Note: this is a custom edit workaround for the certificate verification issue

5.	Install the HTML to Text converter module: pip install html2text

6.	Copy the following 3 files from the Splunk Project S Content Private Repo here to the same directory where you downloaded and stored the two versions of the automation scripts:
a.	exceptions.py
b.	http_logging.py
c.	utils.py

Running the Script:

Once the above setup steps have been followed, you can execute the Script as follows:
 
1.	Launch Terminal/CMD
2.	Navigate to the directory where the two versions of the script are stored
3.	Execute the command: python <script_name>.py 
4.	The script should create two files, a savedsearches.conf and a tags.conf
5.	Copy the saved search stanzas for the saved searches from savedsearches.conf created by the automation scrips and add it to the savedsearches.conf in the appropriate app on Splunk.
6.	Copy the tags stanzas for the searches from the tags.conf created by the automation script and add it to the tags.conf in the same app on Splunk
7.	Once all the required searches and tags have been copied to the appropriate splunk app, create a DevOps pull request to push the changes to the DevOps Splunk Repos
