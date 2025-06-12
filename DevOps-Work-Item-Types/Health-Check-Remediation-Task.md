**Health Check Remediation**

**What:** Health check remediation tasks are used to track all tasks concerned with troubleshooting Splunk running issues found from health check or daily Splunk operation. These tasks include but not limited to efforts like Splunk performance issue, connectivity issue between Splunk and PAM, Splunk authentication issue, error messages shown during adhoc searches, etc. 
**Area: Splunk\Global FC Deployment Run Team**

**Issues Found:** A short description of the issue found
**Servers Affected:** A list of servers or Splunk server roles affected by this issue
Where to Start: A few steps for run team to re-produce the issue
**Required Info:** 
A few examples of required information by issue category


|**Issue Category**|**Required Information**|
|--|--|
|Search performance issue | 1. Search query 2. Hostname of the server where this issue was found 3. Username of who was running the search 4. (Recommended) A snapshot of job inspection page of the search |
|PAM integration| 1. Hostname of the server which lost connectivity with PAM 2. Username of who tested authentication|
| Splunk web GUI authentication | 1. Hostname of the server where this issue was found 2.Username of who tested authentication |
| Error message | 1. Search query 2. Hostname of the server where this issue was found 3. Username of who was running the search |




![image.png](/.attachments/image-9af908fe-21ea-4031-abd5-2fd6e19646a1.png)