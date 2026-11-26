# Commands and controls

[Back to the overview](../README.md)

## How a player gets a class

1. **Pick a species**: `/selectspecies` opens the selection screen. It shows every class with its lore, roles,
   mana, elements, passive and three signature skills. *Embrace this path* picks it; the server checks the pick
   against your rules (changes allowed, cooldown, admin-only classes) and applies it.
2. **Or an admin gives it**: `/setclass <server id | identifier> <class> [grade]`, and `/setclass <id> none` takes it
   away. Class names: `god`, `demon`, `merfolk`, `vampire`, `werewolf`, `fairy`, `witch`, `elf`, `archer`, `kitsune`, `priest`, `assassin`,
   `knight`, `oni`, `samurai`, `shaman`, `alchemist`, `dragonkin`, `necromancer`, `chronomancer`.
3. **Ranks**: every class has ten ranks (grade 0 = rank 1 ... grade 9 = rank 10, the leader). By default spells 1-2
   are open at rank 1 and each rank opens one more slot; quick abilities open at rank 5. The leader promotes members
   in the class hall.
4. **Levels**: playing the class gives XP. Every level gives a skill point to rank up a spell in the hall's
   **Skills** tab. See [Levels and spell ranks](levels.md).

A player holds one class at a time. Switching keeps each class's own level, so coming back to a class continues
where you left off.

## Casting

| Input | What it does |
|---|---|
| hold **right mouse** + **`1`-`0`** | select / cast the spell in that slot (`0` = slot 10) |
| **`E`** | cast a targeted spell at the ground marker |
| **Backspace** or **right mouse** again | cancel the aim; Backspace also cancels a cast bar |
| the same slot again | end, land or detonate a spell that keeps running (it glows on the bar) |
| **`G`** | the quick ability (every class but the God, Demon, Merfolk and Werewolf); `B` before class core 3.2.9 |

- **Direct** spells go off at once. **Targeted** spells show a ground marker (red = out of range) and sometimes a
  preview of the area; nothing locks on: the spell lands where you aimed and the server decides who stood there.
- Getting knocked down, stunned or hit hard during a cast bar breaks the cast (no cost, no cooldown).
- Every key is rebindable: **Settings > Key Bindings > FiveM**, search the class name. The quick ability is listed
  as *Class: spell*, for example *Vampire: Shadow Dash*.

### Class-specific keys

| Class | Spell | Keys |
|---|---|---|
| God | Aegis of the Pantheon | `E` hurls a shield as a boomerang |
| God | Crown of Blades | `E` plants a blade, the slot again consecrates every planted blade |
| Demon | Ascension of the Demon Lord | `E` Hellmaw (fire breath), `G` Abyssal Stomp, `0` ends the form |
| Demon | Hellwhip | `E` lashes, the slot again drops the whip |
| Merfolk | Trident of the Deep | `E` hurls, the slot again recalls it, `X` lets it dissolve |
| Vampire | Throw Spear / Sword Dance | `E` throws; Sword Dance: `G` throws every sword left (while the swords wait, `G` does not Shadow Dash) |
| Werewolf | Call of the Pack | hold right mouse + `E` sends a wolf to the ring under your aim; right mouse + `5` again sends every wolf left |
| Fairy | Wildwood Barrage | `E` hurls a sapling |
| Witch | Smoke Form | `W A S D` drift, `Left Ctrl` rise, `Space` sink, `Shift` surge, `9` reforms |
| Archer | Piercing Shot | hold to draw; let go, left mouse or 1.2 s looses |
| Priest | Mending Light, Aegis, Renewal, Purify, Blessing | aim at an ally and press the slot; aim at nothing (or the sky) to cast on yourself |
| Priest | Rite of Resurrection | walk up to a fallen player and press `E` (5 s); `E`, `Backspace` or `W A S D` cancel |
| Knight | Iron Bulwark | the slot again, or moving, stands you up |
| Samurai | Iaijutsu Draw | keep the blade sheathed for 2 s first: the draw reaches farther and cuts deeper |
| Alchemist | Load Reagent / Flask Toss / Transmute Floor | slot 1 picks acid, frost or ember; slots 2 and 3 use the loaded one |
| Alchemist | Quicksilver Draught | aim at an ally; aim at nothing to drink it yourself |
| Dragonkin | Dragonfire Breath | turn the camera to sweep the fire; the slot again ends it |
| Dragonkin | Wingbeat | `G` again in the air flaps a second time |
| Necromancer | Wall of Bone | the slot again collapses the wall (it hits foes close to it) |
| Chronomancer | Hourglass Ward | aim at an ally; aim at nobody to ward yourself |

## Player commands

| Command | Resource | What it does |
|---|---|---|
| `/selectspecies` | rklselectspecies | open the species selection screen |
| `/manageclass` | every class | open the hall of your class: your rank, your spells, the next unlock, the **Skills** tab (the leader also manages members) |
| `/<class>bar` | each class | unlock the spell bar: drag the slots, pick a theme, shape and colour per slot; ESC or *Seal & Close* saves |
| `/<class>bar hide` / `show` / `toggle` | each class | hide or show the bar (spells still cast while it is hidden) |
| `/onimask` | rkloni | the Oni's horned mask on or off (saved on your PC) |
| `/katana` | rklsamurai | the Samurai's worn katana and saya on or off (saved on your PC) |

Bar commands: `/godbar`, `/demonbar`, `/merfolkbar`, `/vampirebar`, `/werewolfbar`, `/fairybar`, `/witchbar`,
`/elfbar`, `/archerbar`, `/kitsunebar`, `/priestbar`, `/assassinbar`, `/knightbar`, `/onibar`, `/samuraibar`, `/shamanbar`,
`/alchemistbar`, `/dragonkinbar`, `/necromancerbar`, `/chronomancerbar`. The bar editor also holds the class's
**personal switches** (worn gear, camera shake, the God's aura ...): each player's choice, saved on their PC.

Inside the hall: `1`-`6` switch tabs, `/` searches, `PageUp` / `PageDown` change pages, `ESC` closes. An invitation
card answers with `Y` (accept) or `N` (decline).

## Admin commands

| Command | What it does |
|---|---|
| `/setclass <id \| identifier> <class \| none> [grade]` | give, change or remove a class (console too) |
| `/manageclass <class>` | open the hall of any class (admins see every tab and the spell **Editor**) |
| `/classxp <id> <amount>` | give XP (levels up as needed) |
| `/classlevel <id> <level>` | set the level (skill points follow the level) |
| `/classpoints <id> <n \| reset>` | add or take unspent points; `reset` refunds every spell rank |
| `/resetspecies <id \| identifier>` | clear a character's species change cooldown |
| `/<resource>cdkeys` | console: print every player's cooldown key (e.g. `/rklarchercdkeys`; the vampire's is `/vampcdkeys`) |
| `/tidetest [0-100 \| wet \| dry \| parched \| off]` | Merfolk: test the hydration passive |
| `/bloomtest` | Fairy: test the Bloom gauge |

The level commands are shared by every class: the class the target player is in answers them.

## rklui: HUD, mana and the spell showcase

| Command | What it does |
|---|---|
| `/hudsettings` | the HUD settings: essence, metal, size, position, numbers, parts, effects |
| `/rest` | sit down and regenerate |
| `/mana` | your mana pool |
| `/buffs` | the detail panel of your buffs, debuffs, statuses and marks |
| `/mockfight <class> <class>` | the spell showcase: two NPC fighters show every spell of their class, e.g. `/mockfight demon elf` |
| `/mockfight list` | the class names you can type |
| `/mockfight stop` | end your mock fight at once (admins: the one nearest to them, whoever started it) |
| `/hidehud` | hide or show the whole UI, every class bar included |
| `/setmana <id> <value \| max>` | admin: set a player's mana pool |
| `/classes` | admin: the registered classes and the players online per class |

### The mock fight (spell showcase)

A mock fight is a show, not a fight between players. Two NPC fighters appear about 7 m in front of you and cast every
spell of their class at each other with the real spell effects and sounds: the class dash too, the ultimates
last. HP bars and the name of each spell show on screen, and one fighter wins. It is harmless: nobody takes damage and
it gives no XP, mana or loot. Every player within 60 m sees the same fight, also players who walk up later.

- Class names: `gods`, `demon`, `merfolk`, `vampire`, `werewolf`, `fairy`, `witch`, `elf`, `archer`, `kitsune`,
  `priest`, `assassin`, `knight`, `oni`, `samurai`, `shaman`, `alchemist`, `dragonkin`, `necromancer`, `chronomancer` (also `god`, `mermaid`, `vamp`, `wolf`,
  `fae`, `fox`, `healer`, `rogue`, `tank`, `bulwark`, `dragon`, `drake`, `totem` and the resource names).
- Stand on open, flat ground, on foot, facing open space. The fight ends by itself, with `/mockfight stop`, or when you
  walk away (90 m).
- One fight per player, 45 s between two, at most 3 on the server at once, 70 m apart. Who may start one and every
  limit are in `Config.MockFight` ([Configuration](configuration.md#the-spell-showcase-rkluiconfig_manalua)).

The older PvP **mock battle** (player duels and rings with `/mockbattle`, `/mockstats`) is still inside rklui but
switched off (`Config.MockBattle.Enabled = false`); `/mockbattle` answers that it is off.
