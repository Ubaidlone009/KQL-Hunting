
# Detect Volume Shadow Copy Deletion

This query is inspired by the post here: https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1490/T1490.md
-They have described all the different ways system recovery can be inhibited by an adversary


## Query

```KQL
DeviceProcessEvents
  | where (FileName =~ "vssadmin.exe" and ProcessCommandLine has "delete shadows")
   or (ProcessCommandLine has("bcdedit") and ProcessCommandLine has_any("recoveryenabled no", "bootstatuspolicy ignoreallfailures"))
   or (ProcessCommandLine has "wmic" and ProcessCommandLine has "shadowcopy delete")
   or (ProcessCommandLine has "wbadmin" and ProcessCommandLine has "delete" and ProcessCommandLine has_any("backup", "catalog", "systemstatebackup") )
| project Timestamp, DeviceName, FileName, ProcessCommandLine, AccountName, InitiatingProcessAccountUpn, InitiatingProcessCommandLine, InitiatingProcessParentFileName

```


## Acknowledgements

 - [RedCanary Co](https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1490/T1490.md)
 

