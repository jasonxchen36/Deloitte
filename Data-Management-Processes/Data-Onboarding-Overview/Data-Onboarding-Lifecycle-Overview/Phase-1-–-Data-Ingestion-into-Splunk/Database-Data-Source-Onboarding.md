#Database Data Source Onboarding:

  - Use DB Connect from Splunkbase
    - If DB Connect will not work, reach out to Deloitte Global FC Engineering
  - Work with data source owner to determine database details
    - Type of database (e.g., Oracle, MySQL)
    - Table details
      - Query to pull
      - Table names
      - Fields
    - Credentials from the data source owner
    - IP/domain
    - Port (e.g., McAfee EPO TCP 1433)
    - FW rule to allow connectivity to database
  - Configure database details in DB Connect and enable the connection
  - For existing or new data source, refer to General steps section below
  - Work with data source owner to validate that logs are being received in Splunk 