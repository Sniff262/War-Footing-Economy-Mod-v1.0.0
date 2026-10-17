# War Footing — Economy Mod v{MOD_VERSION}

**Unofficial fan mod for War Footing {GAME_VERSION}** (Windows / Steam). Build a defense economy that snowballs the realistic way: build cheaply at scale, export to client states, reinvest, and lobby parliament for a bigger budget.

> Not affiliated with or endorsed by the game's developer. Use at your own risk.

**[⬇ Download {ZIP_NAME}]({ZIP_NAME})** ({ZIP_KB} KB) · [Install](#install) · [Uninstall](#uninstall) · [FAQ](#saves-steam-cloud-and-achievements)

---

## What it adds

| Feature | Where | What it does |
|---|---|---|
| **Arms exports** | Industry → *Arms Exports* | Sell equipment your own factories built to 20 client states across Africa, Asia, Latin America, the Middle East and Europe. |
| **Parliamentary lobbying** | Politics → *Defense Budget* (5th slider) | Spend part of your weekly income to raise your base income permanently. |
| **Economies of scale** | Industry → *Domestic Production* | Volume discounts on big orders and a learning curve on every design. |
| **More production programs** | Industry | +1 program slot per 500 production capacity, plus a new Program Management Office facility. |
| **Profit tracking** | Industry → *Arms Exports* | Production cost, margin, lifetime profit and license payback for every design you export. |

### Arms exports
- Every client has its own budget and shopping list, and all but the richest have a ceiling on what they pay per unit.
- Thin-budget militaries want rifles, anti-tank weapons, mortars and trucks; middle-income ones want armour, artillery and helicopters.
- Jets, ground-attack aircraft and SAM systems are **strategic arms**: a client buys them only from a supplier it trusts (**trade ties 40+**) and only if they fit its price ceiling. Older, cheaper ones suit poorer clients; modern ones go to the rich.
- Every delivery builds trade ties and export reputation, which raise prices and budgets.
- Licensed designs pay the licensor a royalty and can't go to its rival bloc. Arming one bloc's clients pleases that bloc and annoys the other.

### Lobbying
About **10 cents of extra weekly income per dollar** spent, more with high stability, a big industry and a good export reputation.

### Economies of scale
- **Volume discount:** up to 25% off big queue orders and programs.
- **Learning curve:** each design gets cheaper and faster to build the more you make, down to 40% of its starting cost on a fully mature line. Running programs re-price their remaining payments as the line matures.

The in-game **Field Manual (? Help)** explains every rule in detail.

## Install

1. Close War Footing.
2. Download **[{ZIP_NAME}]({ZIP_NAME})** and extract it anywhere (right-click → *Extract All*).
3. Double-click **`Install Economy Mod.bat`**.

The installer finds the game through Steam. If it can't, it asks for the game folder: in Steam, right-click War Footing → *Manage* → *Browse local files*, then drag `War Footing.exe` into the installer window and press Enter.

> **If the installer still can't find the game:** move the whole `War Footing Economy Mod v{MOD_VERSION}` folder into your War Footing folder, so it sits next to `War Footing.exe`, and run `Install Economy Mod.bat` from there. It always uses the game folder it's in. Leave the folder there; uninstalling works from there too.

Nothing else needs to be installed, and it needs about 130 MB of free disk space while it works. If Windows warns that the file came from the internet, choose *Run* (or *More info* → *Run anyway*).

<details>
<summary><b>What exactly does the installer do?</b></summary>

- `Install Economy Mod.bat` runs `mod\installer.js` using the game's own program (`War Footing.exe` can run scripts), so you don't need Node or Python.
- It uses PowerShell only to ask Steam where the game is installed and to check that the game is closed.
- It changes one file, `resources\app.asar`, after copying it to `resources\app.asar.economy-mod-backup`, and writes `resources\economy-mod-install.json` to remember what it did.
- The download doesn't include the game's files. `mod\patch.json` contains the mod's own code plus its edits to the game, each with a few lines of the surrounding game code so it can find its place, and the installer applies them to your copy.

Every script is plain text in the `mod` folder.
</details>

**Check your download** (optional) by running this in PowerShell and comparing:

```powershell
Get-FileHash .\{ZIP_NAME}
```

`SHA-256: {SHA256}`

## Uninstall

Double-click **`Uninstall Economy Mod.bat`**. It puts the original game file back and deletes the backup.

Alternatively, in Steam: right-click War Footing → *Properties* → *Installed Files* → *Verify integrity of game files*. That leaves the 60 MB backup file behind; run `Uninstall Economy Mod.bat` once afterwards to remove it.

## Saves, Steam Cloud and achievements

- **Existing campaigns keep working** and pick the mod up mid-game, with the Lobbying slider at 0%.
- **Modded saves still load in the unmodded game**, which ignores the new data. If you uninstall mid-campaign, set Lobbying to 0% first; otherwise the unmodded Budget panel shows a total under 100% until you move a slider.
- **Saves live in `%APPDATA%\war-footing`, and Steam Cloud keeps a copy.** To restore a folder backup later, first turn off Steam Cloud for War Footing (*Properties* → *General*), or the newer cloud save replaces it.
- **Steam achievements stay on**, and the stronger economy makes some of them (War Chest, Armored Might, scenario wins) easier.

## Game updates

A Steam update replaces the game files, which removes the mod. Run `Install Economy Mod.bat` again afterwards.

- If the game changed since the version this mod was tested on, the installer tells you and asks before installing.
- If an update changed the parts of the game the mod edits, it refuses and changes nothing until the mod is updated.

## Troubleshooting

| Message | What to do |
|---|---|
| *War Footing is running* | Close the game completely and run the installer again. |
| *Windows would not let the installer…* | Something else had the game file open, usually a Steam update or file check, or an antivirus scan. Wait for it to finish and try again. If it keeps happening, check your antivirus history. |
| *… is marked Read-only* | Right-click that file → *Properties* → untick *Read-only*, then run the installer again. |
| The game won't start after installing | Run `Uninstall Economy Mod.bat`, or use Steam's *Verify integrity of game files*. |

When reporting a problem, please open an issue and paste what the installer window printed.

## Steam Deck / Linux

The `.bat` files are Windows-only, but the installer itself runs anywhere with **Node.js 16+**:

1. Close the game (on the Deck, switch to Desktop Mode).
2. Download the *Linux x64* `.tar.xz` from [nodejs.org](https://nodejs.org) and extract it into your home folder (no root needed).
3. Open a terminal (Konsole) in the extracted mod folder, the one that contains `mod` and `README.txt`.
4. Run (adjust the Node folder name):

```bash
~/node-v18.20.4-linux-x64/bin/node mod/installer.js install "$HOME/.local/share/Steam/steamapps/common/War Footing"
```

On an SD card the game is in `/run/media/<card>/steamapps/common/War Footing`. Use `uninstall` instead of `install` to remove the mod.

## Tuning

All of the mod's numbers live in the game's `data/game_constants.json` (sections `production_volume`, `production_learning`, `production_programs`, `arms_exports` and `budget_system.lobbying`), each with a description. You can edit them in the installed game archive with the standard [`asar`](https://github.com/electron/asar) tool. When you repack, keep Steam's files outside the archive:

```bash
asar pack <folder> app.asar --unpack-dir node_modules/steamworks.js
```

`Uninstall Economy Mod.bat` still restores the original afterwards.

## Changelog

- **v{MOD_VERSION}**: first public release.

---------
v1.0.0  First public release.
