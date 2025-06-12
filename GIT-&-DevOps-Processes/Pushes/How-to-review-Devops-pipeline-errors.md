# What to check when validating PRs

This is a guide for the cloud validation process, the page contains the necessary steps to perform when validating PRs and checks after the push and a brief explanation of what is done on every step of the push , also here you'll find a list of bypassers depending of the issue that needs to be bypassed.


## What needs to be checked

When validating PRs you can see the log from the pipeline if you go here:![image.png](/.attachments/image-f1f9fda6-f63e-4d88-a93f-547e7d7c1083.png) _**(It is recommended to open the full log instead of just checking the errors that appear on the PR summary so you can see clearly where the errors are)**_

Once here there you'll see this screen: ![image.png](/.attachments/image-1e12d97d-90b2-41cb-b3b5-95503afa302e.png)
This is the pipeline log, here you can find a record of what is being done with every step detailed. 

There are two main parts in this pipeline regarding the errors, almost every error that appears before the _"Merge Changed Apps"_ step can be bypassed, for these errors you'll find a list of bypassers from different teams and depending on the error you'll need to contact a specific bypasser. 

The second part comes in the _"Merge Changed Apps"_ step. Here we can see a variety of errors and **these errors cannot be bypassed and must be fixed by the author**.

This is a sample of an error: ![image.png](/.attachments/image-830e07c7-dd08-4f81-9652-fe9b237a70a3.png)
The prompt will give you all the necessary information to fix the errors and get the app validated.

It will show you the folder or folders where the errors are located and also it will specify the file and the line inside the file that is causing the error, for example: 

![image.png](/.attachments/image-ea8114b1-81c9-49b1-89cd-490b0a9ef6b7.png)

When the errors are fixed you'll need to submit a new PR and go through validation process again.

## Pipeline explanation

Here is a brief explanation of each step of the validation:

![image.png](/.attachments/image-e38c9cd9-da4c-4bde-a1cb-37f3df26c675.png)

**Initialize job:** Here the pipeline does the necessary checks and tasks to start the job.
![image.png](/.attachments/image-5c303dc0-a447-438d-8a07-a921fbbb601f.png)

**Checkout SHC:** It makes a pull from the branch.
![image.png](/.attachments/image-5f81637c-f16c-430b-8aa1-5f72f95a52d8.png)


**Identify changes:** Looks for the modified apps.![image.png](/.attachments/image-19fe42e6-77f0-4e43-8439-f08ce1d7e61c.png)

**Validate JSONs:** Checks JSON files looking for errors.![image.png](/.attachments/image-b79311ef-89a7-4b28-bc9d-ddeede3109f9.png)

**Test in Dev:** Checks if the changes have been tested in DEV environment. ![image.png](/.attachments/image-72cbfbc5-1d17-43d7-ae2f-2da45f23310d.png)

**Find whitespaces:** Looks for whitespaces inside app files. ![image.png](/.attachments/image-c42eb2f3-5b8b-4502-b4cb-936a19e9d75e.png)

**Searches disabled:** Checks for errors in saved searches: ![image.png](/.attachments/image-24095cc4-888a-42f1-9169-2b6fe7f90e3b.png)

**Lookups uploading:** Here the pipeline uploads the necessary lookups.![image.png](/.attachments/image-9e90e4c5-7c2c-4f2e-b8dd-f7e662d2fe42.png)

**Closely push:** Checks if the PR is done the same day of the push.![image.png](/.attachments/image-dc8c1c20-e464-4064-99e5-927590738c88.png)

**Metadata compliance:** Checks the metadata compliance and looks for errors.![image.png](/.attachments/image-20c1f3d4-6b45-45d9-b2d0-961b7a63128e.png)

**Label size:** Checks that the names of the searches in the stanzas are not longer than 100 characters. ![image.png](/.attachments/image-4ab15fdc-4b28-472b-a941-f2c205192b93.png)

**Rename command:** Tests with the rename command.![image.png](/.attachments/image-0d08e6cf-be47-4370-9dc6-bef0aefeec56.png)

**Cron compliance:** Checks for the scheduled searches.![image.png](/.attachments/image-6d1673c8-4b6d-42a7-a522-d2e899b4e649.png)

**Protected apps:** Tests for protected apps. ![image.png](/.attachments/image-67eb01e3-02f9-47a4-8bed-8e562db46adb.png)

**DEV SNOW tickets:**  Checks if SNOW ticket creation is included in volume testing.![image.png](/.attachments/image-b6826b5e-c998-424d-9e57-b4597dbd49b7.png)

**Splunkbase encapsulation:** Removes some apps from validation![image.png](/.attachments/image-02bd1731-ca5f-4234-ac1f-36ddcc03ebb2.png)

**Dependencies:** Checks and installs all the dependencies.![image.png](/.attachments/image-b85ff43a-1f09-45e0-9937-f3c5ef46c99c.png)

**Merge local folder:** Merges local folder and checks for not bypassable errors ![image.png](/.attachments/image-5d470483-3ec5-4d26-8e3b-8c7abe69a7ea.png)

**Pack apps:** Packs the apps and prompts the apps list. ![image.png](/.attachments/image-833b34b3-50ab-4547-9bdd-52a6ec14f43d.png)

**Validate apps:** Runs the validation and shows the errors. ![image.png](/.attachments/image-b1d44955-8cd9-4d6b-8c74-fbe2f9ff7a4c.png)
