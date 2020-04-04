This guide assumes that you have already created a cluster in EXPRESSCLUSTER.
1. Download the Windows Server Backup script files for mounting and dismounting a volume from this site.
2. Unzip the files into a local folder.
3. Edit the file ***Start.bat*** and change the variable **dataPartitionLetter** to the same drive letter used for the data mirroring disk drive \(Example: *dataPartitionLetter=X*\).
4. Launch the **EXPRESSCLUSTER WebUI** if it is not running and change the mode from **Operation** mode to **Config** mode.
5. Locate the %failover_group% name and click the plus sign to the right of it to add a resource.
6. From the **Type** drop down menu, select **Script resource**, change **Name** to *wsb_script*, and click **Next**.
7. Verify the **Follow the default dependency** box is selected, and then click **Next**.
8. Verify the default **Recovery Operation** options are correct, and then click **Next**.
9. Select ***start.bat*** in the **Details** window and click **Replace**.
10.	**Browse** to the files just downloaded, select ***start.bat***, and click **Open**. Click **Yes** to replace the existing file.
11.	Click **Add** to add the second script file.
12.	Click **Browse**, change the file type from ***\*.bat*** to ***All File \(\*.\*\)***, select ***start.ps1***, and click **Open**. Click **Save**. The new file should be in the list.
13.	Click **Finish**.
14. Click **Apply the Configuration File**.
15. Click **OK** to perform the operation. 
16. Click **OK** to resume the cluster.
17. Change the mode from **Config** to **Operation** and click the **Status** tab.
18. Expand the new script name \(*wsb_script*\) and click the triangle button under the primary server to start the resource.
