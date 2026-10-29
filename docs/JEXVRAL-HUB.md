# Jexvral Hub

This script works together with Jexvral Account Manager V2
(`projects/Jexvral-Account-Manager V2`). The contract is `docs/HUB.md` in that repo; read it
before changing `src/Core/CloudSync.lua`, `src/Core/HubLive.lua`, `src/Core/HubReadouts.lua`,
`src/Core/UiSchema.lua` or how
`src/Core/ControlRegistry.lua` records controls. These files are copies from
`projects/Base Maclib UI`: change them there first and copy them here.

Loadstring (the key comes from Hub > Loader key on jexvral.xyz):

```lua
getgenv().key = "jxk_..."
loadstring(game:HttpGet("https://jexvral.xyz/game/ap/loader"))()
```

- Configs are the same here and on the website: on start the script sends its configs, writes
  the ones it is missing, deletes the ones deleted on the website and loads the config this
  account uses. Saves, new configs, deletes and loads in game go to the website and on to the
  other running clients. Webhook URLs stay on the device.
- While the script runs, the website lists it on the game's board and draws this script's UI
  (tabs, sub tabs, sections, controls) from `UiSchema`, and can switch it to another config.
- `HubReadouts` sends leaderstats and FPS every 10 seconds when they change; modules can add
  more with `table.insert(ctx.Runtime.Readouts, function() return {name = "Wave", value = n,
  progress = true} end)`. `ControlRegistry:Action(section, settings, flag)` makes a button the
  website can press on many clients.
- V1 `jam_` keys no longer sync; members make a new key on the V2 website.
