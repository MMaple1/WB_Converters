# Changelog

Each converter keeps its full history in its own `core/CHANGELOG.md`. Both share the same conversion core (`core/wbconv.py`, identical in both folders).

## 1.2.1 - 2026-11-18

First release of both converters together in one repository.

- **Deeproom partners' deepthroat height.** Converting for Deeproom no longer adds an invented `[deepthroat] origin_y="150"` (it drew the sprite 66 px too high). A real v1.5 `deepthroat_origin_y` becomes Deeproom's value minus 70, and Deeproom to v1.5 adds 70.
- **`WB_1.5_to_Modded/Repair_Deepthroat.bat`** fixes partners converted with an older version. It lists first, asks, only touches blocks the old converter wrote, and backs up the originals.
- PNGs with a transparent colour key (RGB or grayscale `tRNS`) keep their transparency when strips are padded or cropped.
- Descriptors saved in latin-1 no longer crash the conversion when the pack name has characters latin-1 cannot hold.
- The generated stand-in cowgirl strip for ModRoom uses the pack's own frame width (high-res packs) and the right frame count.
- Launchers: paths containing `!` work, an `input/` folder holding only `.gitkeep` counts as empty, and the converter's exit code is passed on.
