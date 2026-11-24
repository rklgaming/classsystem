# Troubleshooting

[Back to the overview](../README.md)

## First checks

- On start every class prints a line in the server console with its core version and the mana pool it uses, then the
  hall's grades (`hall: 10 grades ... boss grade 9`). No line = the resource did not start: check the `ensure` order and
  that ox_lib and oxmysql start first.
- `Config.Debug = true` in a class's `config.lua` prints every cast and every refusal in the server console.
- Look for **"exists in more than one place"** in the server log: two resources with the same folder name (for example
  an old copy of a class) make FiveM start only one of them.

## Common problems

| Problem | Fix |
|---|---|
| *"You lack the required entitlement"* in the console | The server's license key belongs to another Cfx.re account than the one that bought the asset. Use a license key from the buying account (keymaster / Cfx.re Portal), or have the asset transferred to the account of your key. |
| *"Couldn't find resource ox_lib"* or *"... oxmysql"* | That resource is not in your `resources` folder, or its `ensure` line is missing / below the classes. Download the **release** zip ([Getting started](getting-started.md#step-1---check-what-your-server-already-has)) and put `ensure ox_lib` and `ensure oxmysql` above `ensure [class]`. |
| *"@ox_lib/init.lua"* errors | You downloaded ox_lib's source code instead of the release zip. Download `ox_lib.zip` from its releases page. |
| oxmysql says it cannot connect | Your database line (`set mysql_connection_string ...`) in `server.cfg` is missing or wrong. txAdmin recipes add it for you; check the user, password and database name. |
| Nothing happens, no errors | The folders were renamed, or `ensure [class]` is missing. Keep the folder names exactly as shipped. |
| A player cannot cast anything | They hold no class, or a different one: check `Player(id).state['rkl:class']`, give one with `/setclass`. Spells also need **right mouse held** while pressing `1`-`0` (`Config.Casting.requireAim`). |
| The quick ability does nothing on `B` | Since class core 3.2.9 it is on `G`. Players can pick any key under **Settings > Key Bindings > FiveM** (listed as *Class: spell*); a different default for everyone is `key = '...'` in that spell's block in `config.lua`. |
| A dash, leap or blink ends inside a slope or under the floor | Update the class to class core 3.2.9 or later and check that `Config.DashGround.Enabled` is `true` in its `config.lua`. |
| A slot shows chains | The spell is locked by rank (the tooltip names the rank it needs). Promote the player in the hall, or change `Config.SpellLadder`. |
| "Your mana is still loading" | rklui has not built the player's pool yet (right after joining or a rklui restart); try again a moment later. |
| `/setclass` says no permission | Add `add_ace group.admin rklclass.admin allow` and put your account in `group.admin`, or run it from the server console. |
| A class is missing on `/selectspecies` | Its resource is not running (the screen hides it, `Config.UI.hideSealed`), or it is admin-only (`Config.Rules.adminOnly`). |
| "Try again later" on the species screen | A change cooldown is set but the store cannot be read (oxmysql not started). |
| The hall says "member records are not available" | oxmysql is not started; online members still work. |
| No leader in the hall | The leader is the highest grade (or a grade named `boss`); check the console `hall:` line or set `Config.Boss.grades`. |
| Two clients on one account share cooldowns | Run `/<resource>cdkeys` in the console; if two players show the same key, set `Config.CooldownKey = 'session'`. |
| The `[E] Rite of Resurrection` prompt does not show over a fallen player | Your ambulance script marks "down" in a way the Priest does not know yet: add its state bag key to `Config.Revive.deadBags`, or edit `PriestSpellsOpen.IsDeadBody` in `rklpriest/client/client_open.lua`. The prompt never shows for a player in a vehicle (`skipInVehicle`). |
| The rite finishes but the player stays down | `Config.Revive.system` calls the wrong script (or an event your version renamed): set `system` to your script, use `'custom'` with its revive event, or edit `PriestServerOpen.RevivePlayer` in `server/server_open.lua`. `Config.Debug = true` shows which system `'auto'` picked. |
| "Not down" when the player clearly is | The server's check `PriestServerOpen.IsPlayerDead` does not know your script: edit it in `server/server_open.lua`, or add the state bag key to `Config.Revive.deadBags`. |
| No XP from monsters | XP for kills needs rklspawnmonster; spell XP only counts hits on other players (2 XP, capped per minute). |
| `/mockfight` says *"No room here"* | Both fighters need flat, dry ground in front of you: stand on open ground, on foot, facing open space (not water, stairs or a steep slope). |
| *"Another mock fight is too close"* or *"Too many mock fights"* | Fights keep 70 m apart and at most 3 run at once (`Config.MockFight.MinDistance`, `MaxActive`). Move away or wait. |
| *"... is not running on this server"* or *"... has no showcase yet"* | That class's resource is stopped, or it is older than class core 3.2.7 (no `config_preview.lua`): start or update the class. |
| The mock fight ends early | The player who started it walked more than 90 m away (`Config.MockFight.LeaveRange`), left, or typed `/mockfight stop`. |
| `/mockbattle` says it is switched off | Since rklui 3.1.0 the PvP mock battle is off by default; the spell showcase is `/mockfight`. To bring the battle back: `Config.MockBattle.Enabled = true` in `rklui/config_mana.lua`. |

## Testing alone

`Config.HurtCasterForTesting = true` makes every spell hit its own caster too (aim at your own feet). Turn it off again
before going live.

To see every spell of two classes without a second player, type `/mockfight <class> <class>` (rklui), for example
`/mockfight demon elf`.

## Support

- Discord: https://discord.gg/sBFhxRBJvX - open a ticket with the class name, what you did, and the line from your F8 /
  server console.
- Tebex store page: *to be added*.
