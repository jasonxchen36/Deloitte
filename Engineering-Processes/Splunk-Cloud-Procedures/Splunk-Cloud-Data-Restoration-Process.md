This process is designed for Splunk Cloud Data Restoration. Dynamic Data Active Archive moves data from your Splunk Index to a Splunk-maintained archive, and subsequently back from the Splunk-maintained archive to the Splunk Index in a secure and tamper-resistant manner.

**We have a  43 TB (APAC) and 70 TB (EMEA) limit for restoration at any given time which is 10% of our Dynamic Data Active Searchable (DDAS). Therefore please make sure we are within this limit for all the restorations we initiate._** **_Splunk recommends to stay less than 25TB per restore for better performance._**

**Steps to submit a Splunk Cloud Data Restore Request:**
1. If requestor has access to DevOps site, submit a "Splunk Cloud Data Restore" Work Item and populate details of request.
2. If requestor does not have access to DevOps site, Stakeholder sends an email to DT - Cyber Defense Engineering - Architecture <dt-cyberdefenseengineering-architecture@deloitte.com>, with the email subject "Splunk Cloud Data Restore Request" and the following details:
- Purpose of request (e.g., audit, investigation, etc.) 
- Index name
- Timeframe of requested data (maximum of 365 days)
This information should be created in a "Splunk Cloud Data Restore" Work Item manually by the Architecture team.
3. Architecture Lead reviews request, gathers volume (GB/TB) estimate, and works with leadership to approve or deny based on details provided. 
4. If approved, Architecture Lead assigns to Engineer who creates Splunk Cloud Data Restore Work Item with details provided and takes below steps to restore data. 

**Steps to restore archived data to Splunk Cloud Platform:**

1. In Splunk Cloud, go to **Settings** > **Indexes**.
2. For the index where you want to restore data, click **Restore**. The menu displays the restore history for the specified index. You can see the history of data restoration and file size for the data restored.
3. Use the date picker to select a time range to retrieve.
4. Click **Check size**. Splunk Cloud Platform checks to see if the size of the file might impact performance. If the file size is too large, Splunk Cloud Platform blocks you from restoring data. If there is a potential performance impact, Splunk Cloud Platform displays a warning. Splunk Cloud Platform also prevents you from restoring data that overlaps with existing restored data.
5. Enter an **email** **address** to send job status notifications. Splunk Cloud Platform will notify you when the restoration is complete.
6. (Optional) If your time range includes data archived within the last 48 hours, toggle the **Recently Archived Data** switch to disable the default **Exclude** mode. When set to "Exclude" mode, DDAA skips restoration of data archived within the last 48 hours. Note that attempting to restore data that is not fully archived can cause data restoration to fail. 
7. Click **Restore** when you have refined the file size or date range to acceptable limits.
8. To check the status of your data restoration, click **Splunk Archive** in the **Storage Type** field to open the Archive page. To view the restore status, click the **Restore** tab. In the **JobStatus** field, you can see the status of your job:
**Pending**: The job has been submitted, but has not begun processing.
**In** **progress**: The job has been started, and is progressing.
Success
**Cleared**: You've successfully deleted the temporary archive from your index.
**Expired**: The restored data has passed the 30 day retention period and has been deleted from the index.
**Failed**: If you receive a Failed status, click the > button for the archive to display more details about why the restoration failed.

**Note**:   After you initiate data restoration, it can take up to **24- 48 hours** before data is restored. If it takes longer , contact **Splunk Technical Support**. 



**Steps to remove restored data from Splunk Cloud Platform:** 

1. In Splunk Cloud, go to **Settings** > **Indexes**.
2. Select the index with data you want to remove and click **Restore** to open the Restore Archive page.
3. For the range of data you want to remove, select **Clear** in the Actions column.
When the data is successfully removed, the **Jobstatus** column displays a Cleared status.

**Note:** You can manually clear restored data or let it auto-expire from searchable storage after 30 days.

Splunk docs link : https://docs.splunk.com/Documentation/SplunkCloud/9.2.2403/Admin/DataArchiver#Monitor_logs_during_archiving