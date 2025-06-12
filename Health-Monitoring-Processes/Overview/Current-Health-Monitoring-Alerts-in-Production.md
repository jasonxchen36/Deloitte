# **This document provides each of the monitoring alerts we have in place to check for actions run by users, which would impact efficiency of splunk environment.**

**** 
######
######
######
######


**[SecMon - Monitors for Authentications to Splunk GUI using the Admin Account]**
This search will look for authentications to the Splunk GUI using the hard coded Admin account URL

**[SecMon - Monitors for the checkout of the admin password outside change windows]**
This search will look for the checkout of the admin password for our Splunk infrastructure outside of production change windows

**[SecMon - Privileged Account Logins to Splunk]**
This search will look for privileged account logins taken from privileged_users_from_thycotic.csv file and alert when a privileged account is used to login to Splunk

**[SecMon - Clean Command Run on Splunk Backend]**
This search will track users running clean command on the backend of the Splunk

**[SecMon - Start / Stop Command Run on Splunk Backend]**
This search will track users running "splunk start" "splunk stop" on any of the Splunk servers on the command line interface

**[SecMon - Configuration File Removed on Splunk Backend]**
This search will monitor users running "rm" command on backend to delete files.

**[SecMon - Collect Command Run in SPL-Global]**
This search will monitor users running collect or tscollect command on the GUI

**[SecMon - Splunk Backend Session Opened by User]**
This search will track any users who SSH to Splunk Backend.

**[SecMon - Root Session Opened]**
Detects users using sudo command to open up a session as root user

**[SecMon - Outputlookup Command Run in SPL]**
Use case to monitor usage of the outputlookup command in Splunk GUI

**[SecMon - Splunk Content Edited in GUI]**
Use case to detect when Splunk content is edited in GUI

**[SecMon - Shutdown Command Run on Splunk Backend]**
Use case to monitor for usage of the "shutdown" command on command line interface.

**[SecMon - Third Party Software Installed on Splunk]**
Use case to monitor for usage of the "Yum" or "RPM" commands.

**[SecMon - User logging in on the Splunk Backend outside of change window]**
Use case to alert when Users logging in on the Splunk Backend outside of change window 

**[SPM - Potential Content Search Issue (FC Apps)]**
Alerts if a saved search is running more frequently than the lowest configured cron (288 searches/24 hours) or if the number of failed saved search attempts is greater than the number of successful saved search attempts.

**[SPM - Saved Search Over 5 minutes]**
Detects savedsearches with an average run time of over 5 minutes

**[SPM - Non-approved acceleration running]**
Acceleration running in non-approved app.

