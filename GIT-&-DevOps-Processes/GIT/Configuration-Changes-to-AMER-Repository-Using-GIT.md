##Connecting to the SHC_AMER Branch
1. Connect through GIT into the Splunk master branch (live version of code)
2. **git checkout SHC_AMER** <- checks out the "SHC_AMER" branch, which is where all our standard code for the Americas is stored after review. Make sure you are in the path of the repo you will need to be in. 
![image.png](/.attachments/image-3e501f27-5902-4230-af01-3b71b20f5101.png)
3. **Launch git pull** <- grabs all the changes made since last time we connected to the Deloitte repository. This ensures you will be working with the latest version of code.
![image.png](/.attachments/image-ffe452f3-b689-412f-852b-e19fc7690f2e.png)

##Checking out of the Splunk Master Branch
Because of the repository structure, you are unable to make changes to the files when they are within the master branch. **git checkout -b <your branch name\>** <- creates a new branch with the specified name (based on your current branch). If you're adding a new search, you could call it something related to the use case or content that is being added.
![image.png](/.attachments/image-f0a986ab-d5e5-48b3-86c0-c291852dede8.png)
Once you checkout the code from the master branch to a new branch it will indicate that you have switched branches and now you are able to make changes to the file.

##Making changes to  the source code files

Edit your files (in the git repository) using your normal process. Once the changes have been made, run the command **git status** <- shows what files you've changed that haven't been "staged" (added to the list of files that will be saved to the repository when you commit). 
![image.png](/.attachments/image-8b723617-6c00-4921-960d-9acf14ce3cd7.png)
In order for the files to be added you must use the command **git add <name of file to add\>** <- adds files to the list of files to stage. You can add more than one file by adding whole folders, or putting multiple filenames after the add command. An error message will show up only if the command didn’t work correctly. 

After adding files, use the command **git status** to make sure that your changed files were added. As you can see the file name changes from red to green validating the change.
![image.png](/.attachments/image-c3a23f00-a7d5-4586-ba0e-cc4f77b0965b.png)
**git commit** <- "commits" your changes. Your editor will pop up so you can enter a commit message, which is a few lines that explain what your changes do. Write your changes, and save the commit message to commit your changes. 
![image.png](/.attachments/image-a5a55972-f5ae-4207-b67f-f37e8e4f5cdb.png)
![image.png](/.attachments/image-916f05f6-e104-4bd1-ba18-1f04852de6a3.png) 
![image.png](/.attachments/image-3fd29620-a600-4c2a-a299-baae9d40a402.png)

##Checking in to the source code repository
At this point, your changes have been saved, but are only on your local machine. We need to "push" your changes up to the server so they can be merged into the "SHC_AMER" branch, which everyone works off of. Use the following command **git push origin <your branch name\>** <- takes your local branch and uploads it to the server. At this point, you change is on the remote server, but not yet in the "SHC_AMER" branch, which we use to store our live configurations. we have to submit a "pull request" to get our changes approved an added to the main branch.
![image.png](/.attachments/image-83d2041e-30d3-484e-a48e-63359f626c5b.png)
This indicates that the files have been successfully added from the local branch to the remote branch. 
![image.png](/.attachments/image-ae525db7-fe69-4f34-9927-259cb705acc4.png)

##Merging your changes into the SHC_AMER branch
To merge your newly saved changes changes, you have to create a "pull request" to get your changes approved and accepted. On [Azure DevOps](https://dev.azure.com/GlobalSOC/Splunk), navigate to **Repos->Pull Requests**:
![image.png](/.attachments/image-207d32b7-a324-423d-a0ae-2d0ac8101e22.png)
At the top right of the screen, click **New Pull Request**:
![image.png](/.attachments/image-0c6c1dd4-5f02-46a1-8e9a-3e9fc9a50139.png)
On the New Pull Request screen, select the branch you created as the source branch, and SHC_AMER as the destination branch. The message field may fill in automatically, if not, enter a description of the changes you have made:
![image.png](/.attachments/image-017b2dc7-4203-4e25-a38c-9ca54b09cc32.png)
You can leave the reviewer field empty, but add any work items associated with your request. Also confirm that only the changes you made show up in the "files" section at the bottom of the page, then click "Create."
![image.png](/.attachments/image-dc303ca6-7354-4840-951c-7d71d22039c8.png)
Once the Pull Request has been created, you should see a screen similar to the below screenshot. 
![image.png](/.attachments/image-ead6b684-2113-4569-b304-62a641725f8e.png)
The required approvers are noted at the bottom-right, along with work items. At this point, the pull request is ready for review, and can be merged when the review requirements have been met. 

To have your changes integrated into the SHC_AMER branch automatically when merge requirements are met, rather than having to manually complete the process, you can set auto-complete. To do this, click Set Autocomplete at the top right, confirm "Delete <BranchName\> after merging" is checked, and then click "Set Autocomplete". When your pull request receives all mandatory approvals, it will be automatically merged. 
![image.png](/.attachments/image-c687a423-97f8-46b7-aa08-66157e47d421.png)