**Security Domains with Splunk Enterprise Security allow you to monitor the events and status of import Security Domain.**  

SIEM Engineering assigned a Security Domain to each and every build content use case. 


|Security Domain| Description  |
|--|--|
| **Access** | Display authentication and access-related data such as login attempts, access control events, and default account activity |
| **Endpoint** | Display endpoint data relating to malware infections, patch history, system configurations, and time sync information |
| **Network** | Display network traffic data provided by devices such as firewalls, routers, network intrusion detection systems, network vulnerability scanners, proxy servers, and hosts |
| **Identity** | Display data from your asset and identity lists as well as the types of sessions in use. |
| **Threat** | Display data from Threat Activity by matching Threat Intelligence Source Events
| **Audit** | Display data related to auditing activity such as GPO, audit logs, and Logging Services


Please use this as **guidance** only:

| **ID** | **Description** | **Description** | **Security Domain** |
|--|--|--|--|
| FC-001 | Endpoint Malware\ Malicious Code | Identify Malware discovered on endpoint during a running, scheduled or on-demand anti-virus scan. Correlate risk level, high, medium, low. Raise alert level if: multiple hosts are infected at once, hosts are re-infected after cleaning and reintroduced to network, a high number of infections are on one computer. **Includes**: Advanced Persistent Threat, Detection of Weaponized Macros, Ransomware, Hidden Malware, Malicious Link, Malware on Removable Media, Multiple Instance of the same Malware, Removable Media, USB Impersonation  | Endpoint
| FC-002 | Unauthorized Email Access | Detect unauthorized access attempts, and unauthorized access, to Deloitte email accounts and mailboxes | Access
| FC-003 | Network Malicious Code | Detection of Malicious Code Traversing through the network | Network
| FC-004 | Suspicious Cloud Management Activity | Detect suspicious cloud services activities such as changes to VMs, key store activity, access to cloud management / root accounts. | Access
| FC-005 | Command Line Interface | Detect the use of the command line on endpoints, servers, and cloud services (e.g., Azure powershell) and correlate with other malicious activity or known malicious commands issued through the shell. | Every 10 min | Threat
| FC-006 | Privilege Access Management Misuse | Detects potential misuse of Deloitte's privileged access management solution (Thycotic Secret Server) | Access
| FC-007 | Suspicious Domain Controller Activities | Detect suspicious behavior (unauthorized software installed, interactive logins, malicious network activity) to domain controllers | Access
| FC-008 | Service Account Monitoring | Detect suspicious service account behavior by monitoring for activity such as logins during non-standard times and service accounts that have not had a password change in x days. | Access/Identity
| FC-009 | Unauthorized Software Installed | Detect the installation of unauthorized software (e.g., password cracker, key logger, Tor, torrent, RAT, nMAP) | Threat
| FC-010 | Suspicious Logon Based on Geography | Detect suspicious logon activity based on geography by identifying login attempts from suspicious locations, login attempts from locations outside of the normal geographical locations for a user account, and unrealistic login attempts based on geography and time (e.g., login attempt is suspicious since the time it takes to travel between the two locations is greater than the time between the two login attempts). | Access
| FC-011 | Data Exfiltration | Detect potential data exfiltration attempts by monitoring the the size and time of outbound communications and uploads to non-sanctioned cloud providers. | Network
| FC-012 | Phishing Attack | Detect attempts to obtain sensitive information from personnel by mail received from unknown senders with supsicous mail headers and/or subject lines which includes (but is not limited to) those disguised as a trustworthy entity | Threat
| FC-013 | Suspicious Log/ Audit Trail Activity | Detect suspicious log/audit trail activity by monitoring for logging service or source stopped or disabled and the deletion or alteration of logs. | Audit
| FC-014 | Suspicious Outbound Communication | Detect suspicious outbound communication such as internal beaconing to external command and control (C2) infrastructure and  unauthorized outbound traffic over well-known ports | Every 6 min | Threat/Network
| FC-015 | Disabled Service | Detect if a mandatory service on an endpoint has been stopped or disabled | Endpoint
| FC-016 | Suspicious Password Reset Activity | Detect suspicious password reset/change activity such as a user account's password changed by another user or a password is reset in less than x hours | Access
| FC-017 | Logon Attempt to Disabled or Ex-Employee Account | Detect attempts to authenticate to disabled or expired accounts | Acces/Identity
| FC-018 | Reconnaissance Detection | Detect potential reconnaissance activity such as port scanning from the Internet and from within the network and potential file and directory enumeration | Network
| FC-019 | DNS | Detect suspicious DNS activity by monitoring for high number of DNS failures, excessive number of DNS queries to the DNS servers, DNS queries from unauthorized sources, DNS zone transfers, and DNS queries to a non-standard port | Network
| FC-020 | Fileless and Memory-Based Attack | Detect fileless and memory-based attacks by leveraging events generated from endpoint detection and response solution | Endpoint
| FC-021 | Web Application Attack | Detect potential web application attacks by correlating events from web and database servers (e.g., SQL, XSS, fuzzing) | Threat
| FC-022 | Non-secure or Custom Encryption Mechanism Used | Detect if a non-secure (e.g., DES) or custom (e.g., substitution cipher script) encryption mechanism is used within Deloitte's environment to provide confidentiality for sensitive data | Network
| FC-023 | Logon Attempt | Detect suspicious logon behavior such as multiple failed logon attempts within x time | Access
| FC-024 | Hardware/Software Inventory | Detect rouge devices on the network by correlating against the configuration management database (CMBD). Leverage the CMDB to detect vulnerable software by correlating against public vulnerability databases | Identity
| FC-025 | Critical File System Changes | Detect critical file system changes to sensitive system and application executables, libraries, sensitive data directories, and configurations. Changes include monitoring of unique file properties such as file hashes and suspicious system alterations (e.g., owner and permissions changes to files or directories or the introduction of extra files into key system areas) | Endpoint
| FC-026 | Suspicious Inbound Communication | Detect suspicious traffic from outside of the organization to internal assets | Network/Threat
| FC-027 | Spoofing | Detect potential spoofing attacks such as Man-in-the-Middle (MiTM) | Network
| FC-028 | Endpoint to Endpoint Communication | Detect network traffic between two endpoints that should not be communicating with each other | Network/Threat
| FC-029 | Network Protocols | Detect network traffic to prohibited network protocols and detect abnormal network traffic for common protocols (e.g.,  SSH traffic in segment with no Linux servers) | Network
| FC-030 | Network Device Configurations | Detect unauthorized alterations to firewall, router, and switch configurations | Endpoint
| FC-031 | URL Filtering Proxy System | Detect malicious activity to URLs that are not blocked by URL Filtering Proxy System | Threat/Network
| FC-032 | Mobile Threat Management | Detect and identify indicators of compromise on mobile devices. | Endpoint
| FC-033 | Vulnerability Management System | Detect potential security incidents by correlating true positives from vulnerability scanning results with other security events | Threat
| FC-034 | Suspicious Account Management Activity | Detect suspicious account management activity such as a new user account created on multiple hosts, new local administrator account created, and accounts that have been deleted a short time after creation | Access/Identity
| FC-035 | Changes to Sensitive AD Groups | Detect changes to sensitive AD groups | Identity