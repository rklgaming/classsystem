# Configuration

[Back to the overview](../README.md)

Every class has its own `config.lua`. All twenty are built on the same class core, so the sections below are the same in
each one; only the class block, the passive and the spells differ. A feature you may not want is a switch
(`Enabled = true / false`), never hard-wired. Texts live in `language.lua`, never in `config.lua`.

`config.lua` is loaded on both sides and sent to every player: **never put a webhook URL or a secret in it** (the hall's
Discord webhook goes in `server/server_open.lua`).

## The main sections

| Section | What you set there |
|---|---|
| `Config.Framework` | `'auto'` (Qbox > QBCore > ESX), `'esx'`, `'qb'`, `'qbox'` or `'standalone'` |
| `Config.ClassSource` | `'sql'` (default: our table `rkl_classsystem`) or `'job'` (a framework job per class, `Config.ClassJob`) |
| `Config.ClassStore` | the table name, `/setclass` and `/manageclass` command names, the admin ACE (`rklclass.admin`), admin groups, the one-time job import |
| `Config.Class` | the class id, label, element, mana essence, accent colour and particle tint |
| `Config.CooldownKey` | how cooldowns are kept per player: `'auto'`, `'character'`, `'license'` or `'session'` |
| `Config.EnforceServerCooldowns` | `true` (recommended): the server is the last check for every cooldown |
| `Config.Casting` | right-mouse aiming, face the target, anti-spam, range slack, break the cast on a hit, no melee lock-on |
| `Config.Mana` | the mana pool: `'auto'` (rklui's shared pool when it runs, otherwise `fallback` = `'armour'`), `'armour'`, `'health'`, `'stamina'`, `'custom'`, `'pool'`; the label (Grace, Vitae, Rage ...) |
| `Config.Rklmana` | the class network with rklui: shared statuses, shields, damage, marks, buffs, one move-speed arbiter; `Enabled = false` = fully standalone |
| `Config.Sound` | `'own'` (the class's own sound files, volume by distance) or `'interactsound'`; `Enabled = false` mutes every spell |
| `Config.SyncDistance`, `Config.RoutingBuckets` | how far others see your spells; spells stay inside a routing bucket |
| `Config.Keys` | the ten slot keys (`1`-`0`) |
| `Config.Targeting`, `Config.Protection`, `Config.Damage` | who spells may hit (players, NPCs, vehicles), spawn protection, damage rules |
| `Config.DashGround` | (class core 3.2.9) every dash, leap, lunge and blink follows the floor on slopes, stairs, bridges and indoors, stops at walls and never ends under the floor; `Enabled = false` = the old straight-line dashes |
| `Config.Status` | crowd control kinds (root, slow, stun, blind, fear, lift, silence ...) with immunity and cleanse rules |
| `Config.Healing` | the healing classes are the **God** and the **Priest**; every other class keeps only HP gained by attacking |
| `Config.Buffs` | power, ward, protect, haste, focus, slow, weaken: used when rklui is not running |
| `Config.UI` | the bar: saved layout, edit command (`/<class>bar`), hide / show key and button, theme accent, slot shape and size; `Config.UI.personal` = the players' own switches (below) |
| `Config.Ranks` | the names of the ten ranks (English + Tagalog) and their badge colour / icon |
| `Config.SpellLadder` | which rank unlocks which bar slot (default: slots 1-2 at rank 1, then one per rank; quick abilities at rank 5) |
| `Config.Boss` | the class hall: who is the leader, who may hire, invitations, rate limits, the initiation ritual, the log |
| `Config.Editor` | the admin spell editor in the hall (see below) |
| `Config.Levels` | levels, XP, skill points and spell ranks (see [Levels and spell ranks](levels.md)) |
| `Config.Passive` | the class passive: every part has its own switch; `Enabled = false` removes it |
| `Config.Heal`, `Config.Shield`, `Config.Support` (Priest) | heal and shield caps: one heal at most 35, per player 70 HP / 10 s and 60 shield / 12 s across all priests; who a heal may target |
| `Config.Revive` (Priest) | the Rite of Resurrection: which revive / ambulance system it calls, the 5 s channel, ranges, cooldowns, the Faith cost (see [Integration](integration.md#the-priests-rite-of-resurrection-revive--ambulance-systems)) |
| `Config.Spells.<key>` | every spell: slot, rank, cost, cooldown, cast time, range, damage, statuses, colours, particles, sounds, timings |

### A spell block

Each spell has a block in `Config.Spells` with a comment that explains it. The values you change most:

```lua
throw_spear = {                       -- inside Config.Spells (rklvampire)
    slot = 1, minGrade = 0, label = 'Throw Spear', icon = 'throw_spear.png',
    type = 'direct', usesE = true, cooldown = 8000, manaCost = 9, element = 'blood',
    range = 55.0,
    -- damage, statuses (bleed ...), PvP caps, particles, sounds and timings follow, each with a comment
    -- Enabled = false takes a spell off the bar, the ladder and the hall; the server refuses it
},
```

Damage numbers are player damage; NPCs take more (`impact.npcDamage`). The PvP caps (at most 50 per hit, crowd control
at most 2.5 s, `maxPerVictim` per cast) apply after every bonus, so balance stays fair whatever you change.

### The spell editor (in game, admins)

`/manageclass <class>` > **Editor** (admins only: the server refuses it for everyone else): every spell in bar order. Move a spell to another slot, change its damage, mana,
cooldown, range / radius, cast time, crowd control, on / off and unlock rank, or open *Show all values*. Each field shows
the shipped value with a reset button. **Save** applies at once for every player and writes only the changed values to
`data/spell_overrides.json` (the previous file is kept as `.prev.json`). A hand edit of that file is picked up within
5 seconds; a broken file keeps the last good one.

### The class hall

- The **leader** is the highest grade, a grade named `boss`, or the grades in `Config.Boss.grades`.
- Recruiters: `Config.Boss.canHire`. An invitation shows a card for 30 s (`inviteMs`); accepted = hired at
  `hireGrade`.
- Every decree is checked on the server: never on yourself, never on someone of your rank or higher.
- Members are managed online and offline. The last 100 decrees are kept in `boss_log.json`; a Discord webhook is
  optional (`BOSS_WEBHOOK` in `server/server_open.lua`, `Config.Boss.log.webhook = false` keeps it local).
- The **initiation ritual** (the recruit kneels in the class's magic circle) can be switched on / off in the hall's
  Settings tab.
- `Config.Boss.Enabled = false` removes the hall (the rank ladder still works).

### The showcase look (`config_preview.lua`)

Every class also has an open `config_preview.lua` (class core 3.2.7): how the class looks and fights in a `/mockfight`
spell showcase. It never changes the real spells, and nothing in it runs without rklui.

| Key | What it does |
|---|---|
| `Config.Preview.Enabled` | `false` = this class plays no spells in a showcase (only their names show) |
| `fighter` | the fighter: ped `model`, `fallback` model and `scale`; freemode peds also take `components`, `props`, `headBlend`, hair and eye colour |
| `dash` | the class dash, shown once more on top of the spells |
| `spells.<key>` | one row per spell: `skip` (never shown), `kind` (`attack` / `support` / `dash` / `ult`), `dmg` / `heal` (how far the showcase HP bar moves), `hitMs`, `showMs`, `castTimeScale`, `move` |
| `MaxCasts`, `MaxFights`, `MaxShowcaseMs`, `Shake` | how many showcase casts and fights of this class one player draws at once, the time limit, camera shake on / off |

### Worn and held gear

Several classes wear or hold their own models: the Knight's sword and tower shield, the Oni's club, horned mask and
gourd, the Samurai's katana and saya, the Shaman's mask and drum, the Alchemist's brass still and flasks, the Dragonkin's
horns, scale mantle and wings, the Necromancer's bone staff and skull lantern, the Archer's bow and the Assassin's
daggers. Every player in range sees them.

Each piece is one row: `Enabled`, `model`, `bone`, the offset and `rot`.

```lua
swordWorn = { Enabled = true, model = 'kn_sword_hip', bone = 11816, offset = vector3(0.05, -0.03, -0.19), rot = vector3(0.0, 0.0, 0.0), rotOrder = 2 },
```

- **Server switch**: `Enabled = false` on a row hides that piece for everyone; the block's own `Enabled = false`
  switches the class's worn gear off for the whole server.
- **Players' switch**: each player turns their own worn gear on or off in the bar editor (`/<class>bar`); see
  *Personal switches* below.
- `bone` is a ped bone id (`11816` pelvis, `24818` upper back, `31086` head, `57005` right hand, `61163` left forearm).
  The offset is in metres in that bone's own frame (bone frames are not Z-up). `rot` is in degrees, applied the way
  `AttachEntityToEntity` does with rotation order 2: R = Rz(z) · Rx(x) · Ry(y), plain signs (measured in game). Most
  worn models are built into their bone's frame, so their `rot` stays `0, 0, 0`.

| Class | Gear rows | Offset key | Players' switches (`/<class>bar`) |
|---|---|---|---|
| Knight | `Config.Gear` | `offset` | worn sword and shield |
| Oni | `Config.Kit.gear` | `pos` | horned mask (also `/onimask`), club on the back, gourd on the hip |
| Samurai | `Config.Kit.gear` | `pos` | katana and saya (also `/katana`) |
| Shaman | `Config.Gear` | `offset` | worn mask and drum |
| Alchemist | `Config.Gear` | `offset` | worn still and vial belt |
| Dragonkin | `Config.Kit.gear`, `Config.Kit.wings`, `Config.Kit.scales` | `pos` | folded wings, dragon horns, scale mantle |
| Necromancer | `Config.Kit.gear` | `pos` | worn staff and lantern (or each on its own), lich mantle, the servants' bone dress |
| Chronomancer | the spell rows (e.g. `hourglass` in `Config.Spells.hour_zero`) | `offset` | worn props (hourglasses, rings) |
| Archer | `Config.Gear` | `offset` | bow on the back |
| Assassin | `Config.Gear` | `offset` | daggers in hand |

A few pieces belong to one spell and sit in that spell's block (the Chronomancer's hourglasses, the Necromancer's lich
mantle); they use the same row format.

### Personal switches (`Config.UI.personal`)

Since class core 3.2.11 every class can give its players on / off switches of their own. They show in the bar editor
(`/<class>bar`) and each player's choice is saved on their PC.

```lua
Config.UI.personal = {
    { key = 'gear',  Enabled = true, default = true, label = 'ui_pref_gear',  note = 'ui_pref_gear_note' },
    { key = 'shake', Enabled = true, default = true, label = 'ui_pref_shake', note = 'ui_pref_shake_note' },
}
```

- `Enabled = false` hides a row; it then always uses its `default`.
- `label` and `note` are keys in `language.lua`.
- Your own scripts read a switch with `exports['<resource>']:GetPref(key)` ([Integration](integration.md)).

### The Witch's wand (`Config.RequireWeapon`, rklwitchspells)

| Key | Default | What it does |
|---|---|---|
| `Enabled` | `false` | `true` = the witch must hold one of `weapons` to start a spell; a running spell can always be recast or ended |
| `weapons` | `{ 'weapon_wand', 'weapon_wand2' }` | weapon names as your weapons / inventory know them (case does not matter), or weapon hashes |
| `label` | `'wand'` | what the *"Hold your ... to cast"* message calls it |
| `quick` | `true` | the quick ability needs it too; `false` = only the bar slots |
| `serverCheck` | `true` | the server checks the held weapon too (OneSync); `false` = the player's game only |
| `lockonOff` | `true` | while she holds one, right mouse stays the spell button (GTA's own aim and lock-on stay off) |

## The spell showcase (`rklui/config_mana.lua`)

`/mockfight <class> <class>` is set up in `Config.MockFight`. Restart `rklui` after a change.

| Key | Default | What it does |
|---|---|---|
| `Config.MockFight.Enabled` | `true` | `false` = `/mockfight` is off |
| `Config.MockFight.Command` | `'mockfight'` | the command name |
| `Config.MockFight.Who` | `'everyone'` | who may start one: `'everyone'`, `'class'` (players who hold a class), `'ace'` (`AcePermission`, default `rklui.mockfight`) or `'admin'`; admins always may |
| `Config.MockFight.CooldownMs` | `45000` | per player, from the end of their last fight |
| `Config.MockFight.MaxActive` | `3` | fights on the whole server at once |
| `Config.MockFight.MinDistance` | `70.0` | a new fight must be this far (m) from every running one |
| `Config.MockFight.ViewRange` | `60.0` | players this close see the fight; players who walk in later get it too |
| `Config.MockFight.LeaveRange` | `90.0` | the player who started it goes this far away (or leaves) = the fight ends |
| `Config.MockFight.MaxDurationMs` | `180000` | the longest one fight may take (the casts are squeezed to fit) |
| `Config.MockFight.Fighters` | `{}` | a fighter look per class, e.g. `elf = { model = 'mp_f_freemode_01' }`; wins over the class's `config_preview.lua` |
| `Config.MockFight.Aliases` | | more names players may type, e.g. `wolf = 'werewolf'`, `fox = 'kitsune'` |
| `Config.MockBattle.Enabled` | `false` | the older PvP mock battle (`/mockbattle` duels and rings, `/mockstats`); `true` brings it back |

The texts (`mf_...`) are in `rklui/locales/en.lua` and `tl.lua`.

## The species screen (`rklselectspecies/config.lua`)

| Key | Default | What it does |
|---|---|---|
| `Config.Locale` | `'en'` | `'en'` or `'tl'` |
| `Config.Command` | `selectspecies` | `Enabled`, `name`, `restricted` (then `add_ace group.vip command.selectspecies allow`) |
| `Config.StartGrade` | `0` | the rank a new species starts at |
| `Config.Rules.allowChange` | `true` | a player with a species may switch |
| `Config.Rules.cooldownHours` | `0` | hours between two changes (the first pick is never delayed) |
| `Config.Rules.keepGrade` | `false` | keep the rank when switching, or start at `StartGrade` |
| `Config.Rules.allowNone` | `false` | show *Leave Species* |
| `Config.Rules.adminOnly` | `{}` | classes only admins may pick, e.g. `{ 'god' }` |
| `Config.Rules.adminBypass` | `true` | admins skip the cooldown, `allowChange` and `adminOnly` |
| `Config.Apply.command` | `'setclass'` | the shared class command the pick runs through |
| `Config.Store` | `'auto'` | `'sql'` (table `rkl_selectspecies`) or `'json'` (`data/changes.json`) |
| `Config.UI` | | scale, blur, sounds, colours, hide classes whose resource is not running |
| `Config.Species` | 10 | the cards: label, epithet, lore, roles, mana, elements, passive, three skills (en + tl) |

A class whose resource is not running is hidden (or shown as *Sealed*) and can never be picked.
