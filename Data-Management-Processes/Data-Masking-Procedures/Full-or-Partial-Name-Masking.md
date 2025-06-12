## *** IMPORTANT ***
****
Any masked data must have the following field replacement as its value to reflect parity with the Fusion Center analyst playbooks: **<redacted>**
***
 
The below process applies to when a full or partial name appears within ingested logs and the information can be used to correlate against user data. If you suspect that name masking is required, please reach out to your respective team lead with examples. 

Service account names do not need to be masked.

<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">There are two ways to mask or anonymize data in Splunk, at search time or index time. It is the preference and requirement for Global Fusion Center Engineers to implement any data masking at index time and <strong>not</strong> at search time. All data masking efforts must be performed in DEV and then later implemented in PROD once all configurations are confirmed working.</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">Search time data masking has the following issues which is why it is not recommended:</span></p>
<ul style="list-style-type: disc;margin-left:undefined;">
  <li><span style="font-family: Calibri, sans-serif; font-size: 14px;">It is resource intensive on a search head to perform the masking and replacement of fields within _raw&nbsp;</span></li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">It has to be implemented on <strong>all</strong> search heads in the environment&nbsp;</span></span></li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">Most importantly, search time data masking is not full-proof and there will always be a way to circumvent the masking</span></span></li>
</ul>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">Index time data masking can be performed either during the parsing segment on a HF/UF or directly on an index cluster by pushing configurations from the ICM.&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;">
  <br>
</p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">There are important caveats for implementing masking at the UF level or at the indexer level:&nbsp;</span></p>
<ul style="list-style-type: disc;margin-left:undefined;">
  <li><span style="font-family: Calibri, sans-serif; font-size: 14px;">Splunk indexers do not parse structured data</span>
    <ol style="list-style-type: circle;">
      <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-family:;font-size:10.5pt;">When you forward structured data (e.g. JSON) to an indexer, the indexer does not parse it. Forwarded data skips the following queues on the indexer, which precludes data parsing:</span></span>
        <ul style="list-style-type: square;">
          <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">Parsing</span></span></li>
          <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">Aggregation</span></span></li>
          <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">Typing</span></span></li>
        </ul>
      </li>
      <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-family:;font-size:10.5pt;">The forwarded data must arrive at the indexer already parsed by configuring a props.conf on the forwarder that sends the data.</span></span></li>
    </ol>
  </li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">Splunk universal forwarders can only parse unstructured data</span></span>
    <ol style="list-style-type: circle;">
      <li><span style="font-size: 10.5pt; font-family: Calibri, sans-serif;">If the UF is forwarding unstructured data (e.g. syslog) to the index cluster, then the data masking can be performed on the UF level if and only if the INDEXED_EXTRACTIONS attribute is used &nbsp;</span></li>
    </ol>
  </li>
</ul>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">Splunk HFs can parse structured or unstructured data, which makes them the easiest location to perform data masking. The location in which you will have to implement any data masking will depend on the ingest path for the data source. It is <strong>highly</strong> recommended you perform data masking as part of the data onboarding process, and not retroactively.</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:15px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><strong><span style="font-size:27px;">Anonymize Data</span></strong></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">There are two methods to implement data masking with Splunk Enterprise:</span></p>
<div style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;">
  <ul style="margin-bottom:0in;list-style-type: disc;margin-left:undefined;">
    <li style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-family: Calibri, sans-serif; font-size: 14px;">Use the SEDCMD like a sed script to do replacements and substitutions. The sed script method is easier to do, takes less time to configure, and is slightly faster than a transform. But there are limits to how many times you can invoke SEDCMD and what it can do. For instructions on this method, see 
        <a href="http://docs.splunk.com/Documentation/Splunk/7.3.3/Data/Anonymizedata#Anonymize_data_with_a_sed_script"><span style="color:#2A80B9;">Anonymize data with a sed script</span></a>. Using SEDCMD is the easiest method and the preferred method to use when possible.
      </span></li>
  </ul>
</div>
<p style="margin-top:0in;margin-right:0in;margin-bottom:.0001pt;margin-left:.5in;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size:14px;color:black;">&nbsp;</span></span></p>
<div style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;">
  <ul style="margin-bottom:0in;list-style-type: disc;margin-left:undefined;">
    <li style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">Use a regular expression (regex) transform. This method takes longer to configure, but is easier to modify after the initial configuration and can be assigned to multiple data inputs more easily. For instructions on this method, see</span>&nbsp;
        <a href="http://docs.splunk.com/Documentation/Splunk/7.3.3/Data/Anonymizedata#Anonymize_data_with_a_regular_expression_transform"><span style="color:#2A80B9;">Anonymize data with a regular expression transform</span></a>
      </span></li>
  </ul>
</div>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size: 14px; color: black; font-family: Calibri, sans-serif;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><strong><span style="font-size:27px;">Key Points to Anonymizing Data</span></strong></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif; border-box;font-variant-ligatures: normal;font-variant-caps: normal;orphans: 2;text-align:start;widows: 2;-webkit-text-stroke-width: 0px;text-decoration-style: initial;text-decoration-color: initial;word-spacing:0px;"><span style="font-size:14px;">Before you can anonymize data, you must select a set of events to anonymize.</span></p>
<ul style="list-style-type: disc;margin-left:undefined;">
  <li><span style="font-family: Calibri, sans-serif; font-size: 14px;">You use props.conf to select the events to anonymize</span></li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">You then use props.conf to anonymize the events with a sed script</span></span></li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">Or, you use props.conf&nbsp;and transforms.conf to anonymize the events with a regular expression transform</span></span></li>
</ul>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><strong><span style="font-size:14px;color:#2D2D2D;">&nbsp;</span></strong></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><strong><span style="font-size:21px;">Select Events to Anonymize</span></strong></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">You can anonymize event data based on whether the data comes from a specific source or host, or is tagged with a specific source type. You must specify which method to use in&nbsp;props.conf. The stanza name that you specify in&nbsp;props.conf&nbsp;determines how Splunk Enterprise selects and processes events for anonymization.</span></p>
<ul style="list-style-type: disc;margin-left:undefined;">
  <li><span style="font-family: Calibri, sans-serif; font-size: 14px;">[host::&lt;host&gt;] matches events that contain the specified host</span></li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">source::&lt;source&gt;&nbsp;matches events with the specified source</span></span></li>
  <li><span style="font-family: Calibri, sans-serif; font-size: 14px;">&lt;sourcetype&gt; matches events with the specified source type. You must specify the source type in inputs.conf for this stanza type to work. This option is a Splunk best practice.</span></li>
</ul>
<p style="margin-top:0in;margin-right:0in;margin-bottom:.0001pt;margin-left:.5in;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><strong><span style="font-size:21px;">Replace Strings in Events with SEDCMD</span></strong></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif; border-box;font-variant-ligatures: normal;font-variant-caps: normal;orphans: 2;text-align:start;widows: 2;-webkit-text-stroke-width: 0px;text-decoration-style: initial;text-decoration-color: initial;word-spacing:0px;"><span style="font-size:14px;">You can use the&nbsp;SEDCMD&nbsp;method to replace strings or substitute characters. The syntax for a&nbsp;sed&nbsp;replace is:</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif; border-box;font-variant-ligatures: normal;font-variant-caps: normal;orphans: 2;text-align:start;widows: 2;-webkit-text-stroke-width: 0px;text-decoration-style: initial;text-decoration-color: initial;word-spacing:0px;"><span style="font-size:14px;">SEDCMD-&lt;class&gt; = s/&lt;regex&gt;/&lt;replacement&gt;/flags</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif; border-box;font-variant-ligatures: normal;font-variant-caps: normal;orphans: 2;text-align:start;widows: 2;-webkit-text-stroke-width: 0px;text-decoration-style: initial;text-decoration-color: initial;word-spacing:0px;"><span style="font-size:14px;">The SEDCMD command has the following components:</span></p>
<ul style="list-style-type: disc;margin-left:undefined;">
  <li><span style="font-family: Calibri, sans-serif; font-size: 14px;">regex is a Perl language regular expression</span></li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">replacement&nbsp;is a string to replace the regular expression match.</span></span></li>
  <li><span style="font-family: Calibri, sans-serif; font-size: 14px;">flags can be either the letter g to replace all matches or a number to replace a specified match.</span></li>
</ul>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">Example of Azure AD Data masking with SEDCMD by source</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">[source::tenant_id:cfd6034a-a249-4178-be7a-0803526c4a43]</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">SEDCMD-Azure_AD_Name_Mask= s/"identity": "[^,]*, [^,]*"/"identity": "&lt;redacted&gt;"/g &nbsp; s/"userDisplayName": "[^,]*, [^,]*"/"userDisplayName": "&lt;redacted&gt;"/g</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><strong><span style="font-size:21px;">Restrictions for Using the Sed Script to Anonymize Data</span></strong></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif; border-box;font-variant-ligatures: normal;font-variant-caps: normal;orphans: 2;text-align:start;widows: 2;-webkit-text-stroke-width: 0px;text-decoration-style: initial;text-decoration-color: initial;word-spacing:0px;"><span style="font-size:14px;">If you use the&nbsp;SEDCMD&nbsp;method to anonymize the data, the following restrictions apply:</span></p>
<ul style="list-style-type: disc;margin-left:undefined;">
  <li><span style="font-family: Calibri, sans-serif; font-size: 14px;">The SEDCMD script applies only to the _raw field at index time. With the regular expression transform, you can apply changes to other fields.</span></li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">You cannot use more than one&nbsp;SEDCMD&nbsp;type transformation for the same host, source, or source type in a single&nbsp;props.conf&nbsp;file.</span></span></li>
</ul>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><strong><span style="font-size:21px;">Use a Regular Expression Transform with Transforms.conf to Anonymize Events</span></strong></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif; border-box;font-variant-ligatures: normal;font-variant-caps: normal;orphans: 2;text-align:start;widows: 2;-webkit-text-stroke-width: 0px;text-decoration-style: initial;text-decoration-color: initial;word-spacing:0px;"><span style="font-size:14px;">Each stanza in&nbsp;transforms.conf&nbsp;defines a transform class that you can reference from&nbsp;props.conf&nbsp;for a given source type, source, or host.</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif; border-box;font-variant-ligatures: normal;font-variant-caps: normal;orphans: 2;text-align:start;widows: 2;-webkit-text-stroke-width: 0px;text-decoration-style: initial;text-decoration-color: initial;word-spacing:0px;"><span style="font-size:14px;">Transforms have several settings and variables that let you specify what changes and where, but the following are the most important:</span></p>
<ul style="list-style-type: disc;margin-left:undefined;">
  <li><span style="font-family: Calibri, sans-serif; font-size: 14px;">The REGEX setting specifies the regular expression that points to the string in the event that you want to anonymize</span></li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">The&nbsp;FORMAT&nbsp;setting specifies the masked values</span></span></li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">The&nbsp;$1&nbsp;variable represents the text of the event before the regular expression that represents the string in the event that you want to mask</span></span></li>
  <li><span style="font-family: 
        Calibri,sans-serif;"><span style="font-size: 14px;">The&nbsp;$2&nbsp;variable represents the text of the event after the regular expression</span></span></li>
  <li><span style="font-family: Calibri, sans-serif; font-size: 14px;">DEST_KEY = _raw says to write the value from FORMAT to the raw value in the log. This anonymizes the event.</span></li>
</ul>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">Example of Azure AD Data masking with props and transforms:</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">Props.conf</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">[amdl:diagnosticLogs]</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">TRANSFORMS-sourcetype=ms_aad_signin,ms_aad_audit</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">TRANSFORMS-mask=azure_ad_identity_mask, azure_ad_userDisplayName_mask</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">TRUNCATE = 0</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">TIME_FORMAT = %Y-%m-%dT%H:%M:%S.%7QZ</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">TIME_PREFIX = \"time\"\:\"</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">Transforms.conf</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">[azure_ad_identity_mask]</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">REGEX = (.*)(\"identity\")\:(\"[^\,]*, [^\,]*\")(.*)</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">FORMAT =$1$2:"&lt;redacted&gt;"$4</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">DEST_KEY = _raw</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">LOOKAHEAD=100000</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">[azure_ad_userDisplayName_mask]</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">REGEX = (.*)(\"userDisplayName\")\:(\"[^\,]*, [^\,]*\")(.*)</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">FORMAT =$1$2:"&lt;redacted&gt;"$4</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">DEST_KEY = _raw</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">LOOKAHEAD=100000</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><strong><span style="font-size:21px;">Restrictions for Using the Regular Expression Transform to Anonymize Data</span></strong></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif; border-box;font-variant-ligatures: normal;font-variant-caps: normal;orphans: 2;text-align:start;widows: 2;-webkit-text-stroke-width: 0px;text-decoration-style: initial;text-decoration-color: initial;word-spacing:0px;"><span style="font-size:14px;">If you use the regular expression transform to anonymize data, the following restrictions apply, include the LOOKAHEAD setting when you define the transform and set it to a number that is larger than the largest expected event. Otherwise, anonymization could fail.</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">&nbsp;</span></p>
<p style="margin:0in;margin-bottom:.0001pt;font-size:16px;font-family:&quot;Calibri&quot;,sans-serif;"><span style="font-size:14px;">References:</span></p>
<ul style="list-style-type: disc;margin-left:undefined;">
  <li><span style="font-family:&quot;Times New Roman&quot;;">
      <a href="https://docs.splunk.com/Documentation/Splunk/7.3.3/Data/Anonymizedata"><span style="color:blue;">https://docs.splunk.com/Documentation/Splunk/7.3.3/Data/Anonymizedata</span></a>
    </span></li>
  <li><span style="font-family:&quot;Times New Roman&quot;;">
      <a href="https://docs.splunk.com/Documentation/Splunk/8.0.1/Deploy/Datapipeline"><span style="color:blue;">https://docs.splunk.com/Documentation/Splunk/8.0.1/Deploy/Datapipeline</span></a>
    </span></li>
  <li><span style="font-family:&quot;Times New Roman&quot;;">
      <a href="https://docs.splunk.com/Documentation/Splunk/7.3.3/Admin/Propsconf"><span style="color:blue;">https://docs.splunk.com/Documentation/Splunk/7.3.3/Admin/Propsconf</span></a>
    </span></li>
  <li><span style="font-family:&quot;Times New Roman&quot;;">
      <a href="https://docs.splunk.com/Documentation/Splunk/7.3.3/Admin/Transformsconf"><span style="color:blue;">https://docs.splunk.com/Documentation/Splunk/7.3.3/Admin/Transformsconf</span></a>
    </span></li>
</ul>


























































































































































































































