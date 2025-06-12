Deloitte Cloud Services (DCS) provides a core set of platform capabilities, known as **Platform Guardrails or Layer 0**. These core capabilities enable Deloitte Cloud Services to manage cloud standards, policies, and guidelines and are automatically provided to all DCS users. **Platform Guardrails/Layer 0** ensures critical security measures are implemented at the platform layer and supports **PM40**, **ISO**, and **SOC2** requirements. Each capability is supported by world-class technologies and solutions enabling DCS to provide a secure, seamless, and scalable cloud environment.

Information within this wiki comes from the following url and was replicated in the instance the reference material is no longer available: https://resources.deloitte.com/sites/onetechnology/Documents_New/Business_of_IT/OneCloud/Tech-Platform-Guardrails.pdf

## Guardrail Capabilities
Below are the platform/layer 0 – guardrail technologies supporting each cloud service provider. Also, included are platform-custom roles.


|Capability|Description|
|--|--|
|Firm Network Connectivity|Provide intrusion detection/prevention services (IDS/IPS) using Deloitte connected VPCs to provide secure inbound and outbound access to the Deloitte network and public internet.|
|Resource-Specific Policies|Aligns infrastructure deployment to a common control framework.|
|Activity Logging|All account activity is logged, encrypted, and stored. Logs are ingested by Splunk and monitored by SOC.|
|Security Event Monitoring (SIEM)|SOC monitoring and detection of platform security events is based on log analysis for specific use cases (network & OS layers included).|
|Service Health Monitoring|Monitor for health status of all deployed cloud services on the vendor platform.|
|Password Policy IAM|Firm’s password policy enforced for all accounts.|
|Required Global Tags|Tags are used to assist with resource allocation for billing/reporting and configuration management/automation. Listed are the required tags, however optional tags are available.|
|Cost Management|Access to Cloudability which provides cost reporting, monitoring, and optimization capabilities.|
|Custom Roles|Custom cloud service provider roles are automatically implemented to accommodate platform support and appropriate user access.|
|Compliance Management|Enables preventative or corrective processes based on specific noncompliant events. Processes include missing tag enforcement, exposed security groups, unencrypted storage, etc.|
|Security Audit|Enables access to a tool that detects misconfigurations within AWS accounts from a list of industry, firm and project policies (ISO, HIPPA, CSA / CCM, NIST, SOC 2, etc.). SOC monitors alerts (est. Q1 FY20).|
|Enterprise Support|All accounts are enabled with enterprise support, which provides a concierge-like service. The focus is assisting project teams achieve their outcomes and find success in the cloud.|

## Platform Guardrail Information
Listed are the capabilities provided at the platform/layer 0 level. Also, provided are the technologies supporting each capability by cloud service provider.

<TABLE  class=MsoTableGrid  border=1  cellspacing=0  cellpadding=0 style="border-collapse:collapse;border:none">
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;background:#D9D9D9;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal><B><SPAN style="color:black">Capability
  </SPAN></B></P>
  </TD>
  <TD  width=192  valign=top style="width:2.0in;border:solid windowtext 1.0pt;border-left:none;background:#D9D9D9;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal><B><SPAN style="color:black">AWS</SPAN></B></P>
  </TD>
  <TD  width=201  colspan=2  valign=top style="width:150.65pt;border:solid windowtext 1.0pt;border-left:none;background:#D9D9D9;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal><B><SPAN style="color:black">Azure
  </SPAN></B></P>
  </TD>
  <TD  width=204  colspan=2  valign=top style="width:153.0pt;border:solid windowtext 1.0pt;border-left:none;background:#D9D9D9;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal><B><SPAN style="color:black">GCP </SPAN></B></P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Firm Network Connectivity</P>
  </TD>
  <TD  width=192  valign=top style="width:2.0in;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpFirst style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>MPLS (DirectConnect)</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>F5</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Palo Alto</P>
  <P  class=MsoNormal>&nbsp;</P>
  </TD>
  <TD  width=201  colspan=2  valign=top style="width:150.65pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpFirst style="margin-left:21.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>MPLS (ExpressRoute)</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:21.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>F5</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:21.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Palo Alto</P>
  </TD>
  <TD  width=204  colspan=2  valign=top style="width:153.0pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpLast style="margin-left:18.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Google Cloud VPN</P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Resource-Specific Policies</P>
  </TD>
  <TD  width=192  valign=top style="width:2.0in;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Automation-driven policies that protect and secure the
  platform environment.</P>
  </TD>
  <TD  width=201  colspan=2  valign=top style="width:150.65pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>There are several policies protecting and securing the platform
  environment which DCS is monitoring against, such as:</P>
  <P  class=MsoNormal>&nbsp;</P>
  <P  class=MsoListParagraphCxSpFirst style="margin-left:21.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Storage account encryption at rest/in transit.</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:21.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Restrict public IP usage.</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:21.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>SOC managed Splunk integration with Key Vault.</P>
  </TD>
  <TD  width=204  colspan=2  valign=top style="width:153.0pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>There are several policies protecting and securing the platform
  environment which DCS is monitoring against, such as:</P>
  <P  class=MsoNormal>&nbsp;</P>
  <P  class=MsoListParagraphCxSpFirst style="margin-left:18.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Storage account encryption at rest/in transit.</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:18.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Restrict Public IP usage.</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:18.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>SOC Management Splunk Integration.</P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Activity Logging</P>
  </TD>
  <TD  width=192  valign=top style="width:2.0in;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Cloudtrail</P>
  </TD>
  <TD  width=201  colspan=2  valign=top style="width:150.65pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Azure Activity Monitor</P>
  </TD>
  <TD  width=204  colspan=2  valign=top style="width:153.0pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpFirst style="margin-left:17.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Forseti Security</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Cloud Audit Logs</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:17.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Stackdriver Logging</P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Security Event Monitoring (SIEM)</P>
  </TD>
  <TD  width=192  valign=top style="width:2.0in;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpFirst style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>SOC Managed Splunk</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Argo (Elasticsearch)</P>
  </TD>
  <TD  width=201  colspan=2  valign=top style="width:150.65pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>SOC Managed Splunk</P>
  </TD>
  <TD  width=204  colspan=2  valign=top style="width:153.0pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>SOC Managed Splunk</P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Service Health Monitoring</P>
  </TD>
  <TD  width=192  valign=top style="width:2.0in;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpFirst style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>AWS Service Health</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Argo (Elasticsearch)</P>
  </TD>
  <TD  width=201  colspan=2  valign=top style="width:150.65pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Azure Service Health</P>
  </TD>
  <TD  width=204  colspan=2  valign=top style="width:153.0pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpFirst style="margin-left:17.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Google Cloud Status Dashboard</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:17.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Stackdriver Monitoring</P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Password Policy IAM</P>
  </TD>
  <TD  width=192  valign=top style="width:2.0in;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Firm’s password policy through IAM.</P>
  </TD>
  <TD  width=201  colspan=2  valign=top style="width:150.65pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Azure Active Directory (AD)</P>
  </TD>
  <TD  width=204  colspan=2  valign=top style="width:153.0pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Azure Active Directory/Azure AD Connect</P>
  <P  class=MsoNormal>&nbsp;</P>
  <P  class=MsoNormal>Active Directory integration with G Suite SaaS App:</P>
  <P  class=MsoListParagraphCxSpFirst style="margin-left:17.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>G Suite supports SP initiated SSO</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:17.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>G Suite supports automatic user provisioning </P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Required Global Tags</P>
  </TD>
  <TD  width=597  colspan=5  valign=top style="width:447.65pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>The following tags are required for each cloud provider.
  Reference <A 
  href="https://resources.deloitte.com/sites/onetechnology/Documents_New/Business_of_IT/OneCloud/Tech-Tagging.pdf">Public
  Cloud Provider Object Tagging</A> for more details. </P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Required Global Tags</P>
  </TD>
  <TD  width=199  colspan=2  valign=top style="width:149.2pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Tagging required at the account level:</P>
  <P  class=MsoListParagraphCxSpFirst style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Billing Code</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Member Firm</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Country Code</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Contacts:</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:37.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Group Contact</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:37.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Primary Contact</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:37.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Secondary Contact</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Client</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Country</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Function</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Project Name</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Classification</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Environment</P>
  </TD>
  <TD  width=199  colspan=2  valign=top style="width:149.2pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Tagging required at the resource level:</P>
  <P  class=MsoListParagraphCxSpFirst style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Billing Code</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Member Firm</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Country Code</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Function</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Contacts</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>CS</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Environment</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Application</P>
  <P  class=MsoNormal>&nbsp;</P>
  </TD>
  <TD  width=199  valign=top style="width:149.25pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Tagging required at the project level:</P>
  <P  class=MsoListParagraphCxSpFirst style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Billing Code</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Member Firm</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Country Code</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Function</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Contacts</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>CS</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Environment</P>
  <P  class=MsoNormal>&nbsp;</P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Cost Management</P>
  </TD>
  <TD  width=199  colspan=2  valign=top style="width:149.2pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Cloudability</P>
  </TD>
  <TD  width=199  colspan=2  valign=top style="width:149.2pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Cloudability</P>
  </TD>
  <TD  width=199  valign=top style="width:149.25pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpFirst style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Cloudability</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Cloudhealth</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Apptio</P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Compliance Enforcement</P>
  </TD>
  <TD  width=199  colspan=2  valign=top style="width:149.2pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>AWS Lambda</P>
  </TD>
  <TD  width=199  colspan=2  valign=top style="width:149.2pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpFirst style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Azure Policy</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Cloud Functions</P>
  </TD>
  <TD  width=199  valign=top style="width:149.25pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Cloud Functions</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Org Policies</P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Security Audit</P>
  </TD>
  <TD  width=199  colspan=2  valign=top style="width:149.2pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpFirst style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Security Hub</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Redlock</P>
  </TD>
  <TD  width=199  colspan=2  valign=top style="width:149.2pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Azure Security Center</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:19.0pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Redlock</P>
  </TD>
  <TD  width=199  valign=top style="width:149.25pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Security Command Center</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:17.5pt;text-indent:-.25in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>Redlock</P>
  </TD>
 </TR>
 <TR>
  <TD  width=188  valign=top style="width:141.35pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Enterprise Support </P>
  </TD>
  <TD  width=199  colspan=2  valign=top style="width:149.2pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>AWS Enterprise Support</P>
  </TD>
  <TD  width=199  colspan=2  valign=top style="width:149.2pt;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Microsoft Enterprise Support</P>
  </TD>
  <TD  width=199  valign=top style="width:149.25pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Google Cloud Enterprise Support</P>
  </TD>
 </TR>
</TABLE>

## Custom Roles 

Below are the custom roles Deloitte has created for AWS, Azure, and GCP. _Roles may change with product maturity._


<TABLE  class=MsoTableGrid  border=1  cellspacing=0  cellpadding=0 style="border-collapse:collapse;border:none">
 <TR>
  <TD  width=209  valign=top style="width:157.0pt;border:solid windowtext 1.0pt;background:#D9D9D9;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal><B><SPAN style="color:black">Cloud Vender</SPAN></B></P>
  </TD>
  <TD  width=576  valign=top style="width:6.0in;border:solid windowtext 1.0pt;border-left:none;background:#D9D9D9;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal><B><SPAN style="color:black">Custom
  Role</SPAN></B></P>
  </TD>
 </TR>
 <TR>
  <TD  width=209  valign=top style="width:157.0pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Amazon Web Services (AWS)</P>
  </TD>
  <TD  width=576  valign=top style="width:6.0in;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Service roles needed for each account:</P>
  <P  class=MsoListParagraphCxSpFirst style="margin-left:17.0pt;text-indent:in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B>Cost Management Role</B> - Role for
  Cloudability to obtain additional usage metrics from accounts. </P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.0pt;text-indent:in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B>Security Audit Role</B> – The role for the
  global security audit tool (read only).</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.0pt;text-indent:"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B>Trust Role</B> – The trust to Layer 1 to enable
  provisioning.</P>
  <P  class=MsoListParagraphCxSpMiddle style="margin-left:17.0pt;text-indent:"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B>VPC Flow Logs</B> – Used for network
  monitoring.</P>
  <P  class=MsoListParagraphCxSpLast style="margin-left:17.0pt;text-indent:"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp
  </SPAN></SPAN></SPAN><B>Governance</B> – Used to perform automated
  remediation.</P>
  </TD>
 </TR>
 <TR>
  <TD  width=209  valign=top style="width:157.0pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Azure</P>
  </TD>
  <TD  width=576  valign=top style="width:6.0in;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Roles created within each subscription:</P>
  <P  class=MsoListParagraph style="text-indent:in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B>Custom RBAC Administrator</B> – Cross
  subscription service account allowing deployment and management of custom
  RBAC roles. Allows DCS to create new subscriptions automatically with defined
  custom roles.</P>
  <P  class=MsoNormal>Deployed by default:</P>
  <P  class=MsoListParagraphCxSpFirst style="text-indent:in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B>Resource Lock Operator</B> – Allows prevention
  of changes to a resource.</P>
  <P  class=MsoListParagraphCxSpLast style="text-indent:.in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B>VM Network Attacher</B> – Allows a VM to
  join a centrally managed virtual network. </P>
  <P  class=MsoNormal>Service accounts used when an account is compromised and
  assists with resolving concerns. Service accounts are vaulted. All access is
  logged. </P>
  <P  class=MsoListParagraphCxSpFirst style="text-indent:in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B> Management Group Contributor</B> – Manages
  Azure Management Groups and Azure Policies. No access to subscriptions.</P>
  <P  class=MsoListParagraphCxSpMiddle style="text-indent:in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN>The SOC is in the form of the “atrame\DTTL
  GISO Azure sec” AD group to Security Reader Role.</P>
  <P  class=MsoListParagraphCxSpMiddle style="text-indent:in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B>Account Owner</B> – Allows automated
  creation of subscriptions. Access to the subscriptions are removed after
  initial subscription creation.</P>
  <P  class=MsoListParagraphCxSpMiddle style="text-indent:in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B>Subscription Owner</B> – Built-in “root”
  account used for emergencies only. The password is managed in ‘secret server’
  with MFA and workflow approval needed access.</P>
  <P  class=MsoListParagraphCxSpLast style="text-indent:in"><SPAN style="font-family:Symbol"><SPAN>·<SPAN style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  </SPAN></SPAN></SPAN><B>Security Reader and Monitoring Reader </B>–
  For resource inventory purposes. Does not allow access to data or VMs and
  cannot modify any services. </P>
  </TD>
 </TR>
 <TR>
  <TD  width=209  valign=top style="width:157.0pt;border:solid windowtext 1.0pt;border-top:none;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>Google Cloud Platform (GCP)</P>
  </TD>
  <TD  width=576  valign=top style="width:6.0in;border-top:none;border-left:none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0in 5.4pt 0in 5.4pt">
  <P  class=MsoNormal>None defined at this time.</P>
  </TD>
 </TR>
</TABLE>

