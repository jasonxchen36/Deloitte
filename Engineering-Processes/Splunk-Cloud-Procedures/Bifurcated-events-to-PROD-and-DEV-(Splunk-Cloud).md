#####################################################################################################################
**Before ingest events in production, please be sure the format, timestamp... is good and are compliance for ingestion**
#####################################################################################################################


In some cases is necessary to ingest events in production and development at same time. For this purpose we develop an App (del_apac|emema_bifurcated) inside ServerClass (del_apac|emea_azure_cloud_bifurcated) in DS az1436l021 (APAC), az1436l013 (EMEA). When we need to bifurcated events, we need to add the HF to it.

Before start the process, create WI with the request

![image.png](/.attachments/image-99f3bd11-5de2-48f2-8d1f-ab2f68b91535.png)

We need to be sure the index was created in both environments.
After that, we need go to **/opt/splunk/etc/deployment-apps/del_<REGION>_bifurcated/local/transforms.conf** and edit the REGEX, in case there are more than one index, split by "|", with the index name that we want to bifurcated

![image.png](/.attachments/image-f536f5b4-3f68-44e7-9ef2-94f3e807166b.png)

when the index is update, reload the serverclass

**/opt/splunk/bin/splunk  reload deploy-server -class del_apac_azure_cloud_bifurcated**

Overview
- Create WI using the template, "Splunk Cloud: Send data from PROD to DEV environment"
- Check if the index was created, in case does not exist, follow the steps to created index
- Add the index in the REGEX, in case there are more than one index, split by "|", in the /opt/splunk/etc/deployment-apps/del_<apac>_bifurcated/local/transforms.conf
- Reload the serverclass in DS, /opt/splunk/bin/splunk  reload deploy-server -class del_<apac_azure>_cloud_bifurcated
- Check events.

You can use this [link](https://docs.splunk.com/Documentation/Splunk/8.2.2/Forwarding/Routeandfilterdatad#Replicate_a_subset_of_data_to_a_third-party_system) as reference