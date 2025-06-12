Below instructions make reference to the general procedure when pushing changes to DMC servers:

usatramekj147
|eu1436l035 >> **EMEA DMC Brach deprecated. Apps merged to SHC_EMEA brach.**
|ap1436l035 >> **APAC DMC Brach deprecated. Apps merged to SHC_APAC brach.**|

from branches:

DMC_AMER
DMC_EMEA   >> **Deprecated**
DMC_APAC   >> **Deprecated**


1 - Create a backup of the directory /opt/splunk/etc/apps

2 - Go to /opt/splunk/git/DMC

3 - Perform a "git pull"

4 - Copy the files edited from the previous pull from /opt/splunk/git/DMC/ into /opt/splunk/etc/apps


