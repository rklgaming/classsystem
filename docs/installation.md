# Installation

[Back to the overview](../README.md)

## Requirements

| Resource | Needed for |
|---|---|
| [ox_lib](https://github.com/overextended/ox_lib) | keybinds and callbacks (every class) |
| [oxmysql](https://github.com/overextended/oxmysql) | who holds which class, the levels, the species changes and the hall's offline members |
| OneSync | server-side checks of positions and hits |
| ESX Legacy, QBCore or Qbox | optional: detected on their own. Without a framework the classes run standalone through ACE |

**Optional**

| Resource | What it adds |
|---|---|
| `rklspawnmonster` | monster and boss kills give class XP |
| an ambulance / revive script | the Priest's **Rite of Resurrection** raises fallen players through it (esx_ambulancejob, esx_death, qb-ambulancejob, qbx_medical, wasabi_ambulance, ars_ambulancejob, or your own); without one it uses its own standalone get-up. See [Integration](integration.md#the-priests-rite-of-resurrection-revive--ambulance-systems). |
| ox_inventory (ESX) | needed only by rklui's Stat part (potions, crafting, item effects); switch that part off without it |

## What you get

```
[class]/
  rklgods/          God
  rkldemon/         Demon
  rklmerfolk/       Merfolk
  rklvampire/       Vampire
  rklwerewolf/      Werewolf
  rklfairyspells/   Fairy
  rklwitchspells/   Witch
  rklelf/           Elf (Elementalist)
  rklarcher/        Archer
  rklkitsune/       Kitsune
  rklpriest/        Priest
rklselectspecies/   the species selection screen
rklui/              the fantasy HUD + the shared class mana and class network + mock battles
```

Every class is a complete resource on its own: its spells, icons, models, particles and sounds are inside its own
folder. You can run all eleven or only the ones you want.

**rklui** has three parts, each with a switch in its `config.lua` (`Config.Modules = { Hud = true, Mana = true, Stat = true }`):

| Part | What it is |
|---|---|
| Hud | the fantasy vitals HUD: health and mana orbs, stamina / breath, hunger and thirst, `/hudsettings`, `/rest` |
| Mana | one server-checked mana pool shared by every class + the class network (statuses, shields, marks, elements and reactions, cross-class buffs, one move-speed arbiter) + mock battles |
| Stat | potions, crafting and item effects for ESX + ox_inventory; switch it off (`Stat = false`) if you do not use it |

Without rklui every class runs alone on its own mana pool (armour by default). If you keep rklui started but turn its
Mana part off, set `Config.Rklmana.Enabled = false` in each class.

## Steps

1. Put the `[class]` folder, `rklui` and `rklselectspecies` in your server's `resources` folder. Keep the folder names
   (the classes call `exports.rklui`).
2. Add to `server.cfg`, **after** your framework:

   ```cfg
   ensure ox_lib
   ensure oxmysql
   ensure rklui                 # the HUD + shared mana (after es_extended / ox_inventory)
   ensure [class]
   ensure rklselectspecies
   ```

   A folder in square brackets starts every resource inside it. If you already start a parent folder (for example
   `ensure [rkl]`), there is nothing to add.
3. Give your admins the rights:

   ```cfg
   add_ace group.admin rklclass.admin allow             # /setclass, the spell editor, the level commands (every class)
   add_ace group.admin rklmana.admin allow              # rklui: /setmana, /classes, /manadebug, stopping a mock battle
   add_ace group.admin rklselectspecies.admin allow     # admin-only species, cooldown bypass, /resetspecies
   ```

   ESX / QBCore / Qbox admin groups (`admin`, `superadmin`, `owner`, `god`) count as admins too
   (`Config.ClassStore.adminGroups`).
4. Restart the server. On the first start these tables are created on their own:

   | Table | Holds |
   |---|---|
   | `rkl_classsystem` | which class (and rank) each character holds; one table for every class |
   | `rkl_classlevels` | level, XP, skill points and spell ranks per character per class |
   | `rkl_selectspecies` | the last species change per character (for the change cooldown) |

   A manual import is in each resource's `setup/` folder if you prefer it.
5. Give yourself a class to test: `/setclass <your server id> vampire 9` (rank 10 = every spell), or open
   `/selectspecies`.

## Frameworks

- **Auto-detect** (`Config.Framework = 'auto'`): Qbox, then QBCore, then ESX.
- **Standalone**: `Config.Framework = 'standalone'`. Access goes through ACE; the player's license is the identifier.
- **Class storage**: by default (`Config.ClassSource = 'sql'`) the class lives in the `rkl_classsystem` table, so no
  framework job is needed. `Config.ClassSource = 'job'` uses a framework job per class instead (the job files for ESX,
  QBCore and Qbox are in each resource's `setup/` folder). On the first `sql` start, characters that already hold the
  class job are copied into the table once.

## Editable files

These files stay open (also under Cfx escrow):

| File | What it is for |
|---|---|
| `config.lua` | every number, colour, model, particle, sound, timing and key; switches |
| `language.lua` | every text (English + Tagalog; add a `Lang.xx` table and set `Locale`) |
| `client/client_open.lua` | damage to players / NPCs / vehicles, the mana pool, the framework's job events |
| `server/server_open.lua` | every framework call of the server: identifiers, the hall's members, the Discord webhook of the hall log |
| `client/passive.lua`, `server/passive.lua` | the class passive |

## Updating

Replace the resource folders, keep your `config.lua` / `language.lua` changes (compare them with the new files), and
keep `data/spell_overrides.json` (the spell editor's saved values) and `boss_log.json` (the hall log).
