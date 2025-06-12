#Standard Operating Procedure (SOP): When to Engage Splunk Support vs. Internal Investigation

**Purpose** 
-------------------------------------------------------------------------------------------
This SOP has been prepared by the Splunk Account Team, and outlines the criteria for Deloitte to determine when they should engage **Splunk Support** versus when they should conduct an **internal investigation** regarding issues with their environment.

**Scope** 
-------------------------------------------------------------------------------------------
This applies to **all** Splunk Cloud users, including administrators, security analysts, IT operations, and developers responsible for data ingestion, search optimization, and system health.

* * *

When to Conduct an Internal Investigation
=========================================

Before opening a Splunk Support case, the following steps should be taken **internally** to ensure the issue is not related to search hygiene, data pipeline misconfigurations, or user-specific errors.

1.1 Search Performance & Hygiene Issues
---------------------------------------

Investigate internally if:
*   Searches are running slowly but completing successfully.
*   Scheduled searches or reports are failing due to excessive resource consumption.
*   Search queries contain inefficient commands (e.g., too many wildcards, unnecessary `join` operations, lack of indexed fields).
*   Dashboards are taking too long to load due to complex queries.
*   Users are experiencing differences in search results due to time range, permissions, or dataset variations.
**Recommended Internal Actions**:
*   Use the **Job Inspector** to review search execution details.
*   Optimize searches by reducing unnecessary `join`, `transaction`, or non-indexed fields.
*   Use `tstats` for accelerated searches where applicable.
*   Review documentation on search best practices (e.g., _Splunk Search Optimization Guide_).

1.2 Data Ingestion & Pipeline Issues
------------------------------------

Investigate internally if:
*   Data is not appearing in Splunk but there are no indexer-related error messages.
*   Fields are not extracting properly, but data is present in raw logs.
*   Ingested data is incorrect due to source misconfiguration.
*   Parsing and transformation errors occur at the Heavy Forwarder or Universal Forwarder.
*   Data is delayed, but there are no system-wide health alerts.
**Recommended Internal Actions**:
*   Verify indexing queue status using the **Monitoring Console**.
*   Check Forwarder and Indexer logs (`splunkd.log`, `metrics.log`, `index=_internal` searches).
*   Validate parsing rules and field extractions using **Field Discovery** and **Regex101**.
*   Review `props.conf` and `transforms.conf` settings.

1.3 User Access & Role Issues
-----------------------------

Investigate internally if:
*   Users are unable to access certain indexes or saved searches due to role-based restrictions.
*   Dashboard permissions are inconsistent between teams.
*   API queries return permission errors for specific endpoints.
**Recommended Internal Actions**:
*   Review role-based access control (RBAC) settings in Splunk Web.
*   Use REST endpoint `/services/authentication/users` to verify user roles.
*   Check the _Splunk Cloud Admin Guide_ for permission configuration.

* * *

When to Engage Splunk Support
================================

If internal investigation does not resolve the issue or points to a platform-related failure, engage Splunk Support.

2.1 Splunk Platform Issues
--------------------------

Engage Splunk Support if:
*   Splunk Cloud is unavailable or experiencing major outages.
*   UI components (Search Head, Indexers, Forwarders) are unresponsive or returning HTTP 500/502 errors.
*   Authentication and SSO integration failures persist despite correct configuration.
*   The Monitoring Console reports degraded health (e.g., excessive CPU, memory, or disk utilization) unrelated to search load.

2.2 Data Indexing & Search Failures
-----------------------------------

Engage Splunk Support if:
*   Data ingestion is failing at the Indexer level without any clear forwarder-side issues.
*   Search results are missing for all users despite proper index permissions.
*   Saved searches or scheduled reports are failing without user-induced errors.
*   The KV Store or Data Model Acceleration is not functioning correctly despite internal troubleshooting.

2.3 Enterprise Security & Cloud-Specific Issues
-----------------------------------------------

Engage Splunk Support if:
*   Correlation searches in Splunk Enterprise Security (ES) are not triggering properly despite correct configurations.
*   Splunk Cloud admin tools are missing or returning errors when accessed.
*   SmartStore data is not retrieving from remote storage as expected.
*   SOAR, ITSI, or UBA components are not integrating correctly despite valid configurations.

2.4 Licensing & Billing Issues
------------------------------

Engage Splunk Support if:
*   License usage is incorrect or Splunk Cloud usage reports an unexpected overage.
*   Your instance is unable to process logs due to licensing restrictions despite having available capacity.
*   Subscription-related questions or provisioning changes are required.

* * *

How to Engage Splunk Support
===============================

If the issue meets the criteria for support engagement, follow these steps:

3.1 Submitting a Support Ticket
-------------------------------

1.  Log in to the **Splunk Support Portal**: [Splunk Support](https://www.splunk.com/en_us/support.html)
2.  Click **Create a Case** and provide the following details:
    *   **Issue Description**: Clearly explain the problem, impact, and when it started.
    *   **Environment Details**: Splunk Cloud version, affected indexes/searches, and relevant logs.
    *   **Troubleshooting Steps Taken**: List actions attempted internally before opening the case.
    *   **Severity Level**:
        *   **Severity 1 (Critical)**: Complete outage or severe business impact.
        *   **Severity 2 (High)**: Major function impaired, affecting multiple users.
        *   **Severity 3 (Medium)**: Non-urgent issue with a workaround.
        *   **Severity 4 (Low)**: General questions or feature requests.
    **Note**: For Severity 1 cases, always default to opening via the **Splunk Hotline**, for the fastest response.

3.2 Escalation Process
----------------------

*   If the issue is not being addressed timely, request an **Escalation Manager** via the Splunk Support Portal or Hotline.
*   Contact your **Splunk Technical Success Engineer** for assistance with support case management / escalation.

* * *

Summary Decision Matrix
==========================

| **Issue Type** | **Investigate Internally** | **Engage Splunk Support** |
| --- | :-: | :-: |
| Slow or inefficient searches | Yes | No |
| Data not appearing in Splunk | Yes (check pipeline) | If indexing fails |
| UI unresponsive (500 errors) | No | Yes |
| Permission issues | Yes | No |
| License usage problems | No | Yes |
| Cloud outage or major failure | No | Yes |
| Correlation searches failing | Yes (check config) | If persists |

* * *

Conclusion
==========

By following this SOP, Deloitte can efficiently determine whether to investigate an issue internally or engage Splunk Support. This ensures optimal resolution times and minimizes downtime.