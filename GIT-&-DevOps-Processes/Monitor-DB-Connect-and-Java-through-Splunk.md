Once DB Connect and Java are installed/updated, we can monitor their version through Splunk. For that, we must add three new stanzas in a file inside the DB Connect app. Despite having two different Operative Systems, the process is very similar. The only things that changes are the route and the way of restarting Splunk.

The first step is to log into the server. In case you are in Linux, you must do it with the _dtt_sc_splunk_prd_ account using the command **sudo su dtt_sc_splunk_prd**. For Windows, you can modify these files with your a- account. 

Once we are logged in, we must create a new file in the bin DB Connect directory called “del_update.sh”. In Linux you can go to that directory with the command **cd /opt/splunk/etc/apps/splunk_app_db_connect/bin** and creating a new file with **vi del_update.sh**. (In Windows you can do it just with the Notepad app) Once you are in the empty file, you must add the following lines:

**touch $SPLUNK_HOME/etc/apps/splunk_app_db_connect/local/dbx_settings.conf
touch $SPLUNK_HOME/etc/apps/splunk_app_db_connect/default/app.conf**

When the lines are written, press **ESC + :wq** to save the new changes. Make sure that the new script has execute permissions. Executing the command **chmod +x del_update.sh** the script should have the permission mentioned before. (**You must be in the bin directory! If not, you must use absolute routes.**)

![Picture1.png](/.attachments/Picture1-52638ea4-4418-4ef0-8dd4-51cc44014aef.png)

![Picture2.png](/.attachments/Picture2-90a21930-5823-4345-b82e-adb2d8cbd491.png)

This script modifies the file’s date you mention in it to the actual time. This is necessary so there can be events in the index. After creating the script, go to the local DB Connect directory using the following command: cd /opt/splunk/etc/apps/splunk_app_db_connect/local

![Picture3.png](/.attachments/Picture3-51b85002-451c-4d7f-a113-953b402916f3.png)

The next step is to edit the file shown in the previous picture adding the following configuration: (In Windows you can do it just with the Notepad app)

![Picture4.png](/.attachments/Picture4-2cedd9ea-ff64-4503-b968-5e7661d00120.png)

**The index must change depending on the environment you are working on. If you are working on APAC, it should be _dttl_internal_apac_; or if you are working on EMEA, it should be _dttl_internal_emea_.**

What these stanzas makes is report a new event in the index shown every time those files are modified. As these files have the current versions of DB Connect and Java respectively, we will be able to see all versions with just one Splunk query. To make it work, we must edit those files mentioned in the _inputs.conf_. It works just adding some “#” in the file (be careful and do not comment anything).

Once we have added the stanzas to the _inputs.conf_ file and edit the _app.conf_ and _dbx_settings.conf_ files, we must restart Splunk.

To check if we have new events, write in the correspondent Search Head the following query: **index=internal_splunk_prod_[region] host=[host] source=/opt/splunk/etc/apps/splunk_app_db_connect***
