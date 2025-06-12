**_View the comment box below on the process around Splitting Non-English Windows OS Logs by Environment_**

----------------------------------------

# **Converting Japanese logs into English** 


**Solution 1**

_Please note that Windows Server 2019 Datacenter is the system being used for the steps as shown in the image below_

![windows_server_2019_datacenter.jpg](/.attachments/windows_server_2019_datacenter-e80c34aa-4d3f-41eb-93f1-e7f130b752dd.jpg)

1. Splunk Enterprise 8.0.6 is installed locally

![local install.jpg](/.attachments/local%20install-2195ab95-1398-45fa-837f-fe22d1f06688.jpg)

2. Splunkd Service runs with Local System account

![local_account.jpg](/.attachments/local_account-9ff79ada-be39-45c3-bb19-c8910695890a.jpg)

3. WinEventLog:Security contains Japanese characters

![Japanese_characters.jpg](/.attachments/Japanese_characters-61da6b16-483f-48e9-80d3-0d26515703cf.jpg)

4. Change the Logon Account for Splunkd Service to a local account with lang=English (.\splunk)

![change_local_account.jpg](/.attachments/change_local_account-49f4dd8b-4d52-4ce0-8f62-2610a8989f74.jpg)

5. WinEventLog:Security (SourceName = Microsoft Windows security auditing.) now contains English characters only.

![Winevent_log.jpg](/.attachments/Winevent_log-6acf90a7-6cfe-4093-855a-e5c4f9b7cb87.jpg)

6. Although this solution works with SourceName=Microsoft Windows security auditing., still there are some events containing Japanese strings. It is not a issue if nobody is using those event types.

![solution.png](/.attachments/solution-5917c8a3-e480-4b6d-bad7-99855021ac7b.png)

**Additional SourceNames**

![sourcename.jpg](/.attachments/sourcename-c025e6c8-2653-42c3-a326-86cc8377c885.jpg)

**Solution 2**

1. Change the System Locale of the Windows OS. Windows "Welcome screen" becomes English, but users can use Japanese UI once they have login to the system.

![solution2.png.jpg](/.attachments/solution2.png-94be1a5f-fa4d-4248-913e-3a77e0833879.jpg)

Download instructions--> [200914_Winevent_Update.pdf](/.attachments/200914_Winevent_Update-ed7a37a9-d397-4cbc-b667-6407f3fe0e21.pdf)
