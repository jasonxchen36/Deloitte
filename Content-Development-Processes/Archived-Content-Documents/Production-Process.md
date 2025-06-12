Moving Content into Production.

Update your associated work items in DevOps by filling out every field on the work item according to the formatting guidelines below (format requirements only listed for fields with requirements) if you have not done before.
a. Description: content description / requirements
b. Security domain: one word string containing which security domain from Splunk ES the correlation search maps to
c. Cron Expression: Set by framework, but needs to align to be scheduled to be less frequent than search runtime. E.g. if search takes 5 minutes 30 seconds to run, the minimum interval that the search can be scheduled is every 6 minutes
d. Search time earliest: -<integer><quantifier> e.g. -24h = 24 hours
e. Search time latest: -<integer><quantifier> “now” is acceptable here. Same format as “Search time earliest” parameter
f. Throttle field: the variable name to throttle on. Must correspond to the last time the developer named the variable.
g. Throttle duration: same format as search time earliest / latest
h. Search Query logic: Every “|” character must be preceded by a newline except for the last line of logic
i. Search query logic must end in a “| fields” command and explicitly list the “_time” variable.
ii. “_time” variable cannot be renamed to anything else
i. If content is to be consumed by the Monitoring team
i. SecOps Node parameter: defined in mapping from FC use case in spreadsheet “Splunk – Snow SecOps Integration”
ii. SecOps Resource parameter: the variable name of the resource affected that the alert intends to monitor

Move work item to the “Ready for Production” board on Azure DevOps and add the tag "PROD" in the BCT WI.
<span style="color:red">**Confirm that none of the mandatory fields used by SNOW its presented in the Search Query Logic window in the BCT WI : description | node | destination | resource | severity | source | type**</span>

Run Azure_DevOps_API_Conf_Builder_Prod.py to generate the stanza for pushing the logic.

Perform git DevOps activities
a. Switch to our active production branch using git checkout “git checkout SHC_AMER”
b. Sync your repository with the server using “git pull”
c. Create a new branch to hold your content if it's not already a branch already opened for the next change window, for the pull request “git checkout -b <Content Updates SHC REGION DATE PUSH>”
d. Copy the part fo the savedsearches_prod.conf created above to the correct Splunk application FCxxxx. 
e. Make sure that any notables are tagged as prod
i. Open tags.conf in the local directory of the app of the content
ii. Paste the encoded text from tags_prod.conf output from the python script
iii. Ensure that “prod=enabled” 
f. Remove from DEV-Content floder the alert if was in VT before. 
g. Add the configuration to the list of changes to be committed using “git add <filename>” and confirm the changes you want have been added using “git status”
h. Commit your changes using “git commit” and provide a brief but clear description of the changes you made in the commit message
i. Push your newly created changes to the server with “git push origin <Content Updates SHC REGION DATE PUSH>”, where a_brief_but_informative_name is the branch name you created earlier.
j. Create a new pull request in DevOps based on the branch you just pushed
k. Make sure that if you set up Auto-Complete that you do not set the PR to automatically complete linked work items (as these items are still in testing)
After your pull request is approved and has been pushed out during a change window, go into the Splunk GUI and enable your content. Confirm that your content is scheduled to run at a specific time.
a. Make sure you check ES app and Saved Searches, Reports, and Alerts.
Moving Content from Volume Testing to Production.

After your pull request is approved and has been pushed out during a change window, go into the Splunk GUI and enable your content. Confirm that your content is scheduled to run at a specific time. Make sure you check ES app and Saved Searches, Reports, and Alerts.