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
| Digi doppler | When TIME moves, Digi glides to the new time with a pitch bend (like tape) instead of the stock crossfade between overlapping delay lines. Big jumps bend in semitone steps, up to two octaves. Required by Live reverse. | None |
| Tape pickup speed | Tape follows TIME changes about 5× faster (less lag). | None |
| BBD light mode | BBD internal filter cap raised from 4.2 kHz to 12 kHz. | None |
| Tape bright (extra) | Removes two built-in Tape tone shelves (about +3 to +5.5 dB above 1 kHz). | None |
| **Seal Beads (new)** | A granular mode in the Digi slot, inspired by Mutable Instruments Beads. Heavily modified, not a 1-to-1 port (see below). | With MODEL on DIGI, hold **FREEZE (ALT)** + **DELAY SYNC** for about 1 s to enter or leave. **TAP** glows teal while it's on. |

Mods can be mixed freely, with two rules: Live reverse needs Digi doppler (Digi reverse follows TIME through the doppler engine), and Seal Beads needs Live reverse. Reverse, character and doppler share one engine, which is added once.

## Seal Beads

Seal Beads is a **heavily modified Beads**. Don't think of it as a 1-to-1 port of the Mutable Instruments module.
- **Built for the Sealegs:** it deliberately departs from the original to fit the Sealegs architecture, panel and CPU budget.
- **Tuned by ear:** it was tuned to work for both rhythmic and melodic material, from clocked drum chops with swing and ghost hits to long, round, overlapping clouds.
- **Digi only while it runs:** it replaces Digi only while you're in it. Tape, BBD and Digi are unchanged whenever it's off.

| Control | Free running | DELAY SYNC on (clocked) |
| --- | --- | --- |
| Enter / exit | With MODEL on DIGI, hold FREEZE (ALT) + DELAY SYNC for about 1 s. TAP glows teal while Seal Beads is on. The same gesture, or moving MODEL off DIGI, returns to Digi as you left it. | |
| MOD DEPTH | Density: how often grains start. Bottom = none, up to about 40 per second | Grains per pulse: off, 1/8, 1/4, 1/2, 1, 2, 3, 4, 6, 8 |
| WIDTH | Grain size: 20 ms to 8 s | 1/16 to 16 pulses |
| MOD knob | Overlap: each grain runs on into the next ones (up to 3 more), so grains blend while the onsets keep their timing | Same, on the grid |
| COLOR | Grain roundness. Top = hard square gates, noon = Beads-style bell, bottom = extra-round, very soft onsets | Same |
| NOISE | Scatter: even spacing to random gaps, with grains drawn from across the TIME window | Groove: up to noon, swing up to a full triplet shuffle; past noon, late offsets and ghost hits |
| TIME | How far back grains read: 0 to 1, 4 or 16 s (TIME RANGE) | 0 to 1, 4 or 16 pulses |
| MOD RATE | Grain pitch, two octaves either way, lingering on musical intervals | Same |
| FEEDBACK | Feedback through the grain buffer. ALT + DELAY SYNC swaps left and right in the loop | Same |
| HPF / LPF | Filters on the grains and their feedback. The slider ends bypass them | Same |
| FOG | Reverb amount; ALT + FOG sets decay. The FOG/DRIVE switch places it: IN (before the grains), DLY (grains only) or MIX (everything) | Same |
| DRIVE / MIX | Matched to the stock Sealegs drive, input trim (ALT + DRIVE), drive position and equal-power MIX | Same |
| FREEZE | Tap: reverse grains (FREEZE lights magenta). ALT + MOD SYNC: freeze the grain buffer (blue). The Seal Eggs FREEZE swap also swaps these two | Same |
| TAP | Tap tempo when no clock is running. Glows teal while Seal Beads is on | |
| DELAY SYNC | | Locks grains to CLK IN or tap tempo. The tempo is measured from the clock itself and kept if the clock stops, so grains never stall. Hold 1 s to clear the grain buffer |
| MOD SYNC | | Triplet grid (1.5 times the grains per pulse) |
| STEREO CONFIG | PONG: inputs summed into the grains, wide spread. T:W: stereo with random panning. L/R: stereo, no random panning | Same |
| ALT held | FREEZE light shows CPU load (green, yellow, orange, red). Under sustained overload, grains are thinned first and FOG is dropped before the panel can lock up | Same |
| MOD OUT, MOD lights | Still the stock LFO | Same |

Seal Beads contains code from Mutable Instruments Beads and stmlib by Emilie Gillet, used under the MIT licence ([LICENSE-beads.txt](LICENSE-beads.txt)). It's an independent derivative and isn't affiliated with or endorsed by Mutable Instruments.

## Safety checks

- The input must match the SHA-256 of official 1.3.5.0 (`ca90eb8f…adcf`). Anything else is refused.
- The regions where new code goes must be empty in the input.
- The output is checked against the expected SHA-256 for that exact combination (all 64 valid combinations are listed in `mods.js`). If it doesn't match, the download is blocked.

## Known differences

- Digi doppler adds about 1 ms (one audio block) to Digi's delay time. Without doppler, Digi is bit-identical to stock whenever reverse and character are off; Tape and BBD always are.
- With reverse installed, the short ALT+TAP (AUX CV destination) action fires when TAP is released, not when it is pressed.
- Seal Beads adds a CPU load meter that runs in every model (it only measures; audio is unchanged). Inside Seal Beads, the TAP light shows the teal glow instead of the tempo blink.

## Verification

The patches were verified in an ARM Cortex-M7 emulator running the firmware's own DSP code: bit-exact comparisons between builds, randomised sessions (model switches, reverse, character, time and feedback changes, delay-memory clears) and button-gesture tests. Reverse, character and the stability fixes were also tested on hardware. Newer combinations (reverse without character, character or doppler on their own, character with stock Digi) have so far been verified in emulation only.

Seal Beads was developed and played on hardware with the full reverse + character build. In the emulator, every Seal Beads combination was checked: Tape, BBD and Digi are bit-identical to the same build without Seal Beads while it's off, and Seal Beads itself behaves identically whichever other mods are installed. Its own test suite (clock handling, controls, levels, FOG stress and CPU load) passes on the published build.

## Rollback

Flash your original `Sealegs.1.3.5.0.bin` using the official update procedure.

## Files

- `index.html`: the flasher (no build step, no dependencies)
- `mods.js`: patch data (added code and changed constants only) plus reference hashes
- `assets/`: the coin sprites
- `LICENSE-beads.txt`: the MIT licence for the Beads and stmlib code inside Seal Beads

## Disclaimer

Sealegs is designed and made by Intellijel. Seal Eggs is an unofficial, community modification for education and preservation. It isn't affiliated with, endorsed by or supported by Intellijel. Please don't contact Intellijel for help with modified firmware; flash the official firmware first if you need support. Use entirely at your own risk; flashing modified firmware may affect your warranty.
