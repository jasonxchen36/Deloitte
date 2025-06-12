      
Once the data flows into Splunk, we need to add value to the data so that alerts and contents can run on the ingested data to identify potential malicious attacks or alert proactively on bad threat attackers. Hence we normalize the ingested data as per the custom Splunk data model which has been created to meet Deloitte’s Cyber needs. There are set of mandatory fields which are security relevant, and we extract the fields using various normalization techniques. There is a set of steps we follow as a part of Data Normalization:

**Step 13** **–** Determine the data model per data source.
- Normalize the fields under mapped data model. Refer the [Required Fields documentation](https://dev.azure.com/GlobalSOC/Splunk/_wiki/wikis/Splunk.wiki/258/Data-Models) for CIM compliance.

**Step 14 –** Review “**CIM Normalization**” **Phase 2** tab from the data quality dashboard.

**Step 15** **–** For cases where the Data Quality is not 100 percent due to known reasons, send a note to the concerned team/BISO/MF along with the explanations on why it can’t be achieved shared by Vendor/application team for their awareness. The awareness email needs to show the content which is affected by such missing fields.
o   The BISO/Member Firm awareness email sample template is attached [here](https://amedeloitte.sharepoint.com/:u:/r/sites/CyberDefenseEngineering/Shared%20Documents/Data%20Management/Splunk%20Onboarding%20Document/Onboarding%20guide%20documents/RE%20Approval%20needed%20%20Missing%20Field%20and%20Unknown%20Values%20for%20DERA%20Application%20Data%20Sources.msg?csf=1&web=1&e=seYsaC).

**Step 16 –**
- **InfraSec Data Sources**: Create a **CIM validation WI** and assign to Content team by filling this template (as the data quality is not up and running for InfraSec logs yet) [https://dev.azure.com/GlobalSOC/Splunk/_workitems/edit/180859](https://dev.azure.com/GlobalSOC/Splunk/_workitems/edit/180859)
                                                **OR**                                          
- **AppSec Data Sources**: Create a CIM validation WI and the engineer assigns this WI to himself/herself who is working on the data onboarding effort as for AppSec data sources Data Quality Dashboard will be leveraged to validate CIM validation checks.

**Step 17 –**
- **InfraSec Data Sources:** In case there is any feedback from Content team would incorporate the feedback and sent it back to Content team for closure and sign off - **OR** -
- **AppSec Data Sources:** If there are no CIM validation issues the engineer closes the CIM validation WI in his/her name after attaching a snapshot of the data quality dashboard depicting everything looks good. In exceptional cases where the CIM is not met the engineer attaches the awareness email sent to vendor/BISO/MF/stakeholder mentioning why certain fields are missing or the data quality dashboard is not complaint and then close the WI.

To know more about the CIM normalization, please visit: [CIM Normalization](https://amedeloitte.sharepoint.com/:w:/r/sites/CyberDefenseEngineering/Shared%20Documents/Data%20Management/Splunk%20Onboarding%20Document/Onboarding%20guide%20documents/Data%20Onboarding%20Methodologies/Phase%202/Phase2-Data%20Normalization%20proceess.docx?d=w1e8c04f7d389463db7c964d7482c5914&csf=1&web=1&e=bOC8t8)