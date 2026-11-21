# FAQ and glossary

[Back to the overview](../README.md)

## Questions

### Do I need to know how to code?

No. Installing is copying folders and adding a few lines to `server.cfg` ([Getting started](getting-started.md)).
Spell numbers can be changed in game in the Editor, and everything else is a value in `config.lua` with a comment
next to it.

### Does it work with ESX, QBCore and Qbox?

Yes - it detects your framework by itself. It also runs without any framework (standalone).

### What else do I need?

`ox_lib` and `oxmysql` (both free), and OneSync (on by default on txAdmin servers). An ambulance script is optional:
the Priest's revive uses yours if you have one.

### Will it lag my server?

No. When nobody is casting, every class costs 0.00 ms. It is built for servers with 200 players.

### Can I use only some of the classes?

Yes. Every class is its own resource. Remove the ones you do not want from `resources/[class]`; the species screen
hides them.

### Can a player have two classes at once?

No, one class at a time. But each class keeps its own level, so switching back continues where the player left off.

### Can players change the spells, or give themselves a class or levels?

No. Only admins can: the spell Editor, `/setclass`, `/classxp`, `/classlevel`, `/classpoints` and the hall's admin tabs
are checked by the **server** on every request, so even a player with a modified game is refused. Admins are the
server console, players with the `rklclass.admin` (or `<resource>.admin`) permission, and ESX / QBCore admin groups
(`admin`, `superadmin`, `owner`, `god`).

Players can only change their own things: their spell bar's layout and colours, their keys, their personal switches
and their HUD look. None of that touches the spells or other players. A class leader manages the members of their own
class only, and never anyone of their own rank or higher.

### Can I change the spells?

Yes: damage, mana cost, cooldown, range, cast time, crowd control, the bar slot and the unlock rank in the in-game
Editor (`/manageclass <class>` → **Editor**). Colours, particles and sounds are in `config.lua`.

### Can I change the texts or translate them?

Yes. Every text is in `language.lua` (English and Tagalog included); add your own language there.

### Can I edit the code?

The resources are protected by the Cfx.re asset escrow. These files stay open: `config.lua`, `language.lua`,
`client/client_open.lua`, `server/server_open.lua` and the passive files - the places you need to connect your own
framework, ambulance script or economy.

### Is PvP fair?

Yes. One hit on a player is at most 50, crowd control lasts at most 2.5 s, and every cast, hit, cooldown and heal is
checked by the server. Spells show their area before they land, so players can dodge.

### Which classes heal?

The God and the Priest. Every other class only gets health back by attacking (lifesteal, drain). The Priest's heals
and shields are capped by the server so nobody becomes unkillable.

### How do players get their class?

On the species screen (`/selectspecies`), or an admin gives it with `/setclass`. You can open the screen for new
players automatically ([How-to](how-to.md#show-the-species-screen-to-new-players-automatically)).

### Do I need rklui?

It is included and recommended: one shared mana pool for every class, the fantasy HUD, buffs and mock battles. The
classes also run without it, each on its own mana.

### Where do player levels and classes live?

In your database: `rkl_classsystem`, `rkl_classlevels` and `rkl_selectspecies`, created on their own at the first
start.

### I updated - will players lose their progress?

No. Progress is in the database, not in the resource folders. Keep your `data/spell_overrides.json` (your Editor
changes) when you replace the folders.

### Can I resell or share the files?

No. The licence is for your own server.

### Where do I get help?

Discord: https://discord.gg/sBFhxRBJvX - open a ticket with the class name, what you did, and the line from your F8 or
server console.

## Glossary

| Word | What it means |
|---|---|
| **Resource** | one script folder in `resources`, for example `rklarcher` |
| **server.cfg** | the settings file of your server; `ensure` lines in it start resources |
| **ensure** | the `server.cfg` word that starts a resource (`ensure rklarcher`) |
| **txAdmin** | the web panel to run your server: console, players, restart, CFG editor |
| **Live Console** / **server console** | where the server prints messages and where you type console commands (no `/`) |
| **F8 console** | the in-game console of a player; shows client errors |
| **Server ID** | the number of a player while they are online (txAdmin shows it next to the name) |
| **Identifier / license** | a player's permanent ID (`license:...`), also when they are offline |
| **ACE / add_ace** | FiveM permissions in `server.cfg`, e.g. `add_ace group.admin rklclass.admin allow` |
| **Framework** | the base of your roleplay server: ESX, QBCore or Qbox |
| **Standalone** | running without a framework |
| **ox_lib / oxmysql** | free helper resources many scripts need (library / database connector) |
| **OneSync** | FiveM's server sync; needed for server-side checks (on by default with txAdmin) |
| **Escrow / Cfx.re Portal** | how paid FiveM assets are protected and downloaded (portal.cfx.re → Granted Assets) |
| **Class** / **species** | the same thing: God, Demon, Merfolk ... (the species screen is where players pick one) |
| **Rank / grade** | a player's position in their class: rank 1-10 (grade 0-9); 10 = the leader |
| **Level** | a player's experience in a class, 1-50; every level gives a skill point |
| **Spell rank** | how far a spell is upgraded with skill points (0-5) |
| **Hall** | the class's management screen, `/manageclass` |
| **Editor** | the hall tab where admins change spells in game |
| **Mana** | what spells cost; every class names it (Grace, Rage, Faith ...) |
| **Passive** | a class power that is always on (no button) |
| **Quick ability** | the extra spell on <kbd>B</kbd> |
| **Cooldown** | the waiting time before a spell can be cast again |
| **Crowd control** | stun, root, slow, charm, sleep ... effects that stop or slow a player |
| **Routing bucket** | an instance (apartment, private world); spells stay inside it |
| **Export / event** | how other scripts talk to a resource ([Integration](integration.md)) |
| **NUI** | the HTML screens of a script (the spell bar, the hall, the species screen) |
