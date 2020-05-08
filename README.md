# Windows Server Backup with EXPRESSCLUSTER X
This project is an attempt to create an inexpensive backup solution which is easy to deploy using Microsoft's Windows Server Backup with NEC's CLUSTERPRO\EXPRESSCLUSTER software. The idea is to use Windows Server Backup to create the initial backup copy of important files and folders. This backup is mirrored to a remote location on a different server by EXPRESSCLUSTER X. Windows Server Backup utilizes VSS, enabling backups created on multiple dates to be saved locally and then restored as needed. If the drive where the backups are stored on the primary server goes down, files can be restored from the remote backup location.

  ![Configuration](Configuration.png)
  
  ![Restore](Restore.png)

What value does this solution provide?
- Basic backup solution
- Backup scheduling
- Inexpensive disks on DR site for data backup

Setup guide

https://github.com/EXPRESSCLUSTER/Windows-Server-Backup/blob/master/Environment%20Configuration.md

How to create backup and restore data from the backup

https://github.com/EXPRESSCLUSTER/Windows-Server-Backup/blob/master/Testing%20Notes.md

Notes

https://github.com/EXPRESSCLUSTER/Windows-Server-Backup/blob/master/Things%20To%20Consider.md
