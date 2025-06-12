The following Member Firms are noted to have their own DS deployed:
- Mexico
  - `mxmex9851`, `10.49.97.217`, `Windows`
  - RDP using `ATRAME\a-<account>`
  - Note this server is in the `mx.deloitte.com` domain
  - This DS is **colocated** on the one of the two IFs that serve as the "pull" aka "DBConnect" Splunk instances.
  - It is used to serve a number of Mexico DMZ endpoint clients that cannot phone home directly to the AMER DS.
::: mermaid
 graph LR;
  subgraph MEX DMZ
   direction LR
   Z[DMZ Endpoints]
 end
 subgraph MEX
  direction LR
  A[Endpoints]
  subgraph IFs
   direction LR
   B[mxmex9852] & C[mxmex9853] & D{{mxmex9851}}
  end
 end
 A -->|9997/TCP| B & C & M((MTY IFs))
 Z -.->|8089/TCP| D
 Z -->|9997/TCP| B & C
 B & C & D -->|9997/TCP| G((AMER GEMS))
:::
- New Zealand DMZ
  - `nzaklvm142`, `10.52.0.201`, `Windows`
  - RDP using `ATRAME\a-<account>`
  - Note this server is in the `atrapa.deloitte.com` domain
  - This DS serves only Windows DMZ NZ endpoint clients.
  - NZ Linux endpoint clients report to the APAC DS.
::: mermaid
 graph LR;
 subgraph NZ DMZ
  A[Windows Endpoints]
  D[(nzaklvm142)]
  subgraph IFs
   direction LR
   B[nzhlzvm03] & C[nzaklvm141]
  end
 end
 A & B & C -.->|8089/TCP| D
 B & C -->|9997/TCP| G((APAC GEMS))
 A & D -->|9997/TCP| B & C
:::
- The Netherlands
  - `nlams03072`, `10.35.10.7`, `Windows`
  - RDP using `ATRAME\a-<account>`
  - This DS is **colocated** on the IF that serves as the "pull" aka "DBConnect" Splunk instance.
  - It is used to serve a number of Dutch DMZ endpoint clients that cannot phone home directly to the EMEA DS.
::: mermaid
 graph LR;
  subgraph NL DMZ
   Z[DMZ Endpoints]
 end
 subgraph NL
  A[Endpoints]
  subgraph IFs
   B[nlams13072] & C[nlams10050] & D{{nlams03072}}
  end
 end
 A -->|9997/TCP| B & C
 Z -.->|8089/TCP| D
 Z -->|9997/TCP| B & C & D
 B & C & D -->|9997/TCP| G((EMEA GEMS))
:::
- Luxembourg
  - `lulux1782`, `10.125.219.98`, `Linux`
  - SSH using `a-<account>`
  - This DS is **colocated** on one of the two IFs that serve as the "pull" aka "DBConnect" Splunk instances.
  - It is used to serve a number of Luxembourg DMZ endpoint clients that cannot phone home directly to the EMEA DS.
::: mermaid
 graph LR;
  subgraph LU DMZ
   Z[DMZ Endpoints]
 end
 subgraph LU - Kayl DC
  A[Endpoints]
  subgraph IFs
   C[lulux1783] & D{{lulux1782}}
  end
 end
 A -->|9997/TCP| C & D
 Z -.->|8089/TCP| D
 Z -->|9997/TCP| C & D
 C & D -->|9997/TCP| G((EMEA GEMS))
:::
- CBC Relativity
  - `kydiscoverspl1`, `192.168.15.73`, `Linux`
  - Notes:
    - This is a separate and distinct environment from CBC, but the logs from the endpoints are sent to the same cbc_* indexes.
    - One needs to have a local Checkpoint VPN installed. It will be issued by CBC Relativity personnel.
    - In addition one needs to have an Okta account set up by CBC Relativity personnel.  The VPN will use Okta to authenticate and authorize access.
    - Finally, one also needs a separate local CBC Relativity account to access the DS (and IFs).  Request this of the CBC Relativity team as well.
    - Once connectivity via the VPN is established one can use `scp` and `SSH` to transfer files.
    - This DS serves _all_ CBC Relativity endpoint clients, including the two CBC Relativity IFs.
::: mermaid
 graph LR;
 subgraph CBC Relativity
  A[Endpoints]
  D[(kydiscoverspl1)]
  subgraph IFs
   direction LR
   B[kydiscoverspl2] & C[kydiscoverspl3]
  end
 end
 A & B & C -.->|8089/TCP| D
 B & C -->|9997/TCP| G((AMER GEMS))
 A & D -->|9997/TCP| B & C
:::

- Australia (AU-Sydney DMZ and AU-Melbourne DMZ)
  - `ausyddp60165`, `192.168.146.19`, `Linux`
  - `aumeldp60048`, `192.168.46.172`, `Linux`
  - Notes:
    - One needs access to a local account created in each DMZ.
    - Both DMZ DS hosts phone home to the APAC DS for their own Splunk apps.**
    - It should be possible to make them full-tiered DS' to phone home and obtain their clients' apps as well. **[TODO]**
    - Any of the six internal IFs can be used as a jump box to access either DMZ DS host.  Access to the internal IFs is done via SSH using shared accounts **sh_au_splunk** or **splunkgems**  Password: Configured in Thycotic
    - One cannot SSH across DMZs
    - Each DS serves _all_ DMZ endpoint clients for that region (Sydney or Melbourne), including the two DMZ IFs in each region.
    - ** One may wonder why the DMZ DS hosts can connect to the APAC DS, but the DMZ IFs cannot.  Technically, they should be able to do so, but given that the DMZ endpoint clients cannot and require a local DS, it was thought to be easier to let the DMZ IFs use the local DS as well, with a future plan to implement a fully-tiered DS.
::: mermaid
 graph LR;
 AADS[(APAC DS)]
 subgraph SYD DMZ
  SA[Endpoints]
  SD[(ausyddp60165)]
  subgraph SYD DMZ IFs
   direction LR
   SB[ausyddp60163] & SC[ausyddp60164]
  end
 end
 SA -.->|8089/TCP| SD
 SB & SC-->|9997/TCP| G((APAC GEMS))
 SA & SD -->|9997/TCP| SB & SC
 SD & SB & SC -.->|8089/TCP| AADS


 subgraph MEL DMZ
  MA[Endpoints]
  MD[(aumeldp60048)]
  subgraph MEL DMZ IFs
   direction LR
   MB[aumeldp60046] & MC[aumeldp60047]
  end
 end
 MA -.->|8089/TCP| MD
 MB & MC -->|9997/TCP| G((APAC GEMS))
 MA & MD -->|9997/TCP| MB & MC
 MD & MB & MC -.->|8089/TCP| AADS
:::

- Denmark Relativity
  - `DKF-GEMS-01`, `10.0.16.140`, `Windows`. It also acts as an IF.
  - Notes:
    - This is a separate and distinct environment from Denmark, but the logs from the endpoints are sent to the same nord_* indexes.
    - Access to this environment requires the usage of FortiClient VPN. Credentials for it and AD credentials to log into the servers are provided by the firm.
    - This DS serves _all_ Denmark Relativity endpoint clients, including the other IF DKF-GEMS-02.
- I&P  Innovation & Platforms Infrastructure
- GCP