# Create a backup to work with

## Create an immediate backup
1. Launch the Windows Server Backup console (`wbadmin.msc`).
2. Select "Local Backup" in the left pane.
3. Choose "Backup Once..." in the right Actions pane.
4. Complete the process to execute the backup.

Command-line options:
- `wbadmin start backup`
- `Start-WBBackup` (PowerShell)

### Note about the backup
- A folder named `WindowsImageBackup` is created on the destination volume when the first backup is created.
- A subfolder under that folder is created with the name of the host machine.
- Other folders and backup files are created under this second folder.
- Windows Server Backup stores the backup images as `.vhd`/`.vhdx` virtual disk files within this folder structure — this is the standard, documented storage mechanism for Windows Server Backup, not specific to this configuration.

# Recover files
1. Edit the two source text files.
2. Launch the Windows Server Backup console.
3. Select "Local Backup" in the left pane.
4. Select "Recover..." in the right Actions pane.
5. Choose the location where the backup is stored.
6. Select the backup date and time (there may be more than one).
7. Select the recovery type of "Files and folders."
8. Drill down in the directory to choose the file or files to recover.
9. Specify recovery options:
   - Location = original
   - Overwrite
10. Confirm.

**Result:** files were restored to their state at the time the backup was taken.

**If the expected backup date/time doesn't appear:** see [Things To Consider.md](Things%20To%20Consider.md) — if the mirror disk has been failed over and back without the script resource in place, only the latest snapshot will be available.

# Useful commands and cmdlets
- Commands using the [wbadmin utility](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/wbadmin):
  - `wbadmin get status` — shows the status of the currently running backup or recovery operation.
- Commands using [PowerShell](https://docs.microsoft.com/en-us/powershell/module/windowsserverbackup/?view=win10-ps):
  - `Get-WBSummary` — gets the history of backup operations on the computer.
  - `Get-WBJob` — gets the current backup operation.

Both cmdlets return several output fields; the most relevant are summarized below:

| Command | Output Field | Backup Job Running | Recovery Job Running | No Job Running |
|---|---|---|---|---|
| `Get-WBSummary` | `CurrentOperationStatus` | `BackupInProgress` | `RecoveryInProgress` | `NoOperationInProgress` |
| `Get-WBJob` | `JobType` | `Backup` | `FileRecovery` | `None` |
| `Get-WBJob` | `JobState` | `Running` | `Running` | `Unknown` |

Both commands also output a numerical result code for the last backup (`LastBackupResultHR` and `HResult`). A value of `0` indicates success. `Get-WBJob` can also list output from previous jobs: `Get-WBJob -Previous <number of jobs to retrieve>`.
