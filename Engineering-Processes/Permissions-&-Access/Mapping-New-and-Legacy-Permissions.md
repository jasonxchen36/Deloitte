**Capability and App Roles**
| Legacy Role | New Role(s) | Legacy AD Group | New AD Group | Comments |
|--|--|--|--|--|
| access_management | cpblty_gems_user | sg-giso splunk access_management | sg-amer splunk us_access_management | |
| admin | admin | sg-giso splunk advisory_admin | N/A | |
| advisory | cpblty_gems_engineer | sg-giso splunk advisory | sg-all splunk all_gems_engineer_run; sg-all_gems_engineer_build | |
| advisory_admin | cpblty_gems_admin | N/A | sg-all splunk all_gems_engineer_admin | |
| ca_soc_engineer | cpblty_gems_es_user; app_ca_engineering | sg-amer splunk ca_engineer | sg-amer splunk ca_engineer | |
| can_delete | can_delete | N/A | sg-all splunk all_gems_engineer_delete | |
| default | default | N/A | N/A | |
| ess_admin | Ask Daisy | N/A | N/A | Was disabled? |
| ess_analyst | Ask Daisy | N/A | N/A | Was disabled? |
| ess_user | Ask Daisy | N/A | N/A | Was disabled? |
| executive | cpblty_gems_es_user; app_all_gems_executive | sg-giso splunk executive | sg-all splunk all_gems_executive | |
| gir_team | cpblty_gems_es_user; app_all_gcir | sg-giso splunk gir_team | sg-all splunk all_gcir | |
| incident_response | cpblty_gems_es_user; app_us_ir | sg-giso splunk incident_response | sg-amer splunk us_ir | |
| pam | cpblty_gems_user | sg-giso splunk pam | sg-amer splunk us_pam | |
| power | power | N/A | N/A | Will be disabled |
| securonix_itmpcs | cpblty_gems_user; app_us_securonix | N/A | sg-amer splunk us_securonix | |
| SDO | cpblty_gems_user | sg-giso splunk sdo | sg-amer splunk us_sdo | |
| soc_analyst | cpblty_gems_es_user; app_all_gems_analyst_t1 | sg-giso splunk soc_analyst | sg-all splunk all_gems_analyst_t1 | |
| soc_analyst_tier_2 | cpblty_gems_es_user; app_all_gems_analyst_t2 | sg-giso splunk soc_analyst_tier_2 | | sg-all splunk all_gems_analyst_t2 |
| soc_analyst_tier_3 | cpblty_gems_es_user; app_all_gems_analyst_t3 | sg-giso splunk soc_analyst_tier_3 | | sg-all splunk all_gems_analyst_t3 |
| soc_engineer | cpblty_gems_es_user; app_us_engineering | sg-giso splunk soc_engineer | sg-amer splunk us_engineer | |
| soc_metrics | cpblty_gems_es_user; app_all_gems_metrics | sg-giso splunk soc_metrics | sg-all splunk all_gems_metrics | |
| splunk-system-role | splunk-system-role | N/A | N/A | |
| threat_intel | cpblty_gems_es_user; app_all_gems_ti | sg-giso splunk threat intel | sg-all splunk all_ti | |
| tss | cpblty_gems_user | sg-giso splunk tss | sg-amer splunk us_tss | |
| user | user | N/A | N/A | Will be disabled |

**Capability and App Roles - Decommissioned**
| Legacy Role | New Role(s) | Legacy AD Group | New AD Group | Comments |
|--|--|--|--|--|
| ameausfed | N/A | N/A | N/A | Decommissioned |
| basic | N/A | sg-giso splunk report; sg-amer splunk us_user | N/A | Decommissioned |
| bluelock | N/A | sg-giso splunk bluelock | N/A | Decommissioned |
| dac_analytics | N/A | sg-giso splunk dac_analytics | N/A | Decommissioned |
| delete_capability | N/A | sg-giso splunk delete_capability | N/A | Decommissioned |
| open_cloud | N/A | N/A | N/A | Decommissioned |
| rapid_response | N/A | sg-giso splunk rapid-response | N/A | Decommissioned |
| sc_admin | N/A | N/A | N/A | Decommissioned |
| securonix_us_o365 | N/A | sg-giso splunk securonix | N/A | Decommissioned |
| soc_analyst_es | N/A | sg-giso splunk soc_analyst; sg-giso splunk incident_response; sg-giso splunk soc_analyst_tier_3; sg-giso splunk soc_analyst_tier_2 | N/A | Decommissioned |
| soc_engineer_admin | N/A | N/A | N/A | Decommissioned |
| soc_engineer_es | N/A | sg-giso splunk soc_engineer | N/A | Decommissioned |
| soc_metrics_es| N/A | sg-giso splunk soc_metrics | N/A | Decommissioned |
| software-asset | N/A | N/A | N/A | Decommissioned |
| splunkuba | N/A | N/A | N/A | Decommissioned |
| tc_admin | N/A | N/A | N/A | Decommissioned |
| tc_user | N/A | N/A | N/A | Decommissioned |
| web_protection | N/A | N/A | N/A | Decommissioned |
| windows-admin | N/A | N/A | N/A | Decommissioned |

**API Roles**
| Legacy Role | New Role(s) | Legacy Username | New Username | Comments |
|--|--|--|--|--|
| cyber_recon | cyber_recon; api | uscrlogsvc | uscrlogsvc | |
| globaldc | globaldc; api| glbwindcsvc | glbwindcsvc | |
| index_global_o365_git | index_global_o365_git; apit | glbinsiderthreatsvc | glbinsiderthreatsvc | |
| securonix | securonix; api | sg-giso splunk securonix; ussplunkinsitesvc | ussplunkinsitesvc | |
| uk_cic | uk_cic; api | ukcicprodsvc | ukcicprodsvc | |