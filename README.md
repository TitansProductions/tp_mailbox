# TP Mailbox


## Events

Open Mailbox NUI by a location name as parameter (Location must exist on Config.Locations).
```lua

TriggerEvent("tp_mailbox:client:openMailboxByLocationName", locationName ) -- Client Side
TriggerClientEvent("tp_mailbox:client:openMailboxByLocationName", source, locationName ) -- Server Side
```
