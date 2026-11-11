# NetHack LE

The NetHack Learning Environment is a turn-based roguelike with a step loop.

![Agent exploring a NetHack dungeon in NLE](../assets/gifs/nethack-le.gif)

*Recording from the NLE README of an RL agent exploring the NetHack terminal map, from the intro text to dungeon level 3 (turn counter T:1 to T:152), sped up 4x. Source: [NLE README example GIF](https://github.com/NetHack-LE/nle/raw/main/dat/nle/example_run.gif).*

| | |
|---|---|
| Year | Jun 2020 |
| Links | [NLE](https://github.com/heiner/nle) |
| Demo | [README example GIF](https://github.com/NetHack-LE/nle/raw/main/dat/nle/example_run.gif): official recording, captioned "Example of an agent running on NLE", of an agent exploring the NetHack terminal map, with the in-game turn counter advancing. Not human-playable in the browser, no replay viewer, and no LLM shown. |
| Play mode | paused-live, turn-based |
| Clock | none |
| Observation | text |
| Action | text |
| Players | 1 |
| Horizon | long |
| Human reference | n/a |
| Open source | open |
| Convertible to realtime-live | not meaningful |
| Basis | NLE README step loop (turn-based game) |

## Details

- In the turn-based or untimed contrast set (paused-live, turn- or step-based). None of the contrast set has a native clock; a deadline could be imposed but the games do not reward reflexes. They are useful as the "same model, no clock" control.

## Demo

- [video] [NLE README example GIF](https://github.com/NetHack-LE/nle/raw/main/dat/nle/example_run.gif) — opened the repo README (github.com/heiner/nle redirects to github.com/NetHack-LE/nle; no homepage field) and screenshotted the looping 770x434 GIF captioned "Example of an agent running on NLE" at 3 s intervals; it shows an agent, "Agent76001 the Candidate", exploring the tty map, going from "Dlvl:1 ... T:40" to "Dlvl:2 ... T:65" with the message "The door resists!". Play-mode evidence (recording): progress is counted in game turns (T:), not wall-clock time, which fits the turn-based step loop. It is an RL agent, not an LLM. The README also links a Weights & Biases interview video on YouTube, which is not a gameplay demo.

Visited 10 November 2026 in a headless browser.

Related: [TextWorld](textworld.md); [Jericho](jericho.md); [BALROG](balrog.md)
