# Player guide

[Back to the overview](../README.md)

Everything a player can do with a class. Server owners: share this page with your players. Chat commands are typed
after pressing <kbd>T</kbd>.

## Getting a class

### Pick my class

1. Type `/selectspecies` (or use the NPC / menu your server set up).
2. Browse with the mouse or the arrow keys: every class shows its story, mana, elements, passive and three signature
   skills.
3. Press **Embrace this path** (or <kbd>Enter</kbd>) and confirm.
4. Your spell bar appears. You start at rank 1 with the first two spells.

> **Tip:** cannot pick? Your server may allow only one change per cooldown, or keep some classes for admins. Ask an
> admin.

### Change to another class

1. Open `/selectspecies` again and pick another class.
2. Your level in your old class is kept: if you come back, you continue where you left off.

## Casting spells

### Cast a spell

1. Hold the **right mouse button**.
2. Press <kbd>1</kbd> to <kbd>0</kbd> for slot 1 to 10.
3. **Direct** spells go off at once. **Targeted** spells show a circle on the ground: aim it and press <kbd>E</kbd>.
   Red means out of range.

> **Tip:** nothing locks on. The spell lands where you aimed, so you can hit - and you can miss.

### Cancel a spell

1. While aiming: press <kbd>Backspace</kbd> or the right mouse button again.
2. During a cast bar: press <kbd>Backspace</kbd>. You keep your mana and no cooldown starts.

### Use my quick ability

1. Press <kbd>B</kbd> - no aiming needed.
2. Vampire Shadow Dash, Fairy Fae Step, Witch Hex Mirror, Elf Sylvan Veil, Archer Roll Shot, Kitsune Spirit Fox Step,
   Priest Sacred Step, Assassin Shade Step. It unlocks at rank 5.

### End a spell that keeps running

1. A running spell glows on your bar (a whip, a trident, orbiting blades, a ring of fire ...).
2. Hold the right mouse button and press its slot again: it ends, lands or explodes.

### Heal or shield an ally (Priest)

1. Aim at the ally (a small ring marks them) and press the slot: Mending Light <kbd>1</kbd>, Aegis of Faith
   <kbd>3</kbd>, Prayer of Renewal <kbd>4</kbd>, Purify <kbd>5</kbd>, Blessing of Might <kbd>8</kbd>.
2. Aim at nothing (or the sky) to cast it on yourself.

### Raise a fallen player (Priest)

1. Walk up to the fallen player: **[E] Rite of Resurrection** shows over the body.
2. Press <kbd>E</kbd> once. You kneel and a 5 second bar runs.
3. Stay close and do not move: <kbd>E</kbd>, <kbd>Backspace</kbd> or <kbd>W</kbd> <kbd>A</kbd> <kbd>S</kbd>
   <kbd>D</kbd> cancel it (you get your Faith back).

### Use the special keys of my class

1. Some spells use extra keys while they run, for example the Demon Lord: <kbd>E</kbd> fire breath, <kbd>G</kbd> stomp.
2. The full list is in [Commands and controls → Class-specific keys](commands-and-controls.md#class-specific-keys).

## My spell bar

### Move or restyle my spell bar

1. Type `/<class>bar` (for example `/archerbar`, `/priestbar`).
2. Drag the slots where you want them; pick a theme, a slot shape and a colour per slot.
3. Press <kbd>ESC</kbd> or **Seal & Close** to save. It is remembered for you.

### Hide my spell bar

1. Type `/<class>bar hide` (and `show` or `toggle`), or click the small eye button on the bar.
2. Your spells still cast while it is hidden.

### Change my keys

1. Open **Settings → Key Bindings → FiveM**.
2. Search your class name and set new keys for the slots, the quick ability, the bar toggle or the hall.

### Turn my class's extras on or off

1. Open `/<class>bar`. Some classes have personal switches there, for example the God's aura, the Witch's crow, the
   Archer's bow on the back, the Kitsune's mark pips, the Priest's heal numbers and ally ring, the Assassin's daggers in hand and shroud tint.
2. Switch them on or off; they only change what you see.

## Levels and ranks

### Level up my class

1. Hit other players with your spells, defeat monsters and bosses, and fight mock battles: each gives XP.
2. The badge on your bar shows your level. Every level gives you a skill point.

### Rank up a spell

1. Type `/manageclass` and open **Skills** (<kbd>2</kbd>).
2. Each card shows the spell's rank and what the next rank gives.
3. Press **Upgrade** to spend a skill point. A rank adds power and lowers the cooldown and the cost.

### Reset my skill points

1. `/manageclass` → **Skills** → **Reset skills**, then confirm. Every spent point comes back.

> **Tip:** by default you can reset once every 24 hours.

### See my rank and what unlocks next

1. `/manageclass` → **My Rank** (<kbd>1</kbd>): your rank, your spells and the next unlock.
2. **Ranks & Spells** shows the whole ladder.

## The class hall

### Join a class hall

1. The class leader (or a recruiter) invites you. A card shows for 30 seconds.
2. Press <kbd>Y</kbd> to accept or <kbd>N</kbd> to decline.
3. You kneel in the class circle for a short initiation and join at rank 1.

### Run my class as the leader

1. `/manageclass` → **Recruit**: invite players near you or by server ID.
2. **Members**: promote, demote, set a rank or remove a member - even when they are offline.
3. **Log**: every decision, who and when. **Settings**: the initiation ritual on or off.

## Mana, buffs and mock battles

### See my mana and buffs

1. Your mana is the orb on the HUD (and on your bar).
2. `/mana` shows your pool; `/buffs` lists your buffs, debuffs and statuses.

### Change how the HUD looks

1. Type `/hudsettings`: essence, metal frame, size, position, numbers and effects.

### Fight a mock battle (a friendly duel)

1. `/mockbattle <id>` challenges a player near you; they type `/mockbattle accept`.
2. Nobody dies: a knock-out only ends your round, and everyone is healed after.

### Join a mock battle ring

1. The host types `/mockbattle ring`. You type `/mockbattle join <host id>` (up to 8 players).
2. The host types `/mockbattle start`. Last one standing wins. `/mockstats` shows your record.

## When something does not work

### My spell does not cast

1. Are you holding the **right mouse button** while pressing the number?
2. Is the slot locked (chains on it)? Your rank is too low: the tooltip says which rank you need.
3. Is it on cooldown (a timer on the slot) or are you out of mana?
4. Are you stunned, silenced or in a vehicle? Some spells cannot be cast then.

### My bar is gone

1. Type `/<class>bar show`, or `/hidehud` if the whole UI is hidden.
2. Still nothing? You may not hold a class any more: check `/selectspecies` or ask an admin.
