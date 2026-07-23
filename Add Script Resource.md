This guide assumes that you have already created a cluster in EXPRESSCLUSTER.

1. Download the Windows Server Backup script files for mounting and dismounting a volume ([**wsbackup_script.zip**](wsbackup_script.zip)).
2. Unzip the files into a local folder on the primary server.
3. Edit the file **start.bat** and change the variable `dataPartitionLetter` to the drive letter used for the data mirroring disk (example: `dataPartitionLetter=X`).
4. Launch the **EXPRESSCLUSTER WebUI** if it isn't already running, and change the mode from **Operation** mode to **Config** mode.
5. Locate your failover group's name in the tree and click the plus sign to the right of it to add a resource.
6. From the **Type** drop-down menu, select **Script resource**, change **Name** to `wsb_script`, and click **Next**.
7. Verify the "Follow the default dependency" box is selected, then click **Next**.
8. Verify the default **Recovery Operation** options are correct, then click **Next**.
9. Select `start.bat` in the **Details** window and click **Replace**.
10. **Browse** to the files you just downloaded, select `start.bat`, and click **Open**. Click **Yes** to replace the existing file.
11. Click **Add** to add the second script file.
12. Click **Browse**, change the file type from `*.bat` to `All Files (*.*)`, select `start.ps1`, and click **Open**. Click **Save**. The new file should appear in the list.
13. Click **Finish**.
14. Click **Apply the Configuration File**.
15. Click **OK** to perform the operation.
16. Click **OK** to resume the cluster.
17. Change the mode from **Config** back to **Operation** and click the **Status** tab.
18. Expand the new script resource (`wsb_script`) and click the triangle button under the primary server to start the resource.

## Verifying the script ran successfully
After starting the resource, check the EXPRESSCLUSTER cluster log (or the WebUI's alert log) for entries from `wsb_script` confirming the mount/dismount operation completed without error. A failed run typically surfaces as an `ERR`-level log entry referencing an invalid drive letter or a disk that couldn't be located.

## Troubleshooting
- **"Drive Letter is wrong. Please set it as one character."** — the `dataPartitionLetter` value in `start.bat` must be a single letter with no colon or extra characters.
- **"Drive Letter is wrong. It does not exist."** — the specified drive letter doesn't match any currently mounted volume. Confirm the mirror disk resource has come online with the expected letter before the script resource starts.

## About script versioning
The `start.bat` file includes a version comment (e.g. `version : 9.0.3-1`) — this refers to the EXPRESSCLUSTER sample script template version, not the EXPRESSCLUSTER product version (4.1) used elsewhere in this repository. Don't confuse the two when troubleshooting or upgrading.
