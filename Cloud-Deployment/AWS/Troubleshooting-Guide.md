# **Splunk Add-On for AWS**

The details below provide an overview of the how to troubleshoot a common Splunk Add-On for AWS issue.

![image.png](/.attachments/image-6a6574ab-f225-430f-b459-4237721a0c08.png)

# **Redlock SQS Poller Add-On**

The details below provide an overview of the how to troubleshoot a common Redlock SQS Poller Add-On issue.

![image.png](/.attachments/image-b191a88a-6843-4e2c-809f-b318e2b77856.png)

# **Additional Solution**

If the solutions in the previous slides do not work, another issue might be that the Splunk Access Key for the service account has been rotated and this change has not been replicated on the Heavy Forwarder.

![image.png](/.attachments/image-401e16e3-db1f-458d-80ea-799a8ca508c9.png)

# **Additional Solution (cont’d)**

If the solutions in the previous slides do not work, another issue might be that the Splunk Access Key for the service account has been rotated and this change has not been replicated on the Heavy Forwarder.

![image.png](/.attachments/image-f90d10cc-17c2-4f11-b1c9-d8056cad7624.png)

# **Additional Solution (cont’d)**

If the solutions in the previous slides do not work, another issue might be that the Splunk Access Key for the service account has been rotated and this change has not been replicated on the Heavy Forwarder.

![image.png](/.attachments/image-51de9749-8901-41e8-9344-66d4ee0127f2.png)

Troubleshooting Logs

Another way of troubleshooting issues is to look at the logs and see what errors may be showing up in /opt/splunk/var/log/splunk/splunkd.log 

![image.png](/.attachments/image-abf936c9-045d-4c56-b67f-ffa95a4ec8d5.png)

# **DCS AWS Access**

![image.png](/.attachments/image-5a44a76b-10a1-495c-831d-28b496f3c78d.png)

# **Appendix:**

General issues related with cloud:
- Service Now ticket: [DCS - Cloud Environment Request - Global Technology Services Self-Service](https://deloitteglobal.service-now.com/sp?id=sc_cat_item&sys_id=b56a03c9dbd9ffcccb86d18c689619bc)
- Deloitte Cloud Services Operations <dcsoperations@deloitte.com>
- Deloitte Cloud Services Networking <dcsnetworking@deloitte.com>

<TABLE  border=0  cellpadding=0  cellspacing=0  width=1320 style="border-collapse:
 collapse;width:660pt">
 <COL  width=343 style="width:172pt"/>
 <COL  width=276 style="width:138pt"/>
 <COL  width=701 style="width:350pt"/>
 <TR style="height:22.38pt">
  <TD  height=45  class=oa1  width=343 style="height:22.38pt;width:172pt">
  <P style="margin-top:0pt;margin-bottom:0pt;margin-left:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white;font-weight:bold">Document Name</SPAN></P>
  </TD>
  <TD  class=oa1  width=276 style="width:138pt">
  <P style="margin-top:0pt;margin-bottom:0pt;margin-left:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white;font-weight:bold">Document Type</SPAN></P>
  </TD>
  <TD  class=oa1  width=701 style="width:350pt">
  <P style="margin-top:0pt;margin-bottom:0pt;margin-left:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white;font-weight:bold">Description</SPAN></P>
  </TD>
 </TR>
 <TR style="height:87.1pt">
  <TD  height=174  class=oa2  width=343 style="height:87.1pt;width:172pt">
  <P style="margin-top:0pt;margin-bottom:0pt;margin-left:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white"><A 
  href="https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/Shared%20Documents/20-Design%20Splunk%20Environment/Splunk%20Data%20Flow%20Options%20-%20Global.pptx?Web=1">Splunk
  Data Flow Options - Global</A></SPAN></P>
  </TD>
  <TD  class=oa2  width=276 style="width:138pt">
  <P style="margin-top:0pt;margin-bottom:0pt;margin-left:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Data Flow Diagram,</SPAN></P>
  <P style="margin-top:0pt;margin-bottom:0pt;margin-left:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Service Accounts</SPAN></P>
  </TD>
  <TD  class=oa2  width=701 style="width:350pt">
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Heavy Forwarder Mapping (Slides 3):
  List each Splunk Heavy Forwarder and the corresponding Splunk App installed
  on it for ingesting AWS logs and Redlock alerts.</SPAN></P>
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"></P>
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Splunk Data Flow (Slide 12): Illustrate
  the data flow of AWS logs and Redlock alerts to Global Splunk.</SPAN></P>
  </TD>
 </TR>
 <TR style="height:49.94pt">
  <TD  height=100  class=oa3  width=343 style="height:49.94pt;width:172pt">
  <P style="margin-top:0pt;margin-bottom:0pt;margin-left:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white"><A 
  href="https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/Shared%20Documents/40-Device%20feed%20integration/AWS%20Add-On%20for%20Splunk%20Feed%20Integration%20Plan.docx?Web=1">Splunk
  Add-on for AWS - Splunk Feed Integration Plan</A></SPAN></P>
  </TD>
  <TD  class=oa3  width=276 style="width:138pt">
  <P style="margin-top:0pt;margin-bottom:0pt;margin-left:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Feed Integration Plan</SPAN></P>
  </TD>
  <TD  class=oa3  width=701 style="width:350pt">
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Outline how to deploy and configure the
  Splunk Add-On for AWS as part of the data onboarding process.</SPAN></P>
  </TD>
 </TR>
 <TR style="height:53.42pt">
  <TD  height=107  class=oa3  width=343 style="height:53.42pt;width:172pt">
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white"><A 
  href="https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/Shared%20Documents/40-Device%20feed%20integration/Redlock%20SQS%20Poller%20Add-on%20for%20Splunk.docx?Web=1">Redlock
  SQS Poller Add-on - Splunk Feed Integration Plan</A></SPAN></P>
  </TD>
  <TD  class=oa3  width=276 style="width:138pt">
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Feed Integration Plan</SPAN></P>
  </TD>
  <TD  class=oa3  width=701 style="width:350pt">
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Outline how to deploy and configure the
  Redlock SQS Poller Add-On as part of the data onboarding process.</SPAN></P>
  </TD>
 </TR>
 <TR style="height:49.03pt">
  <TD  height=98  class=oa3  width=343 style="height:49.03pt;width:172pt">
  <P style="margin-top:0pt;margin-bottom:0pt;margin-left:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white"><A 
  href="https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/Shared%20Documents/30-Build%20Splunk%20Environment/Splunk%20Ports%20Assigned.xlsx?Web=1">Splunk
  Ports Assigned</A></SPAN></P>
  </TD>
  <TD  class=oa3  width=276 style="width:138pt">
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Ports Assigned</SPAN></P>
  </TD>
  <TD  class=oa3  width=701 style="width:350pt">
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Provides the port numbers and protocols
  used to ingest various AWS logs and Redlock alerts source data.</SPAN></P>
  </TD>
 </TR>
 <TR style="height:49.03pt">
  <TD  height=98  class=oa3  width=343 style="height:49.03pt;width:172pt">
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white"><A 
  href="https://americas.internal.deloitteonline.com/sites/ctoteams/EnterpriseOperations/PlatformDelivery/splunk/Shared%20Documents/Data%20Maturity%20Tracker.xlsx?Web=1">Data
  Maturity Tracker</A></SPAN></P>
  </TD>
  <TD  class=oa3  width=276 style="width:138pt">
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Data Maturity Tracker</SPAN></P>
  </TD>
  <TD  class=oa3  width=701 style="width:350pt">
  <P style="line-height:normal;margin-top:0pt;margin-bottom:
  0pt;margin-left:0in;margin-right:0in;text-indent:0in;text-align:left"><SPAN style="font-size:10.0pt;font-family:Verdana;color:white">Tracks the CIM validation status and
  lists each Splunk index and sourcetype related to AWS.</SPAN></P>
  </TD>
 </TR>

</TABLE>