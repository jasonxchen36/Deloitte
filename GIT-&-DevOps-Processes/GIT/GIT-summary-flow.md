# **Deployment flow**

![image.png](/.attachments/image-11607d96-b51e-45a0-8d1b-fb786235211a.png)

**Standalone**
- Copy the modified files in stand alone and create/update in staging brach
- Validated with the App owner o requester


**Staging**
- Without GIT, directly from back end (cli or .conf file) or front end (GUI)
- Pull request
- Wait for script runing
- Validated with the App owner o requester


**Production**
- Copy the modified files in staging and create/update in prod brach
- Pull request
- Wait for script runing
- Validated with the App owner o requester


**Keep in mind**
- Default.meta https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/28/Known-default.meta-Files
- GIT Install (Windows) https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/14/Installing-Git-(for-Windows)
- Quik guide https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/18/Configuration-Changes-to-AMER-Repository-Using-GIT
- Git commands https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/15/Git-Command-Cheat-Sheet


