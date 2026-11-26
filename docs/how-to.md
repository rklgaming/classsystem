# How-to (for server owners and admins)

[Back to the overview](../README.md)

Every common job, step by step. Commands are typed in the game chat (press <kbd>T</kbd>) with a `/`, or in the
server console (txAdmin **Live Console**) **without** the `/`. Settings are in each class's `config.lua`; after you
change a `config.lua`, restart that resource (console: `ensure rklarcher`, or restart the server).

**Only admins** can do the jobs on this page (who counts as admin: [Getting started, step 5](getting-started.md#step-5---give-yourself-admin-rights)).
The server checks it every time; players cannot change spells, classes or levels, even with a modified game.

Class names for commands: `god`, `demon`, `merfolk`, `vampire`, `werewolf`, `fairy`, `witch`, `elf`, `archer`,
`kitsune`, `priest`, `assassin`, `knight`, `oni`, `samurai`, `shaman`, `alchemist`, `dragonkin`, `necromancer`, `chronomancer`. A player's **server ID** is the number txAdmin shows next to their name.

## Players and classes

### Give a player a class

1. Type `/setclass <id> <class>`, for example `/setclass 12 archer`.
2. The player gets the class at rank 1 and their spell bar appears.

> **Tip:** add a rank at the end to start higher: `/setclass 12 archer 4` (ranks are 0-9; 9 is the leader).

### Give a class to a player who is offline

1. Find their identifier (txAdmin **Players** → the player → copy `license:...`, or on ESX / QBCore their character
   id).
2. Type `/setclass <identifier> <class> [rank]`, for example `/setclass license:1a2b3c archer 0`.

### Change a player's rank

1. Type `/setclass <id> <their class> <rank>`, for example `/setclass 12 archer 6`.
2. Or let the class leader do it in the hall: `/manageclass` → **Members** → **Promote** / **Demote** / **Set rank**.

### Make someone the class leader

1. Type `/setclass <id> <class> 9` (rank 10 = the leader).
2. From then on that player opens `/manageclass` and can hire, promote and remove members.

### Remove a player's class

1. Type `/setclass <id> none`.
2. Their level in that class is kept, in case they come back to it later.

### See who has which class

1. Open the hall as admin: `/manageclass <class>` → **Members** (online and offline, with search and pages).
2. With rklui: `/classes` lists every class and how many players are online in each.

### Let players choose their own class

1. Players type `/selectspecies`, read the classes and press **Embrace this path**.
2. That is all: the screen applies the class for them.

> **Tip:** by default a player can switch class any time. See the next tasks to add a cooldown or make the first
> choice final.

### Make the first choice final, or add a cooldown

1. Open `rklselectspecies/config.lua`.
2. First choice final: set `Config.Rules.allowChange = false`.
3. Or a waiting time between changes: set `Config.Rules.cooldownHours = 24` (any number of hours).
4. Restart `rklselectspecies`.

### Clear a player's species cooldown

1. Type `/resetspecies <id>` (or their identifier for an offline player).

### Keep some classes for admins or VIPs only

1. Open `rklselectspecies/config.lua`.
2. Set `Config.Rules.adminOnly = { 'god' }` (add more names inside the braces).
3. Restart `rklselectspecies`. Other players cannot pick it there; you can still give it to anyone with `/setclass`.

> **Tip:** to make the whole screen VIP-only, set `Config.Command.restricted = true` and add
> `add_ace group.vip command.selectspecies allow` to `server.cfg`.

### Show the species screen to new players automatically

1. Make a small new resource (or use one of your own) and put this in a server file (ESX example):

   ```lua
   AddEventHandler('esx:playerLoaded', function(src)
       if not exports.rklselectspecies:GetSpecies(src) then
           exports.rklselectspecies:OpenFor(src)
       end
   end)
   ```
2. On QBCore use your own "player loaded" event the same way.

### Open the species screen from an NPC, a menu or a key

1. From any client script: `TriggerEvent('rklselectspecies:open')`.
2. From any server script: `exports.rklselectspecies:OpenFor(source)`.

### Let players leave their class

1. Open `rklselectspecies/config.lua` and set `Config.Rules.allowNone = true`.
2. The screen then shows **Leave Species**.

### Use only some of the classes

1. Move the class folders you do not want out of `resources/[class]` (keep a copy).
2. Restart the server. The species screen hides classes whose resource is not running.

## Spells

### Change a spell's damage, cost, cooldown or range

1. Type `/manageclass <class>` and open the **Editor** tab (admins only).
2. Pick the spell. The main values are at the top; **Show all values** shows every number.
3. Change the value and press **Save**. It applies at once for every player - no restart.

> **Tip:** each field shows the original value with a reset button. A warning chip appears if a value goes past the
> fair-play limits (the limits are still enforced in game).

### Put a spell back to its original values

1. `/manageclass <class>` → **Editor** → the spell.
2. Press the reset button next to a field, or reset the whole spell, then **Save**.

### Move a spell to another slot on the bar

1. `/manageclass <class>` → **Editor**.
2. Move the spell up or down to the slot you want (slot 10 = key <kbd>0</kbd>), then **Save**.

### Turn a spell off

1. `/manageclass <class>` → **Editor** → the spell → switch it **off** → **Save**.
2. The spell leaves the bar and the server refuses it.

### Change which rank unlocks a spell

1. `/manageclass <class>` → **Editor** → the spell → change its unlock rank → **Save**.
2. Or in `config.lua`: `Config.SpellLadder.spells = { thousand_arrows = 5 }` (spell key = rank number).

### Give every rank every spell

1. In the class's `config.lua` set `Config.SpellLadder.Enabled = false`.
2. Spells then use their own `minGrade` (0 = everyone). Restart the class.

### Change the default spell keys

1. In `config.lua`: `Config.Keys = { '1', '2', '3', '4', '5', '6', '7', '8', '9', '0' }` - change the keys you want.
2. Restart the class. Players who already set their own keys keep theirs.
3. The quick ability has its own key in its `Config.Spells` block: `slot = 0, key = 'G'`. A new default letter
   reaches every player, even those who had bound the old one.

> **Tip:** players can always change keys themselves: **Settings → Key Bindings → FiveM** → search the class name.

### Change a spell's colours, particles or sounds

1. Open the class's `config.lua` and find `Config.Spells` → the spell's block (each block has a comment that explains
   it).
2. Change the colour, particle or sound values, save, and restart the class.

### Turn the sounds down or off

1. In the class's `config.lua`: `Config.Sound.volume = 0.5` (0 to 1), or `Config.Sound.Enabled = false` for no sounds.
2. Restart the class.

> **Tip:** if you use an InteractSound-style resource, set `Config.Sound.engine = 'interactsound'`.

### Test spells alone (no second player)

1. In `config.lua` set `Config.HurtCasterForTesting = true` and restart the class.
2. Aim spells at your own feet: they hit you too.
3. **Set it back to `false` before players join.**

## Levels and XP

### Give a player XP, a level or skill points

1. XP: `/classxp <id> <amount>` (they level up when they reach the next level).
2. Level: `/classlevel <id> <level>` (skill points follow the level).
3. Skill points: `/classpoints <id> <number>` (a negative number takes points away).

### Reset a player's skill points

1. Type `/classpoints <id> reset`. Every spent point comes back to them.

### Change the highest level

1. In each class's `config.lua`: `Config.Levels.maxLevel = 60` (default 50).
2. Restart the classes.

### Make levelling faster or slower

1. In `config.lua`, `Config.Levels.curve = { base = 100, exp = 1.5 }` decides how much XP each level needs.
2. A smaller `base` (for example 60) = faster levels; a bigger one = slower.
3. Or give more XP per action instead (next task).

### Change how much XP each action gives

1. In `config.lua`, `Config.Levels.xp`:
   - `spellHit = { xp = 2, perMinuteCap = 60 }` - a spell that hits another player
   - `monsterKill = { xp = 25 }`, `bossKill = { xp = 200 }` - with rklspawnmonster
   - `mockRound = { xp = 10 }`, `mockWin = { xp = 50 }` - the PvP mock battle (only when it is switched on in rklui;
     off by default). The `/mockfight` spell showcase gives no XP.
2. Set `xp = 0` to turn a source off. Restart the class.

### Unlock spells by level instead of by rank

1. In `config.lua` set `Config.Levels.unlockByLevel = true`.
2. `Config.Levels.levelLadder = { 1, 1, 3, 6, 10, 15, 20, 26, 33, 40 }` sets the level for bar slots 1-10.

### Change how often players may reset their skill points

1. In `config.lua`: `Config.Levels.reset = { mode = 'cooldown', hours = 24 }`.
2. `mode = 'free'` (any time), `'cooldown'` (once every `hours`) or `'admin'` (only admins).

### Turn the level system off

1. In each class's `config.lua` set `Config.Levels.Enabled = false` and restart.
2. No levels, XP, spell ranks or Skills tab; spells unlock by rank only.

### Give class XP from your own script (fishing, jobs, quests ...)

1. In a **server** script, call the export of the player's class, for example:

   ```lua
   local RES = { god = 'rklgods', fairy = 'rklfairyspells', witch = 'rklwitchspells' }   -- the rest: 'rkl' .. name
   local cls = Player(source).state['rkl:class']          -- { name = 'archer', grade = 3 } or nil
   if cls then
       exports[RES[cls.name] or ('rkl' .. cls.name)]:AddXP(source, 40, 'fishing')
   end
   ```
2. The number is the XP, the text is a reason (it shows in the logs). Nothing happens if the player has no class.

### Wipe all levels for a new season

1. **Back up your database first.**
2. Stop the server, then run this SQL (HeidiSQL, phpMyAdmin or txAdmin's database tool): `TRUNCATE TABLE rkl_classlevels;`
3. Start the server. Everyone starts again at level 1; their classes and ranks stay.

## The class hall

### Open the hall

1. Type `/manageclass`. It opens the hall of the class you hold.
2. Admins can open any class's hall: `/manageclass archer`.

### Choose which rank is the leader

1. By default the leader is the class's highest rank (rank 10).
2. To name it yourself: `Config.Boss.grades = { 8 }` in `config.lua` (rank 9 and up lead). Restart the class.

### Let more ranks recruit new members

1. In `config.lua`: `Config.Boss.canHire = { 7 }` (grade 7 = rank 8; that rank and every higher one may invite).
   Restart the class.

### Invite a player (as the leader)

1. `/manageclass` → **Recruit**: pick a player near you, or type their server ID.
2. They get a card for 30 seconds and press <kbd>Y</kbd> to join or <kbd>N</kbd> to decline.

### Promote, demote or remove a member

1. `/manageclass` → **Members** (online and offline).
2. Use **Promote**, **Demote**, **Set rank** or **Remove** (a confirm box asks first).

### Turn the initiation ritual on or off

1. `/manageclass` → **Settings** → the **initiation ritual** switch (the leader or an admin).

### Send the hall's log to Discord

1. Open the class's `server/server_open.lua` and put your Discord webhook link in `BOSS_WEBHOOK`.
2. Restart the class. Never put a webhook in `config.lua` (players receive that file).

### Give staff full hall access without the class

1. Add to `server.cfg`: `add_ace group.admin rklarcher.boss allow` (one line per class: `<resource>.boss`).

## Mana, HUD and the spell showcase (rklui)

### Use one shared mana pool for every class

1. Start `rklui` (it is in the package). Every class uses it automatically
   (`Config.Rklmana.resource = 'rklui'`).

### Run the classes without rklui

1. Do not start `rklui`. Each class then uses its own mana: armour by default (`Config.Mana.fallback`).
2. Other options for `Config.Mana.type`: `'health'`, `'stamina'`, `'custom'` (its own pool).

### Rename a class's mana

1. In the class's `config.lua`: `Config.Mana.label = 'Focus'` (the name players see). Restart the class.

### Change the HUD look

1. Players type `/hudsettings`: essence, metal frame, size, position, numbers and effects.

### Hide the whole UI (for videos and screenshots)

1. Type `/hidehud`. Type it again to show everything.

### Show the spells of two classes (mock fight)

1. Stand on open, flat ground, on foot, facing open space.
2. Type `/mockfight demon elf` (any two classes; `/mockfight list` shows the names). Two NPC fighters appear in front of
   you and cast every spell of their class at each other, with HP bars, the spell names and a winner.
3. `/mockfight stop` ends it at once (admins: the one nearest to them). Everyone within 60 m sees the same fight;
   nobody is hurt and nobody gets XP.

### Choose who may start a mock fight

1. In `rklui/config_mana.lua`, `Config.MockFight.Who`: `'everyone'` (default), `'class'` (only players who hold a
   class), `'ace'` or `'admin'`. Admins may always.
2. For `'ace'`, add to `server.cfg`: `add_ace group.vip rklui.mockfight allow`.
3. The limits are next to it: `CooldownMs` (45 s per player), `MaxActive` (3 fights at once), `MinDistance` (70 m
   between two fights), `ViewRange` (60 m). Restart `rklui`.

### Change how a class's fighter looks in a mock fight

1. Open the class's `config_preview.lua` and change the `fighter` row: the ped `model`, its `scale`, and for freemode
   peds the clothes (`components`, `props`).
2. Or set it in rklui for one class: `Config.MockFight.Fighters.elf = { model = 'mp_f_freemode_01' }` in
   `rklui/config_mana.lua` (wins over the class's file).
3. Restart the class (or `rklui`).

### Turn the mock fight off, or bring back the PvP mock battle

1. `/mockfight` off: `Config.MockFight.Enabled = false` in `rklui/config_mana.lua`. One class only:
   `Config.Preview.Enabled = false` in its `config_preview.lua`.
2. The older player-vs-player mock battle (`/mockbattle` duels and rings of up to 8, `/mockstats`) is still in rklui,
   switched off. To use it, set `Config.MockBattle.Enabled = true` in `rklui/config_mana.lua`.
3. Restart `rklui`.

### Turn off rklui's potions and crafting

1. In `rklui/config.lua`: `Config.Modules = { Hud = true, Mana = true, Stat = false }`. Restart `rklui`.

## Look and language

### Change a class's colour

1. In the class's `config.lua`: `Config.Class.accent = '#7fbf5a'` (any hex colour). The bar and its panels follow it.
2. Restart the class. Players can still pick their own bar theme in `/<class>bar`.

### Rename the ranks

1. In the class's `config.lua`, `Config.Ranks` has the ten rank names (English `en` and Tagalog `tl`). Change the
   text and restart the class.

### Switch the language

1. In each class's `language.lua` set `Locale = 'tl'` (or your own language).
2. `rklselectspecies/config.lua`: `Config.Locale`; rklui: `Config.Locale`.

### Translate into your own language

1. In `language.lua`, below `Lang.en`, add a table like `Lang.es = { cast_cancelled = 'Hechizo cancelado', ... }`.
2. Set `Locale = 'es'`. Anything you did not translate falls back to English.

### Change a message players see

1. Open the class's `language.lua`, find the text, change it, save and restart the class.

## The Priest (heals and revives)

### Connect the Priest's revive to your ambulance script

1. Open `rklpriest/config.lua` → `Config.Revive`.
2. Leave `system = 'auto'` if you use esx_ambulancejob, esx_death, qb-ambulancejob, qbx_medical, wasabi_ambulance or
   ars_ambulancejob: it finds it by itself.
3. Another script? Set `system = 'custom'` and its revive event:

   ```lua
   custom = { event = 'my_ambulance:client:revive', target = 'client', args = {} },
   ```
4. Restart `rklpriest`. Full details: [Integration](integration.md#the-priests-rite-of-resurrection-revive--ambulance-systems).

### Turn the revive off

1. In `rklpriest/config.lua`: `Config.Revive.Enabled = false`. Restart `rklpriest`.

### Change the revive time, cost or cooldown

1. In `Config.Revive`: `channelMs = 5000` (time in ms), `faithCost = 30`, `cooldownMs = 60000`,
   `targetCooldownMs = 30000`. Restart `rklpriest`.

### Change how much a priest can heal

1. In `rklpriest/config.lua`: `Config.Heal.maxPerCast = 35` and `Config.Heal.window = { ms = 10000, maxHp = 70 }`.
2. Shields: `Config.Shield.window`. Restart `rklpriest`.

## Server and frameworks

### Use the classes without ESX or QBCore (standalone)

1. In each class's `config.lua`: `Config.Framework = 'standalone'`.
2. Give access with `/setclass` as usual (the player's license is their identifier).

### Move from framework jobs to the class table

1. Old setups used a framework job per class. Now the default is `Config.ClassSource = 'sql'` (our own table).
2. On the first start the members of the old jobs are copied into the table once (`Config.ClassStore.import`).
3. To keep the old way: `Config.ClassSource = 'job'`.

### Keep spells inside instances (apartments, private worlds)

1. `Config.RoutingBuckets = true` (default): spells only reach players in the same routing bucket.

### See why a spell does not cast

1. In the class's `config.lua` set `Config.Debug = true` and restart the class.
2. Every cast and every refusal (no mana, cooldown, out of range, locked) prints in the server console.
3. Set it back to `false` when you are done.

### Update to a new version safely

1. Back up the old folders, especially `config.lua`, `language.lua`, `data/spell_overrides.json` (your Editor
   changes) and `boss_log.json`.
2. Replace the resource folders with the new ones.
3. Copy your `data/spell_overrides.json` back, and re-apply your `config.lua` / `language.lua` changes (compare the
   old and new files: new versions can add settings).
4. Restart the server.

### Back up player data

1. Everything players earn is in three database tables: `rkl_classsystem` (classes and ranks), `rkl_classlevels`
   (levels, XP, points, spell ranks) and `rkl_selectspecies` (species changes).
2. Export them with HeidiSQL or phpMyAdmin like any other table.
