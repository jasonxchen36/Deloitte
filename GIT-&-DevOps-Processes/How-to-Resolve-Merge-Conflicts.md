Procedure: 
1. Make sure your SHC_AMER branch is up to date 
-      git checkout SHC_AMER
-      git pull on the SHC_AMER branch
2. Switch to the branch that has merge conflict 
-      git checkout <branch>
3. Merge SHC_AMER and <branch>
-      git merge SHC_AMER
4. Resolve the merge conflicts
-      Open the file which has merge conflicts and find the headers (<<<<<<<) and master (>>>>>>) and decide which commit you want to keep. 
-      This is the tricky part, get in contact with who made conflicting changes to decide which is supposed to remain in the file.
5. Commit the changes to the branch
-      git commit -m "describe your changes"
6. Push your changes
-      git push origin <branch>
