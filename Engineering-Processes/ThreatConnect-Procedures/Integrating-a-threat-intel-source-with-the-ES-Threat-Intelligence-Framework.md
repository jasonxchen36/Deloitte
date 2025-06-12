1)	On a development search head, navigate Apps > Enterprise Security > Configure > Data Enrichment > Threat Intelligence Management
2)	Ready your intel download/lookup by searching it in Splunk. Verify that it contains all the fields, aside from “weight” that the Threat Intel kvstore requires according to this documentation: https://docs.splunk.com/Documentation/ES/7.2.0/Admin/Supportedthreatinteltypes
a.	For example, a download feeding into http_intel should contain the following fields: description,http_referrer,http_user_agent,url
3)	Create a new Source
a.	The name cannot contain spaces
b.	Type is arbitrary; we chose threatlist for all ours
c.	Give a useful description 
d.	Insert the proper URL according to the Threat Intel vendor’s specifications—this step will require searching documentation from the Threat Intel vendor
e.	Set the appropriate delimiting regular expression. For csv files, it’s just a comma
f.	Feed “fields” exactly in the order that the Splunk documentation asks for, adding :$<<number>> after each
i.	For example, a download feeding into http_intel should contain the following: description:$1,http_referrer:$2,http_user_agent:$3,url:$4
4)	Save your Intelligence Download, and verify it is properly feeding into Enterprise Security’s kvstore
a.	A good way to do this is searching on the kvstore and filtering by the vendor’s threat_key
b.	You may need to dedup the IOC field in both the download/lookup and kvstore to get a 100% match
5)	SSH into the development search head and navigate to opt/splunk/etc/apps/SplunkEnterpriseSecuritySuite/local/inputs.conf. View this document to make sure it contains stanzas for the indicator downloads you created. If so, copy this file locally to your machine.
6)	Create a Pull Request to add the new indicator download stanza(s) to SHC_AMER_STAGING/SplunkEnterpriseSecuritySuite/local/inputs.conf.
a.	Verification instructions under step 4 are applicable.
7)	After verifying in staging, create a Pull Request to add the new indicator download stanza(s) to SHC_AMER/SplunkEnterpriseSecuritySuite/local/inputs.conf.
a.	Verification instructions under step 4 are applicable.
8)	After verifying in production, you will want to accelerate the IOC fields in the Splunk ES kvstore to increase search-time performance. 
a.	We have already accelerated these fields in our environment so the following steps may not be applicable.
b.	The following documentation is the most comprehensive guide on kvstore configurations published to-date: http://dev.splunk.com/view/webframework-developapps/SP-CAAAEZJ
9)	Create a Pull Request to add the following stanza(s) to SHC_AMER/DA-ESS-ThreatIntelligence/local/collections.conf:
[<kvstore name>]
replicate = true
accelerated_fields.<acceleration name> = {"<IOC field>":1}
Examples can be found here: https://dev.azure.com/GlobalSOC/Splunk/_git/SHC?path=/DA-ESS-ThreatIntelligence/local/collections.conf


