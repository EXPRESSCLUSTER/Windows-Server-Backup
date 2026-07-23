# Testing Environment

Primary server & Secondary server: Windows Server 2019 Datacenter edition VM

- Attached a 5GB VHDX drive (to be used as the backup destination) and mounted it (e.g. drive F:). Format the volume as NTFS.
- Created a folder called `backup` on the C: drive (to store test files to back up).
- Created two text files in the `backup` folder and edited them.
- Created a subfolder called `backup2` in the `backup` folder and added a text file to that directory.
- Installed the Windows Server Backup feature from "Add roles and features" in Server Manager.

# EXPRESSCLUSTER 4.1 installation and configuration

1. Install EXPRESSCLUSTER 4.1 on both servers, adding a basic license and a mirroring license.
2. Create a cluster between the primary and secondary servers.
3. Create a failover group with a mirror disk resource, mirroring the 5GB drives on each server (e.g. drive F:). Also add a script resource (see [Add Script Resource.md](Add%20Script%20Resource.md)) to maintain snapshots on the mirror disk in the event that the drive is failed over to the standby server and then failed back to the primary server.
4. Set the failover attribute for the group to "Manual Failover." This ensures that the failover group always runs on the Primary server.
5. Test to verify that mirroring is functioning properly.

# Windows Server Backup configuration

1. Launch the Windows Server Backup console by running `wbadmin.msc`.
2. Select "Local Backup" in the left pane.
3. Choose "Backup Schedule..." in the right Actions pane to launch the Backup Schedule Wizard.
4. Click "Next" to get started.
5. Choose the Custom option for the type of configuration, since there's no need to back up the whole server.
6. Locate and select the two text files and the folder to back up.
   - In Advanced Settings, choose the VSS setting appropriate for your environment:
     - **VSS full backup** — clears application transaction logs after a successful backup and lets other VSS-aware backup software recognize this as a full backup point. Recommended when Windows Server Backup is the only backup tool touching these files.
     - **VSS copy backup** — preserves application log files and doesn't affect the backup history seen by other tools. Use this if another backup solution is also protecting the same data.
   - *Verify against your own environment before relying on this distinction operationally — VSS backup-type behavior can vary by application (e.g. SQL Server, Exchange).*
7. Stay with the default backup schedule of "Once a day" at 9:00 PM, or adjust to your requirements.
8. Choose "Back up to a volume."
9. Choose the VHDX drive added earlier as the Destination Volume (e.g. drive F:).
10. Confirm selections.
