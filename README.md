# Wife's Bedroom mod converters

Two converters that move character and room mods between Wife's Bedroom v1.5 and the modded games (Deeproom 4.0.3 Kiwami, ModRoom v3.3). Each folder works on its own; you only need Python (free from python.org; tick "Add Python to PATH" when installing).

| You have mods for... | You want to play them in... | Use |
|---|---|---|
| ModRoom, Deeproom or FutasRoom | Wife's Bedroom v1.5 | `Modded_to_WB_1.5/Convert_to_WB_1.5.bat` |
| Wife's Bedroom v1.5 | Deeproom 4.0.3 or ModRoom v3.3 | `WB_1.5_to_Modded/Convert_from_WB_1.5.bat` |

Drag a mod folder or `.zip` onto the `.bat`, press Enter at each question, and copy what appears in that converter's `output/` folder into your game. Each folder's `README.md` has the details.

**Partners sitting too high in Deeproom's deepthroat pose?** Packs converted for Deeproom before 2026-11-17 can carry a wrong height. Drag your Deeproom `custom_stuff/custom_wives` folder onto `WB_1.5_to_Modded/Repair_Deepthroat.bat`. It lists what it would fix, asks first, and backs up the originals.

Running the tests: `python -m unittest discover -s tests` inside either folder. Changes: `CHANGELOG.md`.

MIT License, see `LICENSE`.
