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
| A player cannot cast anything | They hold no class, or a different one: check `Player(id).state['rkl:class']`, give one with `/setclass`. Spells also need **right mouse held** while pressing `1`-`0` (`Config.Casting.requireAim`). |
| A slot shows chains | The spell is locked by rank (the tooltip names the rank it needs). Promote the player in the hall, or change `Config.SpellLadder`. |
| "Your mana is still loading" | rklui has not built the player's pool yet (right after joining or a rklui restart); try again a moment later. |
| `/setclass` says no permission | Add `add_ace group.admin rklclass.admin allow` and put your account in `group.admin`, or run it from the server console. |
| A class is missing on `/selectspecies` | Its resource is not running (the screen hides it, `Config.UI.hideSealed`), or it is admin-only (`Config.Rules.adminOnly`). |
| "Try again later" on the species screen | A change cooldown is set but the store cannot be read (oxmysql not started). |
| The hall says "member records are not available" | oxmysql is not started; online members still work. |
| No leader in the hall | The leader is the highest grade (or a grade named `boss`); check the console `hall:` line or set `Config.Boss.grades`. |
| Two clients on one account share cooldowns | Run `/<resource>cdkeys` in the console; if two players show the same key, set `Config.CooldownKey = 'session'`. |
| No XP from monsters | XP for kills needs rklspawnmonster; spell XP only counts hits on other players (2 XP, capped per minute). |

## Testing alone

`Config.HurtCasterForTesting = true` makes every spell hit its own caster too (aim at your own feet). Turn it off again
before going live.

## Support

- Discord: https://discord.gg/sBFhxRBJvX - open a ticket with the class name, what you did, and the line from your F8 /
  server console.
- Tebex store page: *to be added*.
