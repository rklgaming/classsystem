# Levels and spell ranks

[Back to the overview](../README.md)

Every member has a **level in each class** (`Config.Levels`). Switching species keeps each class's own level: a vampire
at level 30 who tries the elf starts the elf at level 1 and is still level 30 when they go back.

## How it works

1. **XP** comes from playing the class (only players in this class get it):

   | Source | Default | Notes |
   |---|---|---|
   | a spell that the server saw land on another player | 2 XP | at most 60 XP a minute; the same victim again only after 30 s |
   | a monster kill (`rklspawnmonster`) | 25 XP | every credited player |
   | a boss kill | +200 XP | on top of the monster kill |
   | a mock battle round (rklui) | 10 XP each fighter, +50 XP the winner | rounds per hour are capped |

   Protected or dead players give nothing. The caps follow the character (a relog keeps them). Any source with
   `xp = 0` is off.
2. **Levels** go from 1 to 50 (`maxLevel`). XP from level L to L + 1 = `floor(100 * L ^ 1.5)` (`curve`): level 1 needs
   100, level 10 needs 3,162, level 49 needs 34,300.
3. **Skill points**: one per level (`pointsPerLevel`).
4. **Spell ranks**: spend points in the hall (`/manageclass` > **Skills**). Every spell card shows its rank pips, what
   the next rank gives in plain numbers and an **Upgrade** button. By default a spell has 5 ranks (`maxRank`), and one
   rank gives **+6 % power, -4 % cooldown, -3 % mana cost** (`perRank`): rank 5 = +30 % / -20 % / -15 %.
5. **Respec**: *Reset skills* gives every spent point back. `reset.mode` = `'free'`, `'cooldown'` (once every `hours`,
   default 24) or `'admin'`.

Ranks scale a spell's own numbers before buffs and before the PvP caps (one hit at most 50, crowd control at most
2.5 s), so levels never break PvP balance. `limits` caps what ranks can ever do (power at most x1.5, cooldown and cost
at least x0.5, range at most +50 %).

The spell bar shows a small level badge; a level up shows a toast, a glow on the bar and a chime (`ui`).

## Config.Levels

```lua
Config.Levels = {
    Enabled        = true,
    maxLevel       = 50,
    curve          = { base = 100, exp = 1.5 },
    pointsPerLevel = 1,
    maxRank        = 5,
    perRank        = { power = 0.06, cooldown = 0.04, cost = 0.03, range = 0.0 },
    limits         = { power = 1.50, cooldown = 0.50, cost = 0.50, range = 0.50 },
    unlockByLevel  = false,                                     -- true: spells unlock by level instead of by rank
    levelLadder    = { 1, 1, 3, 6, 10, 15, 20, 26, 33, 40 },    -- bar slot 1..10 -> level (unlockByLevel only)
    quickLevel     = 12,
    reset          = { mode = 'cooldown', hours = 24 },
    xp = {
        spellHit    = { xp = 2, perMinuteCap = 60, sameTargetSec = 30 },
        monsterKill = { xp = 25 },
        bossKill    = { xp = 200 },
        mockWin     = { xp = 50, perHour = 6 },
        mockRound   = { xp = 10, perHour = 12 },
    },
    clientReasons  = {},                                        -- client XP requests allowed, e.g. { fishing = 30 }
    store          = { table = 'rkl_classlevels', flushSeconds = 30 },
    ui             = { barBadge = true, toast = true, sound = true },
    commands       = { xp = 'classxp', level = 'classlevel', points = 'classpoints', resetWord = 'reset' },
}
```

**Per spell**: a spell block can carry its own `levels = { maxRank = 3, power = 0.10 }`, or `levels = false` (no
ranks). With `unlockByLevel = true` a spell unlocks at its own `unlockLevel`, else at `levelLadder[its slot]`.

`Enabled = false` turns everything off: no levels, no XP, no ranks, no Skills tab, no badge.

## Storage

One oxmysql table for every class, `rkl_classlevels` (`identifier`, `class`, `level`, `xp`, `points`, `skills` JSON,
`reset_at`, `updated_at`; primary key identifier + class), created at start (`setup/rkl_classlevels.sql`). A member's
row is read when they load, and written in batches every 30 s, when they drop or leave the class and when the resource
stops. Nothing polls.

## Admin commands

```
/classxp     <server id> <amount>          give XP (levels up as needed)
/classlevel  <server id> <level>           set the level (points follow the level)
/classpoints <server id> <n | reset>       add (or take, n < 0) unspent points; reset = refund every rank
```

The class the target player is in answers, with the same admins as that class's `/setclass`.

For the level exports (AddXP, SetLevel, GetLevel ...), see [Integration and exports](integration.md).
