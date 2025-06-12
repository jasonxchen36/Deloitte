As a part of the effort of migrating from Enterprise to Cloud, the ldapsearch command has been impacted with this change, since it doesn't work on Cloud, normally, we used ran this command on the Search Heads, but with Cloud, we have to use our Heavy Forwarders and then route those results to Cloud's Search Heads.

**What's ldapsearch?**

Is a command that make inquiries to Active Directory and it give's any info regarding an user (mail, role, telephone, etc.)

**Location of ldapsearch configurations** for **EMEA Cloud** and **AMER** moving into Cloud:

EMEA: az1436l035

Hostname: AZ0001AME006.atrame.deloitte.com

We use the best HF regarding connectivity with the domain controllers, the HF with the least latency is 035.

With the AMER Migration into EMEA Cloud, we'll use this HF for both instances, regarding **APAC Cloud**, this is the location of the configurations until we merge all instances into EMEA Cloud:

APAC: aw1436l036


NOTE: We'll update this Wiki document once we merge all instances into EMEA Cloud.









