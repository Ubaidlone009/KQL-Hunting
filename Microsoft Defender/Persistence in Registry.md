
# Check for Persistence in Registry

This query Looks for events involving the creation of new entries in the run/ run once registry.


## Query

```KQL

DeviceRegistryEvents 
| where Timestamp > ago(30d) // Set time frame here
//| where DeviceName =~"DevExample"  // Device name can be filtered here
| where ActionType == "RegistryValueSet" or ActionType == 'RegistryKeyCreated'  
| where isnotempty( RegistryValueData)      //exclude empty reg Values
| where RegistryKey has @"Microsoft\Windows\CurrentVersion\RUN"
//| summarize ComputerCount=dcount(DeviceName), DeviceNames=makeset(DeviceName) by  RegistryValueData, RegistryKey
//| top 100 by ComputerCount
| project Timestamp, DeviceName, RegistryKey, RegistryValueData

```

## Appendix

Tampering with the Windows registry is probably the most common and transparent way to set up persistent access to a windows machine. Using the registry we can execute batch files, executables and even exported functions in DLL's. Before we get started;  the difference between "HKEY_LOCAL_MACHINE" (HKLM) and "HKEY_CURRENT_USER" (HKCU): HKLM keys are run (if required) every time the system is booted while HKCU keys are only executed when a specific user logs on to the system.

Links:

Userinit - [here](https://technet.microsoft.com/en-us/library/cc939862.aspx)

Run and RunOnce Registry Keys - [here](https://msdn.microsoft.com/en-us/library/aa376977(v=vs.85).aspx)


The usual suspects:
	
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run]
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce]
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices]
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce]
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon]

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run]
[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce]
[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices]
[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce]
[HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\Winlogon]

