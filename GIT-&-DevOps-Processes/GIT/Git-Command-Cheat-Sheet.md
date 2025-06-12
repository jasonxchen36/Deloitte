[[_TOC_]]
##Fundamental Commands

###fixing windows line endings
`dos2unix <file_with_windows_line_endings>`

###clone a repository:
`git clone <url_you_copied_from_devops_without_modification>`

###change branch: 
`git checkout <branch_name>`
                
###create a new branch based on the current branch: 
`git checkout -b <new_branch_name>`
                
###Update your local copy of the repository:
`git pull`
                
###Add files to your current commit (snapshot):
`git add <file_or_folder_name>`

###Remove files from your current commit that you don't want saved:
`git reset <file_name>`
                
###Check what files have been added to your commit
`git status`

###Commit/Save your changes:
`git commit`
                
###Push your branch and changes to the remote repository:
`git push origin <your_branch_name>`

###Look at the git history of your current branch (a good place to get CommitIDs)
`git log`

###See differences between the last commit and your current version
`git diff`

##Basic git shortcuts
###Reference the latest commit on your current branch
`HEAD`
Example: 
`git reset --hard HEAD` 
Resets the current working directory back to the latest commit, wiping out any changes since then`

###Remove changes to untracked/uncommitted files:
`git clean -fdx`

##Advanced Git Commands

###See all commits from a given user in a specific range
`git log –all –after="MM/DD/YYYY XX:XX" –before="MM/DD/YYYY XX:XX" –author=<User Name>`

###Remove a commit that was made accidentally: 
`git revert <CommitID of the commit to revert>`

###Manually merge a branch into your current branch
`git merge <BranchToMerge>`

###Create a tag (not available to all users)
`git tag -a <TagName> <CommitId to tag>`

###Push a tag

`git push origin <TagName>`

###"Go back in time" to a specific commit
`git checkout <CommitID>`

###Pull a file from a different branch or commit ID into your current working branch
`git checkout <BranchName or CommitID> <Filename to Retrieve>`
