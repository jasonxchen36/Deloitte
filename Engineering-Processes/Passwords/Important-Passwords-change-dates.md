# **dtt_sc_splunk_thyctc** -- Expires  (every 56 Days)
Perform the following steps on usatramekj130 and eu1436l040. This account is in Thycotic remember to use the option "Change password now" this will change the password on the AD.

o	**The credentials added through the UI are stored in passwords.conf. The password is hashed and should not be manually modified. Follow these steps to update the password:**

       "Change password now" in Thycotic to sync with the Active Directory side
	Rename or remove SPLUNK_HOME/etc/apps/TA-thycotic/local/passwords.conf
	Vi or vim SPLUNK_HOME/etc/apps/TA-thycotic/local/app.conf and change is_configured from 1 to 0
	Save the file
	Restart splunkd
	Log into the UI
	Navigate to Apps > Manage Apps
	Select “Set up” next to TA-thycotic
	Enter the username and new password
	Check index "referential_thycotic_identity_all" to see if new logs are coming (index receives data every hour)

# **dtt_sc_splunkldapsvc & dtt_sc_splunkldapdmz** Every (every 56 Days)
Perform the following steps on this servers: AMER SHC (on any server of the cluster), for EMEA on HF az1436l035, for APAC on HF aw1436l036. These accounts are in Thycotic.

o  **The credential must be added through the UI as "Administrator"**:

 "Change password now" in Thycotic to sync with the Active Directory side
 Go to manage apps. On the app "Splunk Supporting Add-on for Active Directory"click on Launch App.
 Go to configuration, at the top menu.
 Update the password on the following connections: **dtt_sc_splunkldapsvc** for deloitte & **dtt_sc_splunkldapdmz** for deloitte_dmz. 
 Click on "check connection" to see if the password is on sync.
 Save

# **jp_sc_gemssql -- Every (every 180 days)**

This password has the auto change activated but it needs to be renewed on DB Connect app on jptyospap0108.atrapa.deloitte.com

# **Azure DevOps Token** -- Every (every year)

(There is another token for account dtt_sc_splk_devopsth which indexes data from threat hunting project - only in EMEA environment)

**Steps to get the new Token:**

 Check out the "atrame.deloitte.com\dtt_sc_splunk_devops" account from Thycotic.
 Open a new browser using that user and password.
 Go to Splunk project page: https://dev.azure.com/GlobalSOC/Splunk
 Go to "User Settings" > "Personal Access Tokens" (on the top right corner).
 The Token should appear there. 

## This must be changed on the Content Private Repository on both scripts and in every azure TA.

**1- The changes on the Content Private Repository must be as the following (performing a PR into the "master" branch):**

https://dev.azure.com/GlobalSOC/Project%20S%20Content%20Private%20Repository/_git/Project%20S%20Content%20Private%20Repository/commit/ce25f9185463cd2097c4651f0cdda8176ef17167?refName=refs%2Fheads%2Fmaster&path=%2FAzure_DevOps_API_Conf_Builder.py&_a=compare

**2- The changes on the addon must be performed on the following servers: usatramekj132 (AMER), az1436l036 (EMEA and APAC) as "Administrator":**

 Go to TA-azure-devops-custom-addon > Configurations
 Update the Token with the new one.