# Wife's Bedroom mod converters

Two converters that move character and room mods between **Wife's Bedroom v1.5** and the modded games **Deeproom 4.0.3 Kiwami** and **ModRoom v3.3**. Drag a mod onto a `.bat` file, press Enter at each question, and copy the result into your game.

| You have mods for... | You want to play them in... | Use |
|---|---|---|
| ModRoom, Deeproom or FutasRoom | Wife's Bedroom v1.5 | `Modded_to_WB_1.5/Convert_to_WB_1.5.bat` |
| Wife's Bedroom v1.5 | Deeproom 4.0.3 or ModRoom v3.3 | `WB_1.5_to_Modded/Convert_from_WB_1.5.bat` |

## Features

- Converts lovers, partners and bedrooms both ways between Wife's Bedroom v1.5 and Deeproom 4.0.3 / ModRoom v3.3.
- Can build packs for Deeproom, ModRoom or both in one run.
- Drag and drop a mod folder, a whole game folder or a `.zip`. It finds packs in nested folders and bundles.
- Renames files, rewrites each pack's settings file and adjusts sprite strips to the frame counts the target game uses, so nothing looks cut or shifted.
- Never changes your original files. Packs are converted in a temporary folder first, and existing packs in the destination are never overwritten.
- Skips duplicate packs and writes a report that lists every pack with what was done and why.
- Only needs Python. No extra packages to install.

## What's new in v1.2 (since v1.0)

- **Deeproom 4.0.3 support both ways.** v1.0 only built ModRoom packs and only read ModRoom's folders. v1.2 reads Deeproom's `custom_stuff/` folder and builds packs for Deeproom, ModRoom or both.
- **Sprites fit the target game.** Strips are padded or laid out again to the target game's frame counts, including ModRoom partner portraits. v1.0 only renamed files, so the game could cut sprites into the wrong frames.
- **Correct settings files.** Each pack gets one settings file in the target game's format, with the pose, X-ray and deepthroat positions converted. A missing name, description or author is filled in.
- **Finds more packs.** Nested folders, multi-pack bundles, `.zip` files and Steam Workshop folders with only a number for a name.
- **Duplicates handled.** The same character is converted once, and the other copies are listed in the report. Converting again doesn't leave `_2` copies.
- **Safer runs.** Packs are staged in a temporary folder, existing packs are never overwritten, a broken image or odd file name doesn't stop the run, and `--dry-run` shows what would happen.
- **A report for every run**: `output/conversion_report.md`.
- **Deeproom deepthroat height fixed**, plus a repair for packs converted with older versions (see below).
- **Python only.** Pillow is no longer needed.

Full list: `CHANGELOG.md`. Technical details: each converter's `DETAILS.md` and `core/CHANGELOG.md`.

## Requirements

- Windows for the `.bat` launchers. On other systems, run the `.py` scripts directly (see [Command line](#command-line)).
- Python 3, free from [python.org](https://www.python.org/downloads/). Tick **"Add Python to PATH"** when installing. Tested with Python 3.10.

## Quick start

1. Download the latest release zip from the Releases page and unzip it anywhere.
2. Open the folder for the direction you need (see the table above).
3. Drag a mod folder or `.zip` onto the `.bat` file, or put mods in that folder's `input/` folder and double-click the `.bat`. With nothing dropped and an empty `input/`, it asks for a path.
4. Press Enter at each question to use the recommended answers.
5. When it finishes, press any key, then copy the result from that converter's `output/` folder into your game:

| Converter | Copy this | Into |
|---|---|---|
| Modded to WB 1.5 | `output/custom/` | your Wife's Bedroom v1.5 game folder |
| WB 1.5 to Modded (Deeproom) | `output/Deeproom_Mods/custom_stuff/` | your Deeproom game folder (merge with its `custom_stuff/`) |
| WB 1.5 to Modded (ModRoom) | the contents of `output/ModRoom_Mods/` | your ModRoom game folder |

## The questions it asks

| Question | Default | What it means |
|---|---|---|
| Target game (WB 1.5 to Modded only) | Both | `1` Deeproom, `2` ModRoom, `3` or Enter for both. |
| Approximate mode `[y/N]` | No | Yes also converts strips whose frame counts can't match exactly, by dropping frames. No converts only what fits exactly or with padding, and lists the rest in the report. |
| Skip duplicate packs `[Y/n]` | Yes | If the same character appears more than once, only the best copy is converted. The others are listed in the report. |

## The report

Every run writes `output/conversion_report.md`, which you can open in any text editor. It lists each pack as:

- **ok**: converted exactly.
- **padded**: blank frames were added so the game cuts the strip correctly. Nothing was lost.
- **approximate**: frames were dropped (only with approximate mode on).
- **partial**: some sprites were converted and others were left out. The report says which ones and why.
- **skipped**: not converted, with the reason (for example a duplicate, or a sprite the target game needs is missing).

## Command line

Run the scripts directly to use options or to work outside Windows:

```bash
# Modded to WB 1.5
python Modded_to_WB_1.5/Modded_to_WB_1.5.py input_folder
python Modded_to_WB_1.5/Modded_to_WB_1.5.py -d "C:/Games/WB1.5" -y my_pack.zip

# WB 1.5 to Modded
python WB_1.5_to_Modded/WB_1.5_to_Modded.py -t both input_folder
python WB_1.5_to_Modded/WB_1.5_to_Modded.py -t deeproom -d "C:/Games/Deeproom" -y pack.zip
```

| Option | What it does |
|---|---|
| `-t deeproom\|modroom\|both` | Target game (WB 1.5 to Modded only). |
| `-d <folder>` | Write into this folder (a game folder or any export folder) instead of `output/`. |
| `-y` | Don't ask questions. Use the defaults. |
| `--dry-run` | Convert in a temporary folder and write only the report. Nothing else is written. |
| `--approximate` / `--no-approximate` | Allow or refuse dropping frames where frame counts differ (refused by default). |
| `--clean` | Clear the destination's pack folders before writing (only once something has been converted). |
| `--no-quarantine-duplicates` | Convert every copy of a duplicate pack. |
| `--repair-deepthroat` | WB 1.5 to Modded only: fix older Deeproom conversions (see below). |

All options and the exact conversion rules are in each converter's `DETAILS.md`.

## Partners sitting too high in Deeproom's deepthroat pose?

Partners converted for Deeproom with a version older than 2026-11-17 can have a deepthroat height that draws them too high. To fix them, drag your Deeproom `custom_stuff/custom_wives` folder onto `WB_1.5_to_Modded/Convert_from_WB_1.5.bat`, or run:

```bash
python WB_1.5_to_Modded/WB_1.5_to_Modded.py --repair-deepthroat "<custom_wives folder>"
```

It lists what it would fix and asks before changing anything (`-y` applies without asking, `--dry-run` only lists). It only touches settings the old converter wrote, and it saves the originals in a backup zip next to the folder.

## Known limits

- Some ModRoom animations use more frames than Wife's Bedroom v1.5 (for example a lover's mating press: 24 frames against 9). These convert only with approximate mode, which drops frames.
- When a v1.5 partner is converted for ModRoom, the portrait's eye and blush frames are left blank, because v1.5 portraits don't have them. The partner won't blink or blush in ModRoom, but the rest of the portrait displays normally.
- When building for ModRoom, a pack that lacks a sprite ModRoom needs is skipped (ModRoom would crash on it), and the report says which sprite is missing.

## Troubleshooting

- **The window closes immediately.** Python is probably not installed or not on PATH. Reinstall it with "Add Python to PATH" ticked, or open Command Prompt in the converter's folder and run the `.py` file to see the error.
- **A character is missing from the game.** Check `output/conversion_report.md` for why it was skipped or only partly converted.
- **A character looks wrong in the game.** Check whether the report lists it as *approximate*, and that you copied the folder into the right place (see [Quick start](#quick-start)).

## Repository layout

```text
Modded_to_WB_1.5/      ModRoom / Deeproom / FutasRoom to Wife's Bedroom v1.5
WB_1.5_to_Modded/      Wife's Bedroom v1.5 to Deeproom 4.0.3 / ModRoom v3.3
  *.bat                drag-and-drop launcher
  *.py                 the converter
  core/wbconv.py       shared conversion core (identical in both folders)
  core/CHANGELOG.md    full history of that converter
  DETAILS.md           technical details: frame counts, settings rules, all options
  input/  output/      default input and output folders
  tests/               automated tests
CHANGELOG.md           release notes for both converters
```

Each folder works on its own, so you can copy just the one you need.

## Running the tests

Inside either converter folder:

```bash
python -m unittest discover -s tests
```

## License

MIT License, see `LICENSE`.
