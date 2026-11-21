# Integration and exports

[Back to the overview](../README.md)

Every class resource has the same exports. Replace `rklarcher` with the class you call (`rklgods`, `rkldemon`,
`rklmerfolk`, `rklvampire`, `rklwerewolf`, `rklfairyspells`, `rklwitchspells`, `rklelf`, `rklarcher`, `rklkitsune`, `rklpriest`, `rklassassin`).

## Who holds which class

```lua
-- server or client: the class a player holds (one class at a time), set by the class store
local cls = Player(serverId).state['rkl:class']      -- { name = 'archer', grade = 3 } or nil
```

```lua
-- client
exports['rklarcher']:HasClassJob()                 -- -> true while the local player holds this class
-- server
exports['rklarcher']:IsClassBoss(src)              -- -> true for the class leader (the hall's boss rule)
```

Give or take a class from your own script by running the shared command as the console:

```lua
ExecuteCommand(('setclass %d %s %d'):format(src, 'archer', 0))    -- or 'none' to remove
```

## Levels and skill points

```lua
-- SERVER (trusted)
exports['rklarcher']:AddXP(src, amount, reason)    -- -> newLevel, newXp   (nil, why when refused)
exports['rklarcher']:SetLevel(src, level)          -- -> level             (nil, why)
exports['rklarcher']:AddLevel(src, n)              -- -> level             (n may be negative)
exports['rklarcher']:AddSkillPoints(src, n)        -- -> points            (n may be negative, never below 0)
exports['rklarcher']:ResetSkills(src)              -- -> refunded points   (ignores the reset mode)
exports['rklarcher']:GetLevel(src)                 -- -> level, xp, need   (nil when not loaded / not a member)
exports['rklarcher']:GetSkillRank(src, spell)      -- -> rank (0 = none)
-- why: 'off' | 'not_member' | 'loading' | 'bad_amount' | 'bad_level' | 'bad_spell'

AddEventHandler('rklclass:server:levelUp', function(src, class, level) end)   -- server-local

-- CLIENT
exports['rklarcher']:GetLevel()                    -- -> level, xp, need   (nil while not a member / off)
exports['rklarcher']:GetSkillRank(spell)           -- -> rank
exports['rklarcher']:RequestXP(amount, reason)     -- asks the server; only reasons listed in
                                                   --   Config.Levels.clientReasons pass (per-minute cap)
```

Example: give archers XP for a job of your own (server side):

```lua
exports['rklarcher']:AddXP(source, 40, 'hunting_contract')
```

## Combat, statuses and protection

```lua
-- SERVER
exports['rklarcher']:IsPlayerProtected(serverId)          -- is the player shielded by this class right now
exports['rklarcher']:GetProtectionRemaining(serverId)     -- how much of the shield is left
exports['rklarcher']:BlameDamage(victimId, attackerId)    -- name the attacker of your own script damage
exports['rklarcher']:ApplyStatus(target, 'stun', 2000)    -- a class status (root, slow, stun, blind, silence ...)
exports['rklarcher']:GetClassInfo()                       -- id, label, element, essence, accent colour ... (server + client)

-- CLIENT (local player)
exports['rklarcher']:IsProtected()
exports['rklarcher']:GetProtectionRemaining()
exports['rklarcher']:BlameDamage(attackerPed)
exports['rklarcher']:IsCasting()                          -- true during a cast / channel
exports['rklarcher']:HasStatus('root')                    -- a status on the local player
exports['rklarcher']:TryCastSlot(slot)                    -- cast a bar slot from your own key or menu
exports['rklarcher']:IsBarHidden()
exports['rklarcher']:SetBarHidden(true)                   -- hide / show this class's bar
exports['rklarcher']:GetPref(key)                         -- a personal switch from the bar editor
exports['rklarcher']:SetPref(key, on)
```

## Class-specific exports

```lua
-- God
exports.rklgods:IsEnthroned()                             -- client: the local player sits on the Throne of Heaven
exports.rklgods:IsEnthroned(serverId)                     -- server

-- Demon (for a paladin or light class of your own)
exports['rkldemon']:IsDemon(serverId)                     -- server
exports['rkldemon']:GetSouls(serverId)                    -- server / client
exports['rkldemon']:AddHolyZone(coords, radius, ms)       -- server -> id (ms 0 = until removed)
exports['rkldemon']:RemoveHolyZone(id)                    -- server
exports['rkldemon']:AddHellfireZone({ center = coords, radius = 5.0, ms = 6000 })   -- server
exports['rkldemon']:IsInHellfire()                        -- client
Player(serverId).state.rkldemon_souls                     -- souls (any side)
Player(serverId).state.rkldemon_form                      -- set while the Demon Lord form runs

-- Assassin
Player(serverId).state.as_shroud                         -- set while Nightshroud hides her (the server ends it)
```

Each class README (inside the resource) lists the rest of its own exports and state bags.

## The Priest's Rite of Resurrection (revive / ambulance systems)

A priest walks up to a fallen player: **`[E] Rite of Resurrection`** shows over the body. One press of `E`: she kneels, a
5 s cast bar runs, then the **server** checks everything again and calls **your** revive / ambulance system. It is not a
bar spell (the bar keeps its 10 spells + `B`).

**Pick the system** in `rklpriest/config.lua`:

```lua
Config.Revive = {
    Enabled = true,
    system  = 'auto',   -- 'auto' | 'esx_ambulancejob' | 'esx_death' | 'qb-ambulancejob' | 'qbx_medical'
                        -- | 'wasabi_ambulance' | 'ars_ambulancejob' | 'standalone' | 'custom'
    order   = { 'wasabi_ambulance', 'ars_ambulancejob', 'esx_death', 'qbx_medical', 'esx_ambulancejob', 'qb-ambulancejob' },
    custom  = {
        event  = '',          -- e.g. 'myambulance:client:revive'
        target = 'client',    -- 'client' = TriggerClientEvent(event, target, ...args) to the fallen player
                              -- 'server' = TriggerEvent(event, target, ...args) for a server-side handler
        args   = {},          -- extra arguments after the target, e.g. { true }
    },
    -- channelMs (5000), range (2.5), faithCost (30), cooldownMs (60000), targetCooldownMs (30000), ...
}
```

`'auto'` (the default) uses the first **started** resource of `order`; if none is started it uses `standalone` (our own
get-up where the player lies, `standaloneHealth` 150).

| `system` | What the rite calls |
|---|---|
| `esx_ambulancejob` | `TriggerClientEvent('esx_ambulancejob:revive', target)` |
| `esx_death` | `exports.esx_death:Revive(target, 'rklpriest')` (and `exports.esx_death:IsDead(src)` as the server's truth) |
| `qb-ambulancejob` | `TriggerClientEvent('hospital:client:Revive', target)` |
| `qbx_medical` | `TriggerClientEvent('qbx_medical:client:playerRevived', target)` - check your version |
| `wasabi_ambulance` | `TriggerClientEvent('wasabi_ambulance:revive', target)` - check your version |
| `ars_ambulancejob` | `TriggerClientEvent('ars_ambulancejob:healPlayer', target, { revive = true })` - check your version |
| `standalone` | our own get-up on the fallen player's client |
| `custom` | your event from `Config.Revive.custom` |

**Wiring a different ambulance script**, three ways (the files stay editable under Cfx escrow):

1. **No Lua**: `Config.Revive.system = 'custom'` and set `custom.event` (a client event to the fallen player, or
   `target = 'server'` for a server event that gets the target first).
2. **One line** in `server/server_open.lua`: replace the body of `PriestServerOpen.RevivePlayer(target, priestSrc)`,
   for example:

   ```lua
   function PriestServerOpen.RevivePlayer(target, priestSrc)
       return exports.my_ambulance:Revive(target) == true
   end
   ```

   or add a row to its `Revivers` table and name it in `Config.Revive.system`.
3. **A different "is he down?"**: the server's truth is `PriestServerOpen.IsPlayerDead(src)` (`server/server_open.lua`);
   the prompt on the priest's screen uses `PriestSpellsOpen.IsDeadBody(ped, serverId)` (`client/client_open.lua`). Often
   it is enough to add your script's state bag key to `Config.Revive.deadBags` (default `isDead`, `dead`, `isdead`,
   `inLastStand`).

| Open function | File | What it does |
|---|---|---|
| `PriestSpellsOpen.IsDeadBody(ped, serverId)` | `client/client_open.lua` | decides whether the `[E]` prompt shows over a body (state bags, a dead ped, a downed pose) |
| `PriestSpellsOpen.FindReviveTarget()` | `client/client_open.lua` | the nearest fallen player within `promptDistance` (2.2 m), never in a vehicle |
| `PriestSpellsOpen.OnReviveDone(serverId)` | `client/client_open.lua` | empty hook on the priest's client after a revive |
| `PriestSpellsOpen.StandaloneRevive(health)` | `client/client_open.lua` | the `standalone` get-up on the fallen player's client |
| `PriestServerOpen.IsPlayerDead(src)` | `server/server_open.lua` | the server's truth: esx_death, QBCore / Qbox metadata `isdead` / `inlaststand`, a dead state bag, server health 0 |
| `PriestServerOpen.RevivePlayer(target, priestSrc)` | `server/server_open.lua` | calls the system of `Config.Revive.system` -> `true` or `false, reason` |
| `PriestServerOpen.ReviveSystem()` | `server/server_open.lua` | which system `'auto'` picked |

What the server checks before and after the channel: the priest holds the class and is alive, the cooldowns (hers 60 s;
the same body 30 s for any priest), the same routing bucket, the distance on server positions, that the target is
really down, that nobody else is raising that body, no mock battle, and the Faith cost. `RevivePlayer` runs exactly once
per rite; a stopped or missing ambulance script only fails the rite (the Faith goes back), never the class.

**Heals.** The God and the Priest are the healing classes. Priest heals are capped on the server: one heal at most 35,
per healed player at most 70 HP per 10 s and 60 HP of shields per 12 s across all priests together (`Config.Heal.window`,
`Config.Shield.window`). Healing others gives class XP (2 XP per 30 HP, at most 40 a minute).

## Events

```lua
-- server-local: a class was given, changed or removed (by /setclass, the hall, the species screen ...)
AddEventHandler('rklclass:server:classChanged', function(identifier, class, grade, name, via, by, previous)
    -- class = false when the class was removed
end)

-- server-local: a member levelled up
AddEventHandler('rklclass:server:levelUp', function(src, class, level) end)
```

## The species screen (rklselectspecies)

```lua
-- SERVER
exports.rklselectspecies:OpenFor(src)                     -- open the screen -> true | false (not online)
local job, grade = exports.rklselectspecies:GetSpecies(src)   -- the class held now (nil = none)
exports.rklselectspecies:IsSpeciesOpen('kitsune')         -- may it be picked now?
exports.rklselectspecies:ResetCooldown(src_or_identifier, function(ok, err) end)
TriggerClientEvent('rklselectspecies:open', src)
AddEventHandler('rklselectspecies:server:changed', function(src, newJob, oldJob) end)

-- CLIENT
exports.rklselectspecies:Open()
exports.rklselectspecies:Close()
exports.rklselectspecies:IsOpen()
TriggerEvent('rklselectspecies:open')
AddEventHandler('rklselectspecies:client:changed', function(newJob, oldJob) end)
AddEventHandler('rklselectspecies:client:closed', function() end)
```

Example: show the screen to a new character on their first join (ESX):

```lua
AddEventHandler('esx:playerLoaded', function(src)
    if not exports.rklselectspecies:GetSpecies(src) then
        exports.rklselectspecies:OpenFor(src)
    end
end)
```

## rklui (the class network)

With rklui running (`Config.Rklmana.resource = 'rklui'`, the default), every class shares one server-checked mana pool, statuses (a
stun from any class blocks casting in every class), shields, elements and reactions, marks, cross-class buffs and one
move-speed arbiter, and players can fight non-lethal mock battles. Each part has its own switch in `Config.Rklmana`;
`Enabled = false` keeps a class fully standalone. Nothing breaks when rklui is stopped. rklui's own exports
(`exports.rklui`, mana, buffs, mock battle) are listed in the README inside the rklui folder.
