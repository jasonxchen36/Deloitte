

[[_TOC_]]
#**Technician 1:**
All the SHs ES SHC / Staging SHC / Stand-alone including BCP.
Restarting procedure each SHC (Staging / Production / Stand-alone) can be done in parallel.
!! Never restart more than 1 member of the same SHC at the same time.


1. **Get Splunk SHC admin password from Thycotic.**

   _Not necessary_  


2. **Check which SH is currently acting as captain.**

       /opt/splunk/bin/splunk show shcluster-status

   **<font color="red">!!</font>** Captain must be restarted last.



3. **Stop Splunk service and reboot machine in every SHC member.**

   **<font color="red">!!</font>** This task must be done sequentially: Only 1 SH can be restarting at the same time.


4. **Check that patches have been applied successfully:**

   A) Run the following commands:

        rpm -qa kernel
        uname -a


   B) Verify the latest kernel version is running:

	![kernel](/.attachments/1-b8cd2b94-3caf-494b-ae91-2fe127ab0250.png)


5. **Check that splunk service is up and running where apply.**
   **<font color="red">!!</font>** Splunk services in BCP servers should remain stopped.

#**Technician 2:**

All PROD Management Servers (except Master Node).
All BCP Management Servers.


   Restarting process for each machine can be done in parallel.
   **<font color="red">!!</font>** Don’t restart PROD Master Node.

1. **Stop Splunk service and reboot machine.**
   This task can be done in parallel.

2. **Check that patches have been applied successfully:**
   A) Run the following commands:

		rpm -qa kernel
		uname -a

   B) Verify the latest kernel version is running:

	![kernel](/.attachments/2-207b8814-e55f-4713-86d6-7ec3dae42189.png)

3. **Check that splunk service is up and running where apply.**

   **<font color="red">!!</font>** Splunk services in BCP servers should remain stopped.

#**Technician 3:**

All UF / HF – UBA

1. **Stop Splunk service and reboot machine in every SHC member.**

   **<font color="red">!!</font>** This task must be done sequentially: Only 1 UF/HF/UBA can be restarting at the same time.

2. **Check that patches have been applied successfully:**

   A) Run the following commands:

		rpm -qa kernel
		uname -a

   B) Verify the latest kernel version is running:

	![3.jpg](/.attachments/3-67c86040-d2de-4951-8923-e1d7abbe522b.png)

3. **Check that splunk service is up and running where apply.**

   **<font color="red">!!</font>** Splunk services in BCP servers should remain stopped.

#**Technician 4:**

PROD Cluster Master & All IDX.

   **<font color="red">!!</font>** Multiple indexers can be restarted only if they are in the same site.

1. **Get Splunk SHC admin password from Thycotic.**

	ap1436l015 and all indexers.

2. **Change the restart timeout setting in Master Node.**

	`/ opt/splunk/bin/splunk edit cluster-config -restart_timeout 300`

3. **Bring splunk <font color="red">offline</font> and reboot machine in every searchpeer.**

   `/ opt/splunk/bin/splunk offline`

   **<font color="red">!!</font>** Don’t stop Splunk.
   **<font color="red">!!</font>** Multiple indexers can be restarted, only if they are in the same site.

4. **Check that patches have been applied successfully:**

   A) Run the following commands:

		rpm -qa kernel
		uname -a

   B) Verify the latest kernel version is running:

	![kernel](/.attachments/4-c9151234-36ef-4769-9219-e0fd85e9330d.png)

5. **Check that splunk service is up and running where apply.**

   **<font color="red">!!</font>** Splunk services in BCP servers should remain stopped.

6. **Restore the restart timeout setting in Master Node.**

      `/ opt/splunk/bin/splunk edit cluster-config -restart_timeout 60`
