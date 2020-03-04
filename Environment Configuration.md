# Testing Environment
Primary server & Secondary server: Windows Server 2019 Datacenter edition VM
- Attached 5GB VHDX drive (to be used as destination for backup) and mounted it (e.g. drive F:)
- Created folder called 'backup' on C: drive (to store test files to back up)
- Created two text files in 'backup' folder and edited them
- Created subfolder called 'backup2' in 'backup' folder and added a text file to that directory
- Installed the Windows Server Backup feature from 'Add roles and features' in Server Manager

# EXPRESSCLUSTER 4.1 installation and configuration
1. Install EXPRESSCLUSTER 4.1 on both servers, adding a basic license and mirroring license
2. Create a cluster between the primary and secondary servers
3. Create a failover group with a mirror disk, mirroring the 5GB drives on each server (e.g. drive F:)
4. Test to verify that mirroring is functioning properly

# Windows Server Backup configuration
1. Launched Windows Server Backup console by running wbadmin.msc
2. Select 'Local Backup' in the left pane
3. Choose 'Backup Schedule...' in the right Actions pane to launch the Backup Schedule Wizard
4. Click 'Next' to get started
5. Choose the Custom option for the type of configuration since there is no need to back up the whole server
6. Locate and select the two text files and the folder to back up
   - In Advance Settings, choose VSS full backup (VSS settings). This allows for incremental backups.
7. Stay with the default backup schedule of 'Once a day' at 9:00 PM
8. Choose 'Back up to a volume'
9. Choose the VHDX drive added earlier as the Destination Volume (e.g. drive F:)
10. Confirm selections

