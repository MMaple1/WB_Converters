# Wife's Bedroom mod converters

Two converters that move character and room mods between Wife's Bedroom v1.5 and the modded games (Deeproom 4.0.3 Kiwami, ModRoom v3.3). Each folder works on its own; you only need Python (free from python.org; tick "Add Python to PATH" when installing).

## Features

- Converts character and room packs both ways: Wife's Bedroom v1.5 to and from ModRoom v3.3 / Deeproom 4.0.3.
- Drag and drop a folder or `.zip`; press Enter for the defaults.
- Renames files, rewrites the pack settings and adjusts sprite strips to what the target game expects.
- Skips duplicates and lists anything it could not convert, with the reason.
- Never changes your original files.

## What's new in v1.2 (since v1.1)

- **Both converters in one place**, sharing one tested conversion core.
- **Sprites fit the target game:** strips are padded or re-laid out to the frame counts it uses (ModRoom partner portraits included), so nothing looks cut or shifted.
- **Safer runs:** packs are converted in a temporary folder first, existing packs are never overwritten, and `--dry-run` shows what would happen.
- **No more `_2` copies** when you convert the same pack again.
- **Deeproom deepthroat height fixed**, plus a repair for packs converted with older versions.

Full list: `CHANGELOG.md`. Technical details: each converter's `DETAILS.md` and `core/CHANGELOG.md`.

| You have mods for... | You want to play them in... | Use |
|---|---|---|
| ModRoom, Deeproom or FutasRoom | Wife's Bedroom v1.5 | `Modded_to_WB_1.5/Convert_to_WB_1.5.bat` |
| Wife's Bedroom v1.5 | Deeproom 4.0.3 or ModRoom v3.3 | `WB_1.5_to_Modded/Convert_from_WB_1.5.bat` |

Drag a mod folder or `.zip` onto the `.bat`, press Enter at each question, and copy what appears in that converter's `output/` folder into your game. Each folder's `README.md` has the details.

**Partners sitting too high in Deeproom's deepthroat pose?** Packs converted for Deeproom before 2026-11-17 can carry a wrong height. Drag your Deeproom `custom_stuff/custom_wives` folder onto `WB_1.5_to_Modded/Convert_from_WB_1.5.bat` (or run `WB_1.5_to_Modded.py --repair-deepthroat "<folder>"`). It lists what it would fix, asks first, and backs up the originals.

Running the tests: `python -m unittest discover -s tests` inside either folder. Changes: `CHANGELOG.md`.

MIT License, see `LICENSE`.
