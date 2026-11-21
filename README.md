# RKL Class System

Ten fantasy classes for FiveM, each with ten spells, a passive and its own class hall, plus class levels 1-50 with
spell ranks, an in-game species selection screen and a fantasy HUD with one shared mana pool for every class.

This repository holds the **documentation only**: how to install, set up and use the Class System. The scripts are
sold on our Tebex store and are not part of this repository.

| | |
|---|---|
| **Classes** | God · Demon · Merfolk · Vampire · Werewolf · Fairy · Witch · Elf · Archer · Kitsune |
| **Spells** | 106 (ten per class + six quick abilities) and ten passives |
| **Progression** | ten ranks per class (the class hall) + levels 1-50 with skill points and spell ranks |
| **HUD + mana** | `rklui`: health and mana orbs, one shared server-checked mana pool, buffs, mock battles |
| **Frameworks** | ESX Legacy, QBCore, Qbox (auto-detected) or standalone through ACE |
| **Needs** | ox_lib, oxmysql, OneSync |

## Documentation

| Page | What is in it |
|---|---|
| [Installation](docs/installation.md) | requirements, folders, `ensure` order, permissions, the database tables, the first class |
| [Commands and controls](docs/commands-and-controls.md) | how players pick, cast and level a class; every command and keybind |
| [Configuration](docs/configuration.md) | the `config.lua` of a class, section by section, and the species screen's config |
| [Levels and spell ranks](docs/levels.md) | XP, levels, skill points, spell ranks, respec, admin tools |
| [The classes](docs/classes.md) | each class: its theme, mana, passive and spells in short |
| [Integration and exports](docs/integration.md) | exports, events and state bags for your own scripts |
| [Troubleshooting](docs/troubleshooting.md) | common problems and how to get support |

## Quick start

```cfg
ensure ox_lib
ensure oxmysql
ensure es_extended          # or qb-core / qbx_core (leave out for standalone)
ensure rklui                # the HUD + shared mana (keep the folder name rklui)
ensure [class]              # the folder with the ten class resources
ensure rklselectspecies
add_ace group.admin rklclass.admin allow
add_ace group.admin rklmana.admin allow
add_ace group.admin rklselectspecies.admin allow
```

Restart the server. Players open **`/selectspecies`** to pick a class (or an admin gives one with
**`/setclass <id> <class> [grade]`**), then hold **right mouse** and press **`1`-`0`** to cast.

## Support

- Discord: https://discord.gg/sBFhxRBJvX (open a ticket with the class name and the line from your F8 / server console)
- Store: your purchase on our Tebex store (link: *to be added*)

The class resources are licensed per server. Do not resell or share them.
