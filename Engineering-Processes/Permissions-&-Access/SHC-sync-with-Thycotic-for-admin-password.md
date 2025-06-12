Currently we are managing our Splunk servers admin account passwords from Splunk, so please note that for SHC we are unable to maintain a unique password for each member in the cluster as the passwd file gets replicated across all members.
Therefore we will be managing password for only one member of the cluster form Thycotic and rest of the SH’s will pick up from it.

Please find the below server list which are active and rotates password for respective environment SHC. 

==================================================================================

|**Active Servers**| **Environment** |
|--|--|
|usatramekj047  | AMER Dev ES SHC |
| usatramekj134 | AMER Staging SHC |
| usatramekj002 | AMER Prod ES SHC |
| EU1436L052 | EMEA Dev SHC |
| EU1436L017 | EMEA Prod Ad Hoc SHC |
|EU1436L069  | EMEA Prod ES SHC |
|ap1436l012 | APAC Prod ES SHC |

                                                        
