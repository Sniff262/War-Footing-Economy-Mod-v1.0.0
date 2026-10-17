WAR FOOTING - ECONOMY MOD  v1.0.0
Made for War Footing 1.0.1 (Windows / Steam)
Unofficial fan mod. Not affiliated with or endorsed by the game's developer.
======================================================================

Build a defense economy that snowballs - realistically.

 * ARMS EXPORTS (Industry > Arms Exports tab)
   Sell equipment your own factories built to 20 client states in Africa,
   Asia, Latin America, the Middle East and Europe. Each client has its own
   budget and shopping list, and all but the richest have a ceiling on what
   they pay per unit. Thin-budget militaries want rifles, anti-tank weapons,
   mortars and trucks; middle-income ones want armour, artillery and
   helicopters. Jets, ground-attack aircraft and SAM systems are strategic
   arms: a client buys them only from a supplier it trusts (trade ties 40+)
   and only if they fit its price ceiling, so older, cheaper ones suit
   poorer clients and modern ones go to the rich. Sales build trade ties and
   export reputation, which raise prices and budgets. Licensed designs pay
   the licensor a royalty and cannot be sold to the licensor's rival bloc.

 * LOBBYING (Politics > Defense Budget, 5th slider)
   Spend part of your weekly income lobbying parliament to raise your base
   income permanently. About 10 cents of extra weekly income per dollar,
   better with high stability, a big industry and a good export reputation.

 * CHEAPER MASS PRODUCTION (Industry > Domestic Production)
   - Volume discount: bigger queue orders and programs cost less per unit
     (up to 25% off).
   - Learning curve: every design gets cheaper and faster to build the more
     you make (down to 40% of its starting cost on a fully mature line).
     Running programs re-price their remaining payments as the line matures.

 * MORE PRODUCTION PROGRAMS
   3 at once, plus 1 per 500 points of production capacity, plus 1 per level
   of the new Program Management Office facility (5 levels).

 * PROFIT TRACKING
   The Arms Exports tab shows what each design costs you to build, your
   margin at the best offer, lifetime profit, and how much of a license
   your exports have paid back.

The in-game Field Manual (? Help) explains every rule in detail.


INSTALL
-------
1. Close War Footing.
2. Extract this zip anywhere (right-click > Extract All).
3. Double-click "Install Economy Mod.bat".

That's all. The installer finds the game through Steam. If it can't, it
asks you for the game folder: in Steam, right-click War Footing > Manage >
Browse local files, then drag "War Footing.exe" into the installer window
and press Enter.

Nothing else needs to be installed. It needs about 130 MB of free disk
space on the game's drive while it works.

Windows may warn that the file came from the internet: choose "Run" (or
"More info" > "Run anyway").

What the installer does, in plain terms: "Install Economy Mod.bat" runs
mod\installer.js using the game's own program (War Footing.exe can run
scripts). It uses PowerShell only to ask Steam where the game is installed
and to check that the game is closed. It changes one file,
resources\app.asar, after copying it to resources\app.asar.economy-mod-backup,
and writes resources\economy-mod-install.json to remember what it did.
Everything is plain text in the "mod" folder if you want to read it first.


UNINSTALL
---------
Double-click "Uninstall Economy Mod.bat". It puts the original game file
back and deletes the backup.
Alternatively: Steam > right-click War Footing > Properties > Installed
Files > "Verify integrity of game files". (That leaves the 60 MB backup
file behind; run "Uninstall Economy Mod.bat" once afterwards to remove it.)


SAVES, STEAM CLOUD AND ACHIEVEMENTS
-----------------------------------
 * Your existing campaigns keep working. They pick the mod up mid-game
   (with the Lobbying slider at 0%).
 * Modded saves still load in the unmodded game, which ignores the new
   data. If you uninstall mid-campaign, set Lobbying to 0% first: the
   unmodded game spreads that share over the other sliders anyway, but its
   Budget panel shows a total under 100% until you move a slider.
 * Saves live in %APPDATA%\war-footing, and Steam Cloud keeps a copy. To
   restore a folder backup later, first turn off Steam Cloud for War
   Footing (Steam > right-click War Footing > Properties > General), or the
   newer cloud save replaces it.
 * Steam achievements stay on while the mod is installed, and the stronger
   economy makes some of them (War Chest, Armored Might, scenario wins)
   easier.


GAME UPDATES
------------
A game update from Steam replaces the game files, which removes the mod.
Run "Install Economy Mod.bat" again afterwards.
 * If the game changed at all since the version this mod was tested on, the
   installer tells you and asks before installing.
 * If the update changed the parts of the game the mod edits, it refuses
   and changes nothing. Wait for a mod update.


TROUBLESHOOTING
---------------
 * "War Footing is running": close the game completely and run the
   installer again.
 * "Windows would not let the installer...": something else had the game
   file open, usually a Steam update or file check, or an antivirus scan.
   Wait for it to finish and run the installer again. If it keeps
   happening, check your antivirus history in case it blocked the file.
 * "... is marked Read-only": right-click that file > Properties > untick
   "Read-only", then run the installer again.
 * The game won't start after installing: run "Uninstall Economy Mod.bat",
   or use Steam's "Verify integrity of game files".


STEAM DECK / LINUX
------------------
The .bat files are Windows-only. The installer itself works anywhere with
Node.js 16 or newer:
1. Close the game (on the Deck, switch to Desktop Mode).
2. Get Node.js: download the "Linux x64" .tar.xz from nodejs.org and
   extract it into your home folder (no root needed).
3. Open a terminal (Konsole) in the extracted mod folder - the one that
   contains "mod" and this README.
4. Run (adjust the Node folder name):
     ~/node-v18.20.4-linux-x64/bin/node mod/installer.js install "$HOME/.local/share/Steam/steamapps/common/War Footing"
   On an SD card the game is in /run/media/<card>/steamapps/common/War Footing
   (Steam > Manage > Browse local files shows the folder).
   Use "uninstall" instead of "install" to remove the mod.


TUNING (optional, for tinkerers)
--------------------------------
All of the mod's numbers live in the game's data/game_constants.json
(sections production_volume, production_learning, production_programs,
arms_exports and budget_system.lobbying), each with a description. You can
edit them in the installed game archive with the standard "asar" tool. When
you repack, keep Steam's files outside the archive:
    asar pack <folder> app.asar --unpack-dir node_modules/steamworks.js
"Uninstall Economy Mod.bat" still restores the original afterwards.


CHANGELOG
---------
v1.0.0  First public release.
