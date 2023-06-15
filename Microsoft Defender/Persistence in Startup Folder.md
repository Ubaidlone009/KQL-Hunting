
# Look for additions in Startup folder

This query Looks for events involving the creation of new entries in the startup folder. This is another persistence method where adversaries create new entries in startup folder.


## Query

```KQL

DeviceFileEvents  
| where Timestamp > ago(30d)
| where FolderPath has @"\Windows\Start Menu\Programs\Startup\"
| project Timestamp, DeviceName, FolderPath, FileName 
| top 100 by Timestamp

```


