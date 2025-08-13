## Powershell - Limited Space Checker v.1
### When run will notify the user if any of the disks are running low on space.  Below 30GB.

```
#------------------Disk Space checker----------------

#Set threshold variable (in GB)

$Space_Threshold = 30             # Minimum GB on drive before alert (ie: if drive has less than 30GB on the drive is in a warning zone)            

#Gather all logical drivers

$drives = Get-WmiObject Win32_LogicalDisk -Filter "DriveType = 3"

#Gathering freespace data from each drive

foreach($totalDrives in $drives) {

$Free_GB = [Math]::Round($drives.FreeSpace /1GB, 2)

if($Free_GB -lt $Space_Threshold) {

Write-Host $($totalDrives.DeviceID) is low on space. $Free_GB GB remaining. -ForegroundColor Red
} else { Write-Host $($totalDrives.DeviceID) is fine on space. $Free_GB free.
}
}

Read-Host -Prompt "Press Enter to exit"

```

