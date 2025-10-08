# TP Mailbox


## Development Events

- Open Mailbox NUI by a location name as parameter (Location must exist on Config.Locations).
```lua

TriggerEvent("tp_mailbox:client:openMailboxByLocationName", locationName ) -- client to client
TriggerClientEvent("tp_mailbox:client:openMailboxByLocationName", source, locationName ) -- server to client
```

- The specified event sends a telegram to the input target through a server event.
```lua

-- @param senderName : The sender name input.
-- @param senderTelegramId : The sender Telegram ID, you can insert even an invalid telegram id.
-- @param targetTelegramId : The target Telegram ID (ONLY VALID ONES), to send to everyone, use -1 as an input value.
-- @param title, content   : The input text title and content message.
-- @param location         : A valid location / not input from Config.
-- @param stamp            : A valid stamp name from Config.
-- @param anonymous : Required values (0-1), 0 = false, 1 = true
-- @param isJob : Required values (0-1), 0 = false, 1 = true
TriggerEvent('tp_mailbox:server:sendTelegramToTarget', senderName, senderTelegramId, targetTelegramId, title, content, location, stamp, anonymous, isJob) -- SERVER EVENT (Example is Server > Server)
```
