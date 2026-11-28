# What's new

[Back to the overview](../README.md)

Every class prints its core version in the server console on start. Each class's own changes are in the `README.md`
inside its resource.

## Chronomancer 1.1.0 and Samurai 1.1.2 (November 2026)

- **The Chronomancer is now a rift sorcerer.** A new kit: Rift Step on `G`, Rune Bolt, Rewind, Rift Gate, Rune Shield,
  Drop Rift, Binding Bands, Rift Barrage, Echo Cast, Time Lock and the ultimate Endless Loop; the passive Tempo stays.
  New models and spell icons, and `/mockfight` shows every new spell. Her worn props (Rune Shield's mandala, the Binding
  Bands) vanish on every screen as soon as the player stops being a chronomancer. See
  [The classes](classes.md#chronomancer).
- **Samurai 1.1.2**: the katana disappears from a player who leaves the class (another class set, or the class removed),
  on every screen.

## Twenty classes (November 2026)

- **Eight new classes**: the Knight, Oni, Samurai, Shaman, Alchemist, Dragonkin, Necromancer and Chronomancer. Each has
  ten spells, a quick ability on `G`, a passive, ten ranks and its own hall; see [The classes](classes.md). All twenty
  are on the species screen and in `/mockfight`.
- **Worn and held gear** (the Knight's sword and shield, the Oni's club and mask, the Samurai's katana ...): every piece
  is a row in `config.lua` with a server switch, and each player can hide their own; see
  [Configuration](configuration.md#worn-and-held-gear).
- **Witch 1.3.3**: `Config.RequireWeapon` can make the witch hold a wand (or any weapon from a list) to cast. Off by
  default; see [Configuration](configuration.md#the-witchs-wand-configrequireweapon-rklwitchspells).

## Class core 3.2.11 (November 2026)

- **Personal switches**: `Config.UI.personal` rows show as on / off switches in the bar editor (`/<class>bar`); each
  player's choice is saved on their PC. Scripts read them with the `GetPref` / `SetPref` exports.

## Class core 3.2.10 (November 2026)

- **Cast tells everyone sees**: the wind-up of a spell with a cast bar (a charge on the hands, a seal under the caster)
  now shows on every screen in range, not only the caster's. For developers: `OnChannelStart` / `RelayChannelStart` in
  the class core.

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
| `rklgods` (God) | 1.3.3 |
| `rkldemon` (Demon) | 1.3.3 |
| `rklmerfolk` (Merfolk) | 1.3.2 |
| `rklvampire` (Vampire) | 1.3.3 |
| `rklwerewolf` (Werewolf) | 1.3.3 |
| `rklfairyspells` (Fairy) | 1.3.5 |
| `rklwitchspells` (Witch) | 1.3.3 |
| `rklelf` (Elf) | 1.6.3 |
| `rklarcher` (Archer) | 1.6.6 |
| `rklkitsune` (Kitsune) | 1.2.3 |
| `rklpriest` (Priest) | 1.4.1 |
| `rklassassin` (Assassin) | 1.6.2 |
| `rklknight` (Knight) | 1.1.2 |
| `rkloni` (Oni) | 1.1.1 |
| `rklsamurai` (Samurai) | 1.1.2 |
| `rklshaman` (Shaman) | 1.1.0 |
| `rklalchemist` (Alchemist) | 1.1.0 |
| `rkldragonkin` (Dragonkin) | 1.1.1 |
| `rklnecromancer` (Necromancer) | 1.1.2 |
| `rklchronomancer` (Chronomancer) | 1.1.0 |
| `rklui` (HUD, shared mana, `/mockfight`) | 3.1.0 |

Every class above runs class core 3.2.11.
