# Seal Eggs firmware flasher

> **Unofficial, modified firmware. Use it entirely at your own risk.** The author accepts no responsibility for any damage, malfunction, lost settings or warranty issues that may result.

Mods by **Bribery** ([@thisisbribery](https://www.instagram.com/thisisbribery/)).

A browser tool that adds community mods to **your own copy** of the official Sealegs 1.3.5.0 firmware.

**[Open the flasher](https://thisisbribery.github.io/SealEggs_v1/)**

No firmware is hosted here. You load the official `Sealegs.1.3.5.0.bin`, choose mods, and the page writes a modified copy in your browser. Nothing is uploaded.

## Mods

| Mod | What it does | Controls |
| --- | --- | --- |
| Live reverse delay | Reverse playback in Tape, BBD and Digi, with recording and feedback still running. Includes the click and overload fixes. | Tap **FREEZE** to toggle reverse. Hold **FREEZE (ALT)** + hold **TAP** for about 1 s to swap FREEZE between reverse and native Freeze. |
| Secondary character on NOISE | NOISE becomes a second character control: Tape grunge, BBD chip decay, Digi data corruption. | Hold **FREEZE (ALT)** + hold **MOD SYNC** for about 1 s. Remembered across power cycles. |
| Tape pickup speed | Tape follows TIME changes about 5× faster (less lag). | None |
| BBD light mode | BBD internal filter cap raised from 4.2 kHz to 12 kHz. | None |
| Tape bright (extra) | Removes two built-in Tape tone shelves (about +3 to +5.5 dB above 1 kHz). | None |

Every mod can be used on its own. Reverse and secondary character share one engine, which is added once if either is chosen.

## Safety checks

- The input must match the SHA-256 of official 1.3.5.0 (`ca90eb8f…adcf`). Anything else is refused.
- The regions where new code goes must be empty in the input.
- The output is checked against the expected SHA-256 for that exact combination (all 32 combinations are listed in `mods.js`). If it doesn't match, the download is blocked.

## Known differences

- With reverse or character installed, Digi's forward delay runs about 1 ms (one audio block) later than stock. Tape and BBD are bit-identical to stock whenever reverse and character are off.
- With reverse installed, the short ALT+TAP (AUX CV destination) action fires when TAP is released, not when it is pressed.

## Verification

The patches were verified in an ARM Cortex-M7 emulator running the firmware's own DSP code: bit-exact comparisons between builds, randomised sessions (model switches, reverse, character, time and feedback changes, delay-memory clears) and button-gesture tests. Reverse, character and the stability fixes were also tested on hardware. Reverse-only and character-only builds have so far been verified in emulation only.

## Rollback

Flash your original `Sealegs.1.3.5.0.bin` using the official update procedure.

## Files

- `index.html`: the flasher (no build step, no dependencies)
- `mods.js`: patch data (added code and changed constants only) plus reference hashes
- `assets/`: the coin sprites

## Disclaimer

Sealegs is designed and made by Intellijel. Seal Eggs is an unofficial, community modification for education and preservation. It isn't affiliated with, endorsed by or supported by Intellijel. Please don't contact Intellijel for help with modified firmware; flash the official firmware first if you need support. Use entirely at your own risk; flashing modified firmware may affect your warranty.
