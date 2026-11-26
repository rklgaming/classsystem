# RKL Class System

Twenty fantasy classes for FiveM, each with ten spells, a passive and its own class hall, plus class levels 1-50 with
spell ranks, an in-game species selection screen and a fantasy HUD with one shared mana pool for every class.

**Interactive guide: https://rklgaming.github.io/classsystem/** - a task finder ("How do I...?"), every class with its spells,
passive, ranks and real screenshots, a level / spell rank calculator, and every command, config section and export, searchable.

This repository holds the **documentation only**: how to install, set up and use the Class System. The scripts are
sold on our Tebex store and are not part of this repository.

| | |
|---|---|
| **Classes** | God · Demon · Merfolk · Vampire · Werewolf · Fairy · Witch · Elf · Archer · Kitsune · Priest · Assassin · Knight · Oni · Samurai · Shaman · Alchemist · Dragonkin · Necromancer · Chronomancer |
| **Spells** | 216 (ten per class + sixteen quick abilities) and twenty passives; the Priest also raises fallen players (works with your ambulance script) |
| **Progression** | ten ranks per class (the class hall) + levels 1-50 with skill points and spell ranks |
| **HUD + mana** | `rklui`: health and mana orbs, one shared server-checked mana pool, buffs |
| **Spell showcase** | `/mockfight demon elf`: two NPC fighters cast every spell of their class at each other, with HP bars and a winner; harmless, everyone near sees it |
| **Frameworks** | ESX Legacy, QBCore, Qbox (auto-detected) or standalone through ACE |
| **Needs** | ox_lib, oxmysql, OneSync |

## Documentation

**New to FiveM or not a developer? Start with [Getting started](docs/getting-started.md)** - from download to your
first spell, step by step.

| Page | What is in it |
|---|---|
| [Getting started](docs/getting-started.md) | for beginners: download, folders, `server.cfg`, admin rights, first test - no coding |
| [How-to](docs/how-to.md) | every admin job step by step: give classes, change spells, levels, the hall, languages, the Priest's revive, updates |
| [Player guide](docs/player-guide.md) | for your players: pick a class, cast, the bar, levels, the hall, the `/mockfight` spell showcase |
| [FAQ and glossary](docs/faq.md) | common questions and every word explained |
| [Installation](docs/installation.md) | requirements, folders, `ensure` order, permissions, the database tables, the first class |
| [Commands and controls](docs/commands-and-controls.md) | how players pick, cast and level a class; every command and keybind |
| [Configuration](docs/configuration.md) | the `config.lua` of a class, section by section, the showcase look (`config_preview.lua`), `/mockfight` and the species screen's config |
| [Levels and spell ranks](docs/levels.md) | XP, levels, skill points, spell ranks, respec, admin tools |
| [The classes](docs/classes.md) | each class: its theme, mana, passive and spells in short |
| [Integration and exports](docs/integration.md) | exports, events and state bags for your own scripts |
| [Troubleshooting](docs/troubleshooting.md) | common problems and how to get support |
| [What's new](docs/changelog.md) | the latest changes and the current version of every class |

## Quick start

```cfg
ensure ox_lib
ensure oxmysql
ensure es_extended          # or qb-core / qbx_core (leave out for standalone)
ensure rklui                # the HUD + shared mana (keep the folder name rklui)
ensure [class]              # the folder with the twenty class resources
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
