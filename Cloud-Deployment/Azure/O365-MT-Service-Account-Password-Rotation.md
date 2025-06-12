The purpose of this wiki is to describe how to rotate the password to the O365 MT service account. The password is stored in Thycotic secret server and is set to expire every 56 days.

1. Login to Thycotic using your Deloitte credentials

2. Search for the username "dtt_sc_splunk_o365mt" and click view to checkout the account
![image.png](/.attachments/image-99661816-4a49-43c3-8b0b-e398563808f6.png)

3. Click on the lock icon to view the password and copy it to notepad (temporarily)

4. RDP to the windows server az1436w001.atrame.deloitte.com using your Deloitte privileged credentials (a-account)

5. Run Notepad++ as administrator and open the following files:
- **MT-Report-v4-0-4-Splunk.ps1**
"C:\Program Files\SplunkUniversalForwarder\etc\apps\TA-PowerShell-o365_MT\bin"
- **passwords.conf**
"C:\Program Files\SplunkUniversalForwarder\etc\apps\TA-PowerShell-o365_MT\default"

6. Replace the password found in the files with the updated one in Thycotic and click Save (Ctrl+S)

![image.png](/.attachments/image-53fa96a8-4b2b-44c6-8095-a639b7bb29c1.png)

7. Verify the new password and ingest is functioning correctly by:
- Checking the date has updated from the "lastrun" file in the "C:\Program Files\SplunkUniversalForwarder\etc\apps\TA-PowerShell-o365_MT\bin" directory
- If there any new CSV files for ingest in the "C:\Program Files\SplunkUniversalForwarder\etc\apps\TA-PowerShell-o365_MT\logs" directory.


# Backup TA-PowerShell-o365_MT
Latest version of the `TA-PowerShell-o365_MT` is found on the AMER Azure DS az1436l002 under deployment apps as a backup. The TA cannot be managed by the DS since the script runs off the last_run file which dynamically gets updated so the local UF will always have the latest file.
![image.png](/.attachments/image-5f358dec-9aef-4470-9e68-81748635f969.png)