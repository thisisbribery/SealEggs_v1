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
| **Seal Microloops (new)** | A micro-loop mode behind BBD: a few short loops of what you just played repeat, change speed, get rearranged or hold into drones. Three modes (Octaves, Shuffle, Drone), four variations each. Shares the Seal Beads shell. | With MODEL on BBD, hold **FREEZE (ALT)** + **DELAY SYNC** for about 1 s to enter or leave. **TAP** glows orange while it's on. |
| **Seal Beads V2 (new)** | A granular mode in the Digi slot, inspired by Mutable Instruments Beads. Heavily modified, not a 1-to-1 port (see below). | With MODEL on DIGI, hold **FREEZE (ALT)** + **DELAY SYNC** for about 1 s to enter or leave. **TAP** glows teal while it's on. |

Mods can be mixed freely, with three rules: Live reverse needs Digi doppler (Digi reverse follows TIME through the doppler engine), Seal Beads needs Live reverse, and Seal Microloops needs Seal Beads (they share one engine shell). Reverse, character and doppler share one engine, which is added once.

## Seal Microloops

Seal Microloops is a micro-looper hiding behind BBD. A few short loops of what you just played repeat, change speed, get rearranged into new rhythms or hold into drones, so you still hear your playing, rebuilt into intervals and patterns. It runs in the same shell as Seal Beads, so DRIVE, MIX, FOG, FEEDBACK, the filters, stereo and the clock behave the same. It's original code: an homage to boutique micro-loop pedals, not a port of any of them.

**TIME RANGE** picks the mode, **MOD RATE** picks one of four variations (four zones, bottom to top), and **MOD DEPTH** sets how much each variation does.

| Mode | What it does |
| --- | --- |
| **Octaves** (LONG) | Up to four loops of different lengths (1×, 2×, ½× and 1.5× TIME), each at an octave speed. The lengths never line up, so the loops drift against each other. MOD DEPTH brings in loops 2 to 4. |
| **Shuffle** (MED) | The last few seconds are cut into slices and replayed as a shuffled 8-step pattern. Best on drums with DELAY SYNC on. WIDTH sets how many times a pattern plays before it takes fresh audio and reshuffles. |
| **Drone** (SHORT) | Two loops repeat a short sample until it sustains. Stop playing and the drone rings on, fading over a time set by WIDTH (never at the top). Play again and it takes the new sound. New samples are only taken near the peaks of your playing, never from a gap between hits. |

| Mode | A | B | C | D |
| --- | --- | --- | --- | --- |
| Octaves | Normal + an octave up | Normal + an octave down | Everything an octave up | An octave down to two octaves up (½, 1, 2, 4×) |
| Shuffle | A random low-pass per step | Some steps at half speed, an octave down; a soft pad joins at the very top | Up to three overlapping layers, each step a resonant filter sweep | A double-time layer, then a bit-crushed sub-octave layer |
| Drone | Loop length breathes, down to a quarter and back over 10 s (16 pulses clocked) | Sub-octave drone under a resonant low-pass sweeping 8 kHz to 125 Hz and back over 16 s (32 pulses) | Each sample rings through a resonant band (300 Hz to 2.4 kHz), a new band with every new sample | Loop length follows your playing: harder tightens, softer opens |

| Control | Seal Microloops |
| --- | --- |
| Enter / exit | With MODEL on BBD, hold FREEZE (ALT) + DELAY SYNC for about 1 s. TAP glows orange while it's on. The same gesture, or moving MODEL off BBD, returns to BBD as you left it. |
| TIME RANGE | Mode: LONG = Octaves, MED = Shuffle, SHORT = Drone |
| MOD RATE | Variation A, B, C or D |
| MOD DEPTH | Activity: how much the variation does (loops, layers, filter depth, crush, breathing, sweep) |
| TIME | Loop or step length: 25 ms to 2 s. With DELAY SYNC on: 1/16 to 2 pulses |
| WIDTH | Repeats: how many times a loop plays before it grabs fresh audio (1 to 64). In Drone it also sets how long the drone rings on after you stop: about 0.4 s to 20 s, forever at the very top |
| COLOR | Shape of each loop: top = hard edges (stutter), noon = a bell, bottom = extra round |
| MOD knob | Overlap: how much each pass crossfades into the next. 0 = hard restarts, full = seamless |
| NOISE | Scatter: loops grab audio from further back at random. In Shuffle: rests, doubled steps and reversed steps |
| FREEZE | Tap: loops play reversed. ALT + MOD SYNC: hold (stops recording, so the loops keep cycling what you held) |
| FEEDBACK | The loops are recorded back in. ALT + DELAY SYNC swaps left and right in the loop |
| HPF / LPF | Filters on the loops and their feedback. The slider ends bypass them |
| FOG | Reverb, as in Seal Beads. IN smears the audio before it's looped, DLY puts it on the loops, MIX on everything |
| DRIVE / MIX | Matched to the stock Sealegs drive, input trim, drive position and equal-power MIX |
| DELAY SYNC | Locks loop lengths, Shuffle steps and the Drone breathing and sweep to CLK IN or tap tempo. Hold 1 s to clear the loop memory |
| MOD SYNC | Triplets: lengths and steps × 2/3 |
| TAP | Tap tempo when no clock is running. Breathes orange while Seal Microloops is on |
| STEREO CONFIG | PONG and T:W spread the loops across the stereo field. L/R keeps them in place |
| ALT held | FREEZE light shows CPU load (green, yellow, orange, red). Under sustained overload, loops are thinned first |

Seal Microloops is original code. It contains no code or data from any commercial product and isn't affiliated with or endorsed by any pedal maker.

## Seal Beads V2

Seal Beads is a **heavily modified Beads**. Don't think of it as a 1-to-1 port of the Mutable Instruments module.

**New in V2:** a softer COLOR (shape) with a new buttery end, smoother Overlap, and Scatter is now Spray.

- **Built for the Sealegs:** it deliberately departs from the original to fit the Sealegs architecture, panel and CPU budget.
- **Tuned by ear:** it was tuned to work for both rhythmic and melodic material, from clocked drum chops and reshuffled slices to long, buttery, overlapping clouds.
- **Digi only while it runs:** it replaces Digi only while you're in it. Tape, BBD and Digi are unchanged whenever it's off.

| Control | Free running | DELAY SYNC on (clocked) |
| --- | --- | --- |
| Enter / exit | With MODEL on DIGI, hold FREEZE (ALT) + DELAY SYNC for about 1 s. TAP glows teal while Seal Beads is on. The same gesture, or moving MODEL off DIGI, returns to Digi as you left it. | |
| MOD DEPTH | Density: how often grains start. Bottom = none, up to about 40 per second | Grains per pulse: off, 1/8, 1/4, 1/2, 1, 2, 3, 4, 6, 8 |
| WIDTH | Grain size: 20 ms to 8 s | 1/16 to 16 pulses |
| MOD knob | Overlap: each grain runs on into the next ones (up to 3 more), so grains blend smoothly while the onsets keep their timing | Same, on the grid |
| COLOR | Grain shape. Top = hard square gates, noon = Beads-style bell, a quarter up = very round, bottom = buttery: soft-edged grains that melt into one smooth cloud | Same |
| NOISE | Spray: each grain starts from a random spot around TIME, reaching the whole TIME RANGE at full, and grain starts wobble in time without leaving gaps. Grains stay centred in the stereo field | Spray on the grid: grains read from other slices, and the timing stays locked to the clock |
| TIME | How far back grains read: 0 to 1, 4 or 16 s (TIME RANGE). Squared, so the lower half covers the first quarter | 0 to 1, 4 or 16 pulses |
| MOD RATE | Grain pitch, two octaves either way, lingering on musical intervals | Same |
| FEEDBACK | Feedback through the grain buffer. ALT + DELAY SYNC swaps left and right in the loop | Same |
| HPF / LPF | Filters on the grains and their feedback. The slider ends bypass them | Same |
| FOG | Reverb amount; ALT + FOG sets decay. The FOG/DRIVE switch places it: IN (before the grains), DLY (grains only) or MIX (everything) | Same |
| DRIVE / MIX | Matched to the stock Sealegs drive, input trim (ALT + DRIVE), drive position and equal-power MIX | Same |
| FREEZE | Tap: reverse grains (FREEZE lights magenta). ALT + MOD SYNC: freeze the grain buffer (blue). The Seal Eggs FREEZE swap also swaps these two | Same |
| TAP | Tap tempo when no clock is running. Breathes teal while Seal Beads is on; hold ALT to see the usual AUX CV destination blink | |
| DELAY SYNC | | Locks grains to CLK IN or tap tempo. The tempo is measured from the clock itself and kept if the clock stops, so grains never stall. Hold 1 s to clear the grain buffer |
| MOD SYNC | | Triplet grid (1.5 times the grains per pulse) |
| STEREO CONFIG | PONG: inputs summed into the grains, wide spread. T:W: stereo with random panning. L/R: stereo, no random panning | Same |
| ALT held | FREEZE light shows CPU load (green, yellow, orange, red). Under sustained overload, grains are thinned first and FOG is dropped before the panel can lock up | Same |
| MOD OUT, MOD lights | Still the stock LFO | Same |

Seal Beads contains code from Mutable Instruments Beads and stmlib by Emilie Gillet, used under the MIT licence ([LICENSE-beads.txt](LICENSE-beads.txt)). It's an independent derivative and isn't affiliated with or endorsed by Mutable Instruments.

## Safety checks

- The input must match the SHA-256 of official 1.3.5.0 (`ca90eb8f…adcf`). Anything else is refused.
- The regions where new code goes must be empty in the input.
- The output is checked against the expected SHA-256 for that exact combination (all 80 valid combinations are listed in `mods.js`). If it doesn't match, the download is blocked.

## Known differences

- Digi doppler adds about 1 ms (one audio block) to Digi's delay time. Without doppler, Digi is bit-identical to stock whenever reverse and character are off; Tape and BBD always are.
- With reverse installed, the short ALT+TAP (AUX CV destination) action fires when TAP is released, not when it is pressed.
- Seal Beads adds a CPU load meter that runs in every model (it only measures; audio is unchanged). Inside Seal Beads, the TAP light breathes teal instead of its usual colour (holding ALT still shows the AUX CV destination blink); inside Seal Microloops it breathes orange.

## Verification

The patches were verified in an ARM Cortex-M7 emulator running the firmware's own DSP code: bit-exact comparisons between builds, randomised sessions (model switches, reverse, character, time and feedback changes, delay-memory clears) and button-gesture tests. Reverse, character and the stability fixes were also tested on hardware. Newer combinations (reverse without character, character or doppler on their own, character with stock Digi) have so far been verified in emulation only.

Seal Beads was developed and played on hardware with the full reverse + character build, and V2 has been played on hardware. In the emulator, every Seal Beads combination was checked: Tape, BBD and Digi are bit-identical to the same build without Seal Beads while it's off, and Seal Beads itself behaves identically whichever other mods are installed. Its own test suite (clock handling, controls, levels, FOG stress and CPU load) passes on the published build.

Seal Microloops was developed and played on hardware with the full build plus Seal Beads. Its latest version (a fix for Shuffle stalling while TIME or WIDTH moved) has been verified in the emulator: the three modes and their variations, levels, CPU load, and a stress test of fast control moves. Every Seal Microloops combination was checked: Tape, BBD and Digi are bit-identical to the same build without it while it's off, Seal Beads is unchanged, and Seal Microloops behaves identically whichever other mods are installed.

## Rollback

Flash your original `Sealegs.1.3.5.0.bin` using the official update procedure.

## Files

- `index.html`: the flasher (no build step, no dependencies)
- `mods.js`: patch data (added code and changed constants only) plus reference hashes
- `assets/`: the coin sprites
- `LICENSE-beads.txt`: the MIT licence for the Beads and stmlib code inside Seal Beads

## Disclaimer

Sealegs is designed and made by Intellijel. Seal Eggs is an unofficial, community modification for education and preservation. It isn't affiliated with, endorsed by or supported by Intellijel. Please don't contact Intellijel for help with modified firmware; flash the official firmware first if you need support. Use entirely at your own risk; flashing modified firmware may affect your warranty.
