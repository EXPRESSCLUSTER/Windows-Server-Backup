# Create a backup to work with
## Create an immediate backup
1. Launch Windows Server Backup console
2. Select 'Local Backup' in the left pane
3. Choose 'Backup Once...' in the right Actions pane
4. Complete the process to execute the backup

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
   Location = original
   Overwrite
10. Confirm

Result: Files were restored to state when backup was taken
