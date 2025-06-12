To meet member firm policies and standards, there are several capabilities considered by each member firm planning to utilize the Deloitte Cloud Service (DCS) platform. The capabilities are Layer 1 – Member Firm Guardrails.

Information within this wiki comes from the following url and was replicated in the instance the reference material is no longer available: <A href="https://resources.deloitte.com/sites/onetechnology/Documents_New/Business_of_IT/OneCloud/Tech-MF-Guardrails.pdf">https://resources.deloitte.com/sites/onetechnology/Documents_New/Business_of_IT/OneCloud/Tech-MF-Guardrails.pdf</A>

NOTE: For a detailed list of policies, please reference the <A  href="https://resources.deloitte.com/sites/onetechnology/Pages/Business_of_IT/OneCloud/OneCloud_gettingStarted.aspx">Getting started with OneCloud </A>main page. 

## Guardrail Capabilities

Utilize the following links to view platform **Layer 1 – Member Firm Guardrails** used by the U.S. member firms. DCS developed <A href="https://resources.deloitte.com/sites/onetechnology/Documents_New/Business_of_IT/OneCloud/Tech-APIs.pdf"> application programming interfaces (APIs)</A> enabling member firm adoption of Deloitte’s approved public cloud vendors.


<table>
<tbody>
<tr>
<td width="300">
<p><strong>Capability</strong></p>
</td>
<td width="484">
<p><strong>Description </strong></p>
</td>
</tr>
<tr>
<td width="240">
<p>Service Management Integration</p>
</td>
<td width="384">
<p>Integration with ServiceNow for RFCs and CMDB automated actions for inventory and traceability.</p>
</td>
</tr>
<tr>
<td width="240">
<p>Security Audits</p>
</td>
<td width="384">
<p>SOC monitored alerts related to misconfigurations based on industry and firm policies.</p>
</td>
</tr>
<tr>
<td width="240">
<p>Identity Access Management</p>
</td>
<td width="384">
<p>SAML identity provider</p>
</td>
</tr>
<tr>
<td width="240">
<p>Activity Logging and Monitoring</p>
</td>
<td width="384">
<p>Account activity logging certain events (i.e., EC2 Create) are logged and forwarded to a central event bus per region.</p>
</td>
</tr>
<tr>
<td width="240">
<p>Backup</p>
</td>
<td width="384">
<p>Enable access to allow application teams to backup and recover instances based on firm recommended guidelines (once daily).</p>
</td>
</tr>
<tr>
<td width="240">
<p>IaaS Orchestration/Automation</p>
</td>
<td width="384">
<p>US Domain Join US Standard Operating System Builds:</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Windows 2016</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; CentOS 7</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RedHat 7</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; SLES 12 Service</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Pack 3 Ubuntu 16.04</p>
</td>
</tr>
<tr>
<td width="240">
<p>VM Agent Compliance Monitoring</p>
</td>
<td width="384">
<p>Windows</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; FireEye &ndash; replaced by Cylance (security related)</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Antivirus &ndash; McAfee replaced by Cylance (security related)</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Patching &ndash; BigFix, SCCM Infrastructure</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Health Monitoring &ndash; SCOM Splunk</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Vulnerability Scanning &ndash; Tenable &amp; Tanium</p>
<p>Linux</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ClamAV</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Splunk</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Winbind (Domain Join)</p>
</td>
</tr>
<tr>
<td width="240">
<p>Member Form Role-Based Access Control (RBAC)</p>
</td>
<td width="384">
<p>Includes platform guardrail roles, plus the creation of standard RBAC roles specific to member firm<em>. </em></p>
<p><em>Roles are subject to change with product maturity.</em></p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>Listed are the capabilities provided at the platform/Layer 1 level. Also, provided are the cloud service provider&rsquo;s technologies supporting each capability.</p>
<p>&nbsp;</p>
<table>
<tbody>
<tr>
<td width="300">
<p><strong>Capability </strong></p>
</td>
<td width="300">
<p><strong>AWS Process/Tools</strong></p>
</td>
<td width="300">
<p><strong>Azure Process/Tools</strong></p>
</td>
<td width="300">
<p><strong>GCP Process/Tools</strong></p>
</td>
</tr>
<tr>
<td width=188">
<p>Service Management Integration</p>
</td>
<td width="145">
<p>Custom ServiceNow library that integrates with platform solutions to automate actions within CMDB. Integration allows proper auditing and traceability.</p>
</td>
<td width="145">
<p>Use of automated compliance tool, OneCOP, ensures traceability of OneCloud portal actions. APIs available for DevOps deployment pipelines.</p>
</td>
<td width="145">
<p>Use of automated compliance tool, OneCOP, ensures traceability of OneCloud portal actions. APIs available for DevOps deployment pipelines.</p>
</td>
</tr>
<tr>
<td width="188">
<p>Security Audits</p>
</td>
<td width="145">
<p>RedLock</p>
</td>
<td width="145">
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; OneCOP Azure</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Security Center</p>
</td>
<td width="145">
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Forseti</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Security Command Center</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Stackdriver</p>
</td>
</tr>
<tr>
<td width="188">
<p>Identity Access Management</p>
</td>
<td width="145">
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Centrify</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AWS IAM User</p>
</td>
<td width="145">
<p>Azure Active Directory (AD)</p>
</td>
<td width="145">
<p>Azure Active Directory (AD)</p>
</td>
</tr>
<tr>
<td width="188">
<p>Activity Logging and Monitoring</p>
</td>
<td width="145">
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AWS CloudWatch</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AWS CloudTrail</p>
</td>
<td width="145">
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Azure Activity</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Monitor Log</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Analytics Event Hub</p>
</td>
<td width="145">
<p>Stackdriver</p>
</td>
</tr>
<tr>
<td width="188">
<p>Backup</p>
</td>
<td width="145">
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; CPM</p>
<p>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AWS Backup</p>
</td>
<td width="145">
<p>Azure Backup</p>
</td>
<td width="145">
<p>To be determined (TBD).</p>
</td>
</tr>
<tr>
<td width="188">
<p>IaaS Orchestration/Automation</p>
</td>
<td width="145">
<p>Cloudscript</p>
</td>
<td width="145">
<p>Use automated compliance tool, OneCOP, ensures traceability of OneCloud portal actions. APIs available for DevOps deployment pipelines.</p>
</td>
<td width="145">
<p>Use of automated compliance tool, OneCOP, ensures traceability of OneCloud portal actions. APIs available for DevOps deployment pipelines.</p>
</td>
</tr>
<tr>
<td width="188">
<p>VM Agent Compliance Monitoring</p>
</td>
<td width="145">
<p>AWS Systems Manager</p>
</td>
<td width="145">
<p>Not applicable; Agents inside the guests.</p>
</td>
<td width="145">
<p>Not applicable (N/A)</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
