# Getting started (new to FiveM? start here)

[Back to the overview](../README.md)

This page takes you from "I just bought it" to "I am casting spells in game", one step at a time. No programming
needed. If a word is new to you, look it up in the [glossary](faq.md#glossary).

## Step 1 - Check what your server already has

You need a running FiveM server. Most people run it with **txAdmin** (the web panel that comes with FiveM servers).

Open your server's `resources` folder and look for these two folders:

| Folder | What it is | Where to get it if it is missing |
|---|---|---|
| `ox_lib` | a free helper library many scripts use | https://github.com/overextended/ox_lib/releases (download `ox_lib.zip`, not the source code) |
| `oxmysql` | lets scripts talk to your database | https://github.com/overextended/oxmysql/releases (download `oxmysql.zip`) |

> **Tip:** if you installed your server with a txAdmin recipe (ESX, QBCore or Qbox), both are usually already there,
> and your database connection (`set mysql_connection_string ...`) is already in `server.cfg`.

## Step 2 - Download your purchase

1. Open the link from your Tebex purchase email.
2. If the files are protected by the Cfx.re asset escrow, they are in the **Cfx.re Portal**: sign in at
   https://portal.cfx.re with the **same Cfx.re account you used at checkout**, open **Assets → Granted Assets** and
   download them there.
3. Unzip the download on your computer.

> **Tip:** your server's license key must belong to the same Cfx.re account that bought the asset. If not, the server
> console says *"You lack the required entitlement"* and the resource does not start.

## Step 3 - Put the folders in place

1. Copy these folders into your server's `resources` folder:
   - `[class]` (the class resources: `rklgods`, `rkldemon`, `rklmerfolk`, `rklvampire`, `rklwerewolf`,
     `rklfairyspells`, `rklwitchspells`, `rklelf`, `rklarcher`, `rklkitsune`, `rklpriest`, `rklassassin`)
   - `rklui` (the HUD and the shared mana)
   - `rklselectspecies` (the species selection screen)
2. **Do not rename the folders.** The scripts find each other by these names.

> **Tip:** a folder name in square brackets, like `[class]`, is just a group. FiveM starts every resource inside it
> with one line.

## Step 4 - Add the start lines to server.cfg

1. Open `server.cfg` (in txAdmin: **Settings → CFG Editor**; on your PC: open the file with Notepad).
2. Find the line that starts your framework (`ensure es_extended`, `ensure qb-core` or `ensure qbx_core`).
3. Paste these lines **below** it:

   ```cfg
   ensure ox_lib
   ensure oxmysql
   ensure rklui
   ensure [class]
   ensure rklselectspecies
   ```

   If `ensure ox_lib` or `ensure oxmysql` is already higher up in the file, you do not need it twice.
4. Save the file.

## Step 5 - Give yourself admin rights

The admin commands (`/setclass`, the spell Editor, the level commands) only work for admins.

1. Find your **license**: in txAdmin open **Players**, click your name, and copy the line that starts with
   `license:` (for example `license:1a2b3c...`).
2. Add these lines to `server.cfg` (put your own license in the first line):

   ```cfg
   add_principal identifier.license:PUT_YOUR_LICENSE_HERE group.admin
   add_ace group.admin rklclass.admin allow
   add_ace group.admin rklmana.admin allow
   add_ace group.admin rklselectspecies.admin allow
   ```
3. Save, then restart the server.

> **Tip:** on ESX an account in the `admin` / `superadmin` group also counts as admin (ESX: `setgroup <id> admin` in the
> server console). On QBCore the `admin` / `god` permission counts too.

## Step 6 - Restart and check the console

1. Restart the server (txAdmin: **Restart** button).
2. Open the **Live Console** (txAdmin). Each class prints a start line with its core version and its mana pool, then a
   `hall:` line. No red errors = good.
3. The database tables (`rkl_classsystem`, `rkl_classlevels`, `rkl_selectspecies`) are created on their own. You do
   not need to import any SQL.

## Step 7 - Try it in game

1. Join your server.
2. Type `/selectspecies` in the chat (press <kbd>T</kbd>), pick a class and press **Embrace this path**.
3. Your spell bar appears at the bottom of the screen.
4. Hold the **right mouse button** and press <kbd>1</kbd>: you cast your first spell.

> **Tip:** to test every spell at once, give yourself the top rank: in the txAdmin Live Console type
> `setclass 1 vampire 9` (replace `1` with your server ID, shown in txAdmin's player list).

## What next?

- Change spell numbers in game: [How-to → Spells](how-to.md#spells).
- Teach your players the basics: share the [Player guide](player-guide.md).
- Something does not work: [Troubleshooting](troubleshooting.md) and the [FAQ](faq.md).
