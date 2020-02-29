- I did not test the 'Full server' backup option. 
- Windows Server Backup offers three storage destination types: Hard disk dedicated for backups, Volume, and Shared Network Folder.
The dedicated hard disk type is NOT supported by EXPRESSCLUSTER. Do not use it since a Blue Screen will occur when it is being configured!
- It is best to plan on only having the latest backup snapshot for this solution when there is a need to restore files.
- Once the backup storage, which is mirrored by EXPRESSCLUSTER, is failed over to the standby server, VSS functionality is lost. Meaning that only the LATEST snapshot is available to restore from. If trying to restore files from the remote shared server (secondary server), previous snapshots will not show up as available options for restoration. If the mirrored disk is failed back to the primary server, previous snapshots may be visible, but will not allow the user to select files for restoration (a Shadow Copy cannot be found error will occur).
