# Development API

Before reading client and server exports and events, you can also edit specific code through `escrow_ignore.lua` files that we provide in client and server directory folders.

## CLIENT:

### Exports

API Getter Function

```lua
local MailboxAPI = exports.tp_mailbox:getAPI()
```

1. Get player telegrams.

```lua
local telegrams = MailboxAPI.GetPlayerTelegrams()
```

### Events

- Open Mailbox NUI by a location name as parameter (Location must exist on Config.Locations).
```lua

--- @param locationName - requires the custom location name from Config.Locations.
TriggerEvent("tp_mailbox:client:openMailboxByLocationName", locationName ) -- client to client
TriggerClientEvent("tp_mailbox:client:openMailboxByLocationName", source, locationName ) -- server to client
```

To create a valid custom config location for opening through the event:

```lua
    ['custom'] = { -- Add your custom name
        Name = "Custom Office", -- Add your custom name

        Coords = {x = 0.0, y = 0.0, z = 0.0},

        City = "Your Custom Title",

        Hours = { Enabled = false, Duration = {am = 7, pm = 21} }, -- NO HOURS

        BlipData = { -- NO BLIP
            Enabled = false,
            Sprite = 1861010125,
        },

        NPCData = { -- NO NPC
            Enabled = false,
            Model = "",
            Coords = {x = 0.0, y = 0.0, z = 0.0, h = 0.0},
        },

        -- Set to true if you are using target eye for opening the mailbox office. 
        -- (!) Required an NPC Enabled, otherwise must be set to false.
        TargetEye = { Enabled = false, Script = '', Display = ''}, -- version 3.1.7 (NO TARGET EYE)

        ActionDistance = 0.0,
    },
```

## SERVER:

### Exports

API Getter Function

```lua
local MailboxAPI = exports.tp_mailbox:getAPI()
```

1. Get player registration id (Unique Player Telegram Id)

```lua
--- @param source int - Requires the player online id.
local telegramId = MailboxAPI.GetPlayerRegistrationId(source)
```

2. Get player total unread telegrams length.

```lua
--- @param telegramId string - Requires the player telegram unique id.
local unreadTelegramsCount = MailboxAPI.GetPlayerUnreadTelegramsLength(telegramId)
```

3. Get player total unpaid telegram bills length.

```lua
--- @param telegramId string - Requires the player telegram unique id.
local unpaidTelegramsCount = MailboxAPI.GetPlayerUnpaidTelegramBillsLength(telegramId)
```

4. Send a telegram (use -1 to everyone)

```lua
--- @param senderTelegramId string - Requires telegram user id of the sender.
--- @param targetTelegramId string - Requires telegram user id of the target ( -1 for sending to everyone ).
--- @param senderName       string - Requires the sender name.
--- @param title            string - Requires the telegram title subject.
--- @param content          string - Requires the telegram content (description - message area) for explaining the subject
--- @param location         string - Requires a location name (You can also set it to "" just dont ignore it)
--- @param stamp            string - Requires a valid stamp name from Config.Stamps.
--- @param anonymous        int    - Requires an integer value ( 0 = not anonymous, 1 = is anonymous).
--- @param isJob            int    - Requires an integer value ( 0 = not job, 1 = is job).
--- @param isBill           int    - Requires an integer value ( 0 = not bill, 1 = is bill).
--- @param billType         string - Requires a billing type - this will be used for sending the money through a type when checking which is making it easier.
--- @param billCost         int    - Requires a valid billing cost.
MailboxAPI.SendTelegram(senderTelegramId, targetTelegramId, senderName, title, content, location, stamp, anonymous, isJob, isBill, billType, billCost)
```

5. Send a parcel (use -1 to everyone)

```lua

--- @param senderTelegramId string - Requires telegram user id of the sender.
--- @param targetTelegramId string - Requires telegram user id of the target ( -1 for sending to everyone ).
--- @param senderName       string - Requires the sender name.
--- @param title            string - Requires the telegram title subject.
--- @param content          string - Requires the telegram content (description - message area) for explaining the subject
--- @param location         string - Requires a location name (You can also set it to "" just dont ignore it)
--- @param stamp            string - Requires a valid stamp name from Config.Stamps.
--- @param inputCost        int    - Requires a cost for the target to pay for receiving its contents.
--- @param parcelContents   table  - Requires a table form of the sent parcel item contents.

--- {name = {item name}, label = { item label }, quantity = { item quantity } }
MailboxAPI.SendParcel(senderTelegramId, targetTelegramId, senderName, title, content, location, stamp, inputCost, parcelContents)
```
