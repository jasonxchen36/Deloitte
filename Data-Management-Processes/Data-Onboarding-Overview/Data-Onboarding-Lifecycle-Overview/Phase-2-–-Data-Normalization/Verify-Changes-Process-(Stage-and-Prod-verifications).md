#Verifying CIM normalization changes with the Global FC Engineering Content team during the Stage Test and Ready for Prod Verification states. 
 
- Within each CIM Validation Request Work Item (CVRWI) there is a field called "Test Search String" (populated by Global FC Engineering Content team), an example is shown below

![image.png](/.attachments/image-9e14ba8d-068f-4462-9471-f6478f30a5b1.png)

- Once the CVRWI enters the Stage Test state, Engineer will run the Test Search String and verify that the output is accurate/expected by running the search in Splunk
- If output is accurate/expected, Engineer will take a screenshot and upload to the attachments section of the CVRWI
- Engineer contacts (ping, email, Devops call-out) Global FC Engineering Content Engineer and asks them to review the screenshot
- If Global FC Engineering Content Engineer confirms output is accurate/expected, move on to Ready for Production state and repeat this process once PR for Production ES SHC is approved and pushed

##Other verification options
- If the process above fails for any reason, please contact Global FC Engineering Content team via phone, email, ping, or Azure Devops call-out to verify changes that are made