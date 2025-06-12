#API Data Source Onboarding:

  - Determine Splunkbase TA/app that will be used for API pull
    - If custom API pull is needed, reach out to Deloitte Global FC Engineering
  - Read TA documentation and determine what is needed to enable API pull
  - Common API configuration items
    - Credentials from the data source owner
    - URL/domain
    - Logging level
    - Port (commonly 443, but could vary)
    - FW rule to allow connectivity to API
  - For existing or new data source, refer to General steps section below
  - Work with data source owner to validate that logs are being received in Splunk 