# What's new

[Back to the overview](../README.md)

Every class prints its core version in the server console on start. Each class's own changes are in the `README.md`
inside its resource.

## Class core 3.2.9 (November 2026)

- **Dashes stay on the ground.** Every dash, leap, lunge and blink now follows the floor on slopes, stairs, bridges and
  indoors, stops before walls and never ends under the floor. Settings: `Config.DashGround` in each class's
  `config.lua`; `Enabled = false` brings back the old straight-line dashes.
- **The quick ability moved from `B` to `G`** in the eight classes that have one (Vampire, Fairy, Witch, Elf, Archer,
  Kitsune, Priest, Assassin), because `B` is often taken by other scripts. Every player gets `G`, even those who had
  bound the old key; anyone can pick another key under **Settings > Key Bindings > FiveM** (listed as *Class: spell*).
- **Vampire 1.2.2:** while Sword Dance's swords wait, `G` throws them all; Shadow Dash works again once they are gone.

## Class core 3.2.8 (November 2026)

- A new casting look for the God and the Demon.

## Class core 3.2.7 and rklui 3.1.0 (November 2026)

- **The `/mockfight` spell showcase**: two NPC fighters cast every spell of two classes at each other, with HP bars and
  a winner. Harmless, and everyone nearby sees it. Each class's open `config_preview.lua` sets how its fighter looks;
  see [Commands and controls](commands-and-controls.md#the-mock-fight-spell-showcase).
- The older PvP mock battle of rklui is switched off (`Config.MockBattle.Enabled = false`).

## Current versions

| Resource | Version |
|---|---|
| `rklgods` (God) | 1.3.1 |
| `rkldemon` (Demon) | 1.3.1 |
| `rklmerfolk` (Merfolk) | 1.2.1 |
| `rklvampire` (Vampire) | 1.2.2 |
| `rklwerewolf` (Werewolf) | 1.2.1 |
| `rklfairyspells` (Fairy) | 1.2.1 |
| `rklwitchspells` (Witch) | 1.2.1 |
| `rklelf` (Elf) | 1.5.1 |
| `rklarcher` (Archer) | 1.1.1 |
| `rklkitsune` (Kitsune) | 1.1.1 |
| `rklpriest` (Priest) | 1.0.1 |
| `rklassassin` (Assassin) | 1.2.1 |
| `rklui` (HUD, shared mana, `/mockfight`) | 3.1.0 |

Every class above runs class core 3.2.9.
