# Git For Windows Installation
(If you're on Linux or MacOS, git may already be installed, or can be installed using your OS's package manager) 
## 1 Download git for windows from https://gitforwindows.org/
### 1.1 Run the installer
1.	Right-click on the installer file and choose "run as administrator
2.	Select "software install" as your reason for admin access. Note that your git version may be different than those shown in the screenshots. 
 ![image.png](/.attachments/image-f2465155-02c3-4500-b8a0-bd65d3599dc5.png)
3.	Accept the license agreement and install location by clicking "next"
 ![image.png](/.attachments/image-8c4072a6-b6b8-4dda-96ef-79e500adaee6.png)
4.	Leave the default components on the Select Components screen, and leave the start menu folder as the default.
 ![image.png](/.attachments/image-498a2c19-fabc-4435-a268-4a77775d6a9c.png)
5. On the "choose the default editor" screen, pick your editor of choice.
 ![image.png](/.attachments/image-a26fd075-b955-4fdb-8a0d-f34c991ebf3a.png)
*Note: The default option (vim) is notoriously difficult for new users. Unless you are already familiar with its usage, you may want to pick a different editor
**Note: With the exception of nano and vim, the text editor you choose in this dropdown must be pre-installed before installing git. If you choice is not available, the installer will prevent you from continuing
6.	On the "adjusting your PATH environment", leave the default selected (Use Git from the Windows Command Prompt). **Do not select the option to use optional Unix tools from the Windows Command Prompt**
 ![image.png](/.attachments/image-d8397781-f412-4f82-a5a3-4a7466ff226f.png)
7.	On the "Choosing HTTPS transport Backend", choose "Use the native Windows Secure Channel Library". Choosing another option may require adjustments to other part of the git configuration process.  
![image.png](/.attachments/image-4ba2cea9-84eb-4f35-98db-c50772452267.png)
8.	On "Configuring the line ending conversions, make sure "Checkout Windows-style, commit Unix-style line endings" is selected. Any other option will lead to possible difficulties.*
 ![image.png](/.attachments/image-5cb1c09c-7350-4d80-87bc-076e6bb84d55.png)
*Windows and linux use a different line-ending convention (Windows has two nonprinting characters at the end of the line, whereas Linux only has one), and this difference can cause issues. On Windows, files with the Linux format can all appear to be on one line, while on Linux, the ends of lines appear to have an "extra" garbage character, which Splunk may misinterpret.
9.	On "configuring the terminal emulator", Make sure to select MinTTY.
 ![image.png](/.attachments/image-29459b86-7bdb-4f0a-9a0c-48b7412bd0f1.png)
10.	On the "Configuring extra options" page, make sure "Enable Git Credential Manager" is checked - this needs to be installed to authenticate your computer when retrieving or pushing items to our source control system. Please leave the other items on this screen as the default.
 ![image.png](/.attachments/image-0ba06a7c-6a18-44ab-acce-15ea0251a6a4.png)
11.	Leave any experimental options disabled
 ![image.png](/.attachments/image-7f4622da-9e23-4097-83c9-9b123ca1942d.png)
12.	Click Install
13.	Once the installation has completed, clear the "Launch Git Bash" box and click Finish
14.	Refer to the [Configuration Changes](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki?pagePath=%2FGIT%20%26%20DevOps%20Processes%2FConfiguration%20Changes%20to%20AMER%20Repository%20Using%20GIT&pageId=18&wikiVersion=GBwikiMaster) and [Git Command Cheat Sheet](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki?pagePath=%2FGit%20Documentation%2FGit%20Command%20Cheat%20Sheet&pageId=15&wikiVersion=GBwikiMaster) guides for how to use your newly installed tools.