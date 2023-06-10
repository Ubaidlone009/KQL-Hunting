
# Look for new services installed

This query can be used to hunt for new services installed on an endpoint.


## Query

```KQL

DeviceEvents
| where ActionType contains "service"
|extend ServiceName=  tostring(parse_json(AdditionalFields).ServiceName)
| project DeviceName, ActionType, ServiceName

```


