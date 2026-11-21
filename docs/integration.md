# Integration and exports

[Back to the overview](../README.md)

Every class resource has the same exports. Replace `rklarcher` with the class you call (`rklgods`, `rkldemon`,
`rklmerfolk`, `rklvampire`, `rklwerewolf`, `rklfairyspells`, `rklwitchspells`, `rklelf`, `rklarcher`, `rklkitsune`).

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
```

Each class README (inside the resource) lists the rest of its own exports and state bags.

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

## With rklui (optional)

With rklui running (`Config.Rklmana.resource = 'rklui'`), every class shares one server-checked mana pool, statuses (a
stun from any class blocks casting in every class), shields, elements and reactions, marks, cross-class buffs and one
move-speed arbiter, and players can fight non-lethal mock battles. Each part has its own switch in `Config.Rklmana`;
`Enabled = false` keeps a class fully standalone. Nothing breaks when rklui is stopped.
