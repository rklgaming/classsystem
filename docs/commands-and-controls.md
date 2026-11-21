# Commands and controls

[Back to the overview](../README.md)

## How a player gets a class

1. **Pick a species**: `/selectspecies` opens the selection screen. It shows every class with its lore, roles,
   mana, elements, passive and three signature skills. *Embrace this path* picks it; the server checks the pick
   against your rules (changes allowed, cooldown, admin-only classes) and applies it.
2. **Or an admin gives it**: `/setclass <server id | identifier> <class> [grade]`, and `/setclass <id> none` takes it
   away. Class names: `god`, `demon`, `merfolk`, `vampire`, `werewolf`, `fairy`, `witch`, `elf`, `archer`, `kitsune`, `priest`, `assassin`.
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
| **`B`** | the quick ability (Vampire, Fairy, Witch, Elf, Archer, Kitsune, Priest, Assassin) |

- **Direct** spells go off at once. **Targeted** spells show a ground marker (red = out of range) and sometimes a
  preview of the area; nothing locks on: the spell lands where you aimed and the server decides who stood there.
- Getting knocked down, stunned or hit hard during a cast bar breaks the cast (no cost, no cooldown).
- Every key is rebindable: **Settings > Key Bindings > FiveM**, search the class name.

### Class-specific keys

| Class | Spell | Keys |
|---|---|---|
| God | Aegis of the Pantheon | `E` hurls a shield as a boomerang |
| God | Crown of Blades | `E` plants a blade, the slot again consecrates every planted blade |
| Demon | Ascension of the Demon Lord | `E` Hellmaw (fire breath), `G` Abyssal Stomp, `0` ends the form |
| Demon | Hellwhip | `E` lashes, the slot again drops the whip |
| Merfolk | Trident of the Deep | `E` hurls, the slot again recalls it, `X` lets it dissolve |
| Vampire | Throw Spear / Sword Dance | `E` throws; Sword Dance: `G` throws every sword left |
| Werewolf | Call of the Pack | hold right mouse + `E` sends a wolf to the ring under your aim; right mouse + `5` again sends every wolf left |
| Fairy | Wildwood Barrage | `E` hurls a sapling |
| Witch | Smoke Form | `W A S D` drift, `Left Ctrl` rise, `Space` sink, `Shift` surge, `9` reforms |
| Archer | Piercing Shot | hold to draw; let go, left mouse or 1.2 s looses |
| Priest | Mending Light, Aegis, Renewal, Purify, Blessing | aim at an ally and press the slot; aim at nothing (or the sky) to cast on yourself |
| Priest | Rite of Resurrection | walk up to a fallen player and press `E` (5 s); `E`, `Backspace` or `W A S D` cancel |

## Player commands

| Command | Resource | What it does |
|---|---|---|
| `/selectspecies` | rklselectspecies | open the species selection screen |
| `/manageclass` | every class | open the hall of your class: your rank, your spells, the next unlock, the **Skills** tab (the leader also manages members) |
| `/<class>bar` | each class | unlock the spell bar: drag the slots, pick a theme, shape and colour per slot; ESC or *Seal & Close* saves |
| `/<class>bar hide` / `show` / `toggle` | each class | hide or show the bar (spells still cast while it is hidden) |

Bar commands: `/godbar`, `/demonbar`, `/merfolkbar`, `/vampirebar`, `/werewolfbar`, `/fairybar`, `/witchbar`,
`/elfbar`, `/archerbar`, `/kitsunebar`, `/priestbar`, `/assassinbar`.

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

## rklui: HUD, mana and mock battles

| Command | What it does |
|---|---|
| `/hudsettings` | the HUD settings: essence, metal, size, position, numbers, parts, effects |
| `/rest` | sit down and regenerate |
| `/mana` | your mana pool |
| `/buffs` | the detail panel of your buffs, debuffs, statuses and marks |
| `/mockbattle <id>` | challenge a nearby player to a non-lethal duel (`accept` / `decline`) |
| `/mockbattle ring` / `join <hostId>` / `start` / `leave` | a free-for-all ring of up to 8 players |
| `/mockstats` | your mock battle record and the class table |
| `/hidehud` | hide or show the whole UI, every class bar included |
| `/setmana <id> <value \| max>` | admin: set a player's mana pool |
| `/classes` | admin: the registered classes and the players online per class |
| `/mockbattle stop <hostId>` | admin: stop a battle |

A mock battle is non-lethal: fighters are healed and refilled at the start, cannot drop below a knock-out threshold,
and outsiders cannot hit them. Wins, losses and KOs are kept per player and per class (`/mockstats`).
