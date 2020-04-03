1. Download the Windows Server Backup script files for mounting and dismounting a volume from this site.
2. Unzip the files into a local folder.
3. Edit the file Start.bat and change the variable *dataPartitionLetter* to the same drive letter used for the data mirroring disk drive \(Example: **dataPartitionLetter=X\)**.
4. 
2. Click Add to add a script resource.
3. From the Type drop down menu, select Script resource, change Name to 
4. wsb_script, and click Next.
4.	Verify the Follow the default dependency box is selected, and then click Next.
5.	Verify the default Recovery Operation options are correct, and then click Next.
6.	Select start.bat in the Details window and click Replace.
7.	Browse to the files just downloaded, select start.bat, and click Open. Click Yes to replace the existing file.
8.	Click Add to add the second script file.
9.	Click Browse, change the file type from *.bat to All File (*.*), select start.ps1, and click Open. Click Save. The new file should be in the list.
10.	Click Finish.
