# **Creating indexes**
- [ ] **Note that all the changes have to be made on the SHC branch since the ICM branch is no longer available.**

Since we are not using the ICM branch anymore, the new indexes must be added in the indexes.conf file on the "**del_<region>_dev_all_indexes** or  **del_<region>_prod_all_indexes**"
This is the same process as before, the only thing that has changed is the location of the app.
It has been moved from ICM to SHC.


# **Installing, removing or updating Splunk Base apps on Splunk Cloud environment**
Here are the steps to add or update an app to cloud environments:

Every time that you need to add or update an on cloud you need to make a request with
 [this work item template](https://dev.azure.com/GlobalSOC/Splunk/_workitems/create/Task?templateId=a57efbf6-e9fa-4a7b-8415-143bce383737&ownerId=a20838c2-f0b8-4772-97dd-840c8b62cdce): 

 ![image.png](/.attachments/image-39feb04b-462d-482a-bac9-2866a57ea6bd.png)

How to get the required information about the app for the WI:
1. **ID field**: We need to check the ID of the app and add it to the WI, this ID can be checked at the end of the URL on the app page (5948 on this example): ![image.png](/.attachments/image-86fbb239-62ca-46f3-8f53-4aea962b8fb5.png)

2. **Name and Version**: Next you need to check the name and version of the app, **it is very important to check that the app that we want to install is compatible with Splunk Cloud** (You can check if it is compatible with splunk cloud on the Version History tab)

![image.png](/.attachments/image-a88d154b-7608-4638-816e-a40c7d7dccc6.png)

3. **License**: You can get the license link for the app on the summary tab and then scrolling down until you see Licesing, then copy the license link into the WI.

![image.png](/.attachments/image-9588f97c-5c08-4679-80d7-becda18dd2ba.png)

4. **Request type**: Here you need to specify what is your request for , Installing, Updating or Removing the app.

5. **Environment**: Specify the environment.

6. **Justification**: Specify the reason.

**NOTE**: New Splunk Base app permissions are set as: 

`access = read : [ admin, sc_admin, cpblty_gems_es_user ], write : [ admin, sc_admin, cpblty_gems_admin ]`  
`export = system` 
`owner = nobody`

# **Customizing splunk base apps**

**Only if you need to customize** application default settings or **change the default permissions**, you need to add the app to the DevOps branch.

**Once the app is installed** in the environment if you need to make any changes on the app there are a few points to be aware of:

- All the changes have to be made into the **/local** folder, otherwise the changes **will not** be applied

- Your PR with the changes will **go through validation** , the validation proccess is explained [here](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/1120/How-to-review-Devops-pipeline-errors).

- Make sure that your changes are **deployed and tested in DEV** environment before sending PRs with the changes to PROD since the pipeline will check that the changes have already been tested in dev.
_(The process for sending data to dev for testing purposes is explained below on this page)_

![image.png](/.attachments/image-a091ff62-2a82-4baa-9172-2ed699dec413.png)
![image.png](/.attachments/image-805c3291-c144-4e97-a5e9-f9dc71c1ba47.png)

- When submitting the PR make sure to **check the pipeline log** to fix or bypass any errors.




# **Sending data to DEV**


Since we don't have any data on DEV , if you want to use DEV for testing you need to duplicate the PROD data into DEV environment, and here is the [WI template for it](https://dev.azure.com/GlobalSOC/Splunk/_workitems/create/Task?templateId=458d9b0e-5d59-4344-b265-28b995e59ecf&ownerId=a20838c2-f0b8-4772-97dd-840c8b62cdce): 

![image.png](/.attachments/image-e612fc1f-a694-4757-bc83-7e039b281f1c.png)

This is a simple process, you just need to insert two parameters on the request , the index(es) name , the time of bifurcation and the reason of the bifurcation.


*****This is not the final version of this procedure, this page will be updated if there are any changes in the future.***

