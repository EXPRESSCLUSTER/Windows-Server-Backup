# Create a backup to work with
## Create an immediate backup
1. Launch Windows Server Backup console \(wbadmin.msc\)
2. Select 'Local Backup' in the left pane
3. Choose 'Backup Once...' in the right Actions pane
4. Complete the process to execute the backup

  Commandline options:
  - wbadmin start backup
  - Start-WBBackup \(Powershell\)

### Note about the backup:
- a backup folder named WindowsImageBackup is created on the destination volume when the first backup is created
- a subfolder under that folder is created with the name of the host machine
- other folders and backup files are created under this second folder
- I suspect that the file backup may exist in the .vhdx file in one subdirectory

# Recover files
1. Edit the two source text files
2. Launch Windows Server Backup console
3. Select 'Local Backup' in the left pane
4. Select 'Recover...' in the right Actions pane
5. Choose the location where the backup is stored
6. Select the backup date and time (there may be more than one)
7. Select the recover type of 'Files and folders'
8. Drill down in the directory to choose the file or files to recover
9. Specify recover options:
   - Location = original
   - Overwrite
10. Confirm

Result: Files were restored to state when backup was taken

# Useful Commands and Cmdlets
- Commands using [wbadmin utility](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/wbadmin)
  - **wbadmin get status** - Shows the status of the currently running backup or recovery operation.
- Commands using [PowerShell](https://docs.microsoft.com/en-us/powershell/module/windowsserverbackup/?view=win10-ps)
  - **Get-WBSummary** - Gets the history of backup operations on the computer.
  - **Get-WBJob** - Gets the current backup operation.
  
Although both commands provide a number of data fields in their output, some of the more important ones are included in the table below.

| Command | Output Field Name | | Backup Job Is Running | Recovery Job Is Running | No Job Is Running |
| --- | --- | --- | --- | --- | --- |
| **Get-WBSummary** | *CurrentOperationStatus* | | BackupInProgress | RecoveryInProgress | NoOperationInProgress |
| --- | --- | --- | --- | --- | --- |
| **Get-WBJob** | *JobType* | | Backup | FileRecovery | None |
|  | *JobState* | | Running | Running | Unknown |
  
Both commands output a numerical value for the result of the last backup \(*LastBackupResultHR* and *HResult*\). A 0-value indicates success. The Get-WBJob command can also list the output from previous jobs. Syntax is: Get-WBJob -Previous \<number of jobs to retrieve\>
