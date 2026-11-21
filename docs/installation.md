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
| `rklui` | one shared mana pool for every class, the fantasy HUD, the class network (statuses, shields, elements and reactions, cross-class buffs) and mock battles. Without it every class runs alone on its own mana (armour by default). |
| `rklspawnmonster` | monster and boss kills give class XP |

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
rklselectspecies/   the species selection screen
```

Every class is a complete resource on its own: its spells, icons, models, particles and sounds are inside its own
folder. You can run all ten or only the ones you want.

## Steps

1. Put the `[class]` folder and `rklselectspecies` in your server's `resources` folder. Keep the folder names.
2. Add to `server.cfg`, **after** your framework:

   ```cfg
   ensure ox_lib
   ensure oxmysql
   ensure rklui                 # optional: shared mana, HUD, mock battles
   ensure [class]
   ensure rklselectspecies
   ```

   A folder in square brackets starts every resource inside it. If you already start a parent folder (for example
   `ensure [rkl]`), there is nothing to add.
3. Give your admins the rights:

   ```cfg
   add_ace group.admin rklclass.admin allow             # /setclass, the spell editor, the level commands (every class)
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
