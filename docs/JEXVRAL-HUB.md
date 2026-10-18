# Jexvral Hub

This script works together with Jexvral Account Manager V2
(`projects/Jexvral-Account-Manager V2`). The contract is `docs/HUB.md` in that repo; read it
before changing `src/Core/CloudSync.lua`, `src/Core/HubLive.lua`, `src/Core/UiSchema.lua` or how
`src/Core/ControlRegistry.lua` records controls. These files are copies from
`projects/Base Maclib UI`: change them there first and copy them here.

Loadstring (the key comes from Hub > Loader key on jexvral.xyz):

```lua
getgenv().key = "jxk_..."
loadstring(game:HttpGet("https://jexvral.xyz/game/ap/loader"))()
```

- Configs sync to the member's Hub; the copy on the device always wins, and the website only
  sends a config when the member presses "Sync to device".
- While the script runs, the website lists the session and draws this script's UI (tabs, sub
  tabs, sections, controls) from `UiSchema`; changes there apply in game through
  `ControlRegistry:SetFromRemote`, and changes in game show on the website.
- The default config `main` always exists and cannot be deleted.
- V1 `jam_` keys no longer sync; members make a new key on the V2 website.
