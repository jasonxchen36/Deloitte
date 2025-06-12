A. **False Positive Filtering by GEMS**
1. Analyst finds field value they would like to filter out of alert (e.g., host or username)
1. Tier 1 and Tier 2 analysts report the value to Tier 3 analyst to confirm that value should be filtered out due to false positive
1. Tier 3 analyst reaches out to stakeholder and determines if behavior identified in alert is expected behavior
   - If expected behavior, Tier 3 analyst creates Devops “Content Feedback” work item and links to production content work item (“Related Work” section click “Add Link”, “Existing Item”, Link Type as “Parent”, and search for content item in the search box)
   - Content Feedback expected field population
     - Title – Filter Request for [Content Name]
     - Assigned to “Global FC Analysts”
     - Description – what is needed to be filtered out and why, stakeholder that approval was received from
     - Attachment – email (or other attachment) approval from stakeholder signifying that value can be filtered

1. Tier 3 Analyst will make Monitoring lead and GEMS owner aware of the filter and will add value to filter/lookup via the web gui
1. Analysts will confirm that the value has been filtered out properly and respond to the “Discussion” section of Content Feedback work item
1. If value has been filtered out properly and verified, Content Feedback item will be closed out by Tier 3 analyst

B. **False Positive Filtering based on Request (RITM)**
When MF observes any false positives, they raise an RITM/SIR in snow and content team will take care of that and add the requested values in allow list which will not generate further false positives for that specific value. 

[RITM1893420 | Requested Item | ServiceNow](https://deloitteglobal.service-now.com/now/nav/ui/classic/params/target/sc_req_item.do%3Fsys_id%3D6ddd4adb973012581ea0ba67f053af8c%26sysparm_stack%3Dsc_req_item_list.do%3Fsysparm_query%3Dactive%3Dtrue) for reference.

