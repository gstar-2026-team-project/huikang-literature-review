# MineDojo

MineDojo is a Minecraft environment with 20 Hz synchronous stepping.

| | |
|---|---|
| Year | 2016-22 |
| Play mode | paused-live (MineRL, MineDojo, MCU/MineStudio) + realtime-live (native Malmo) |
| Clock | STEP at 20 Hz |
| Observation | pixels (+ some state) |
| Action | mouse/keyboard |
| Players | 1 |
| Horizon | minutes to hours |
| Human reference | n/a |
| Open source | MIT; Malmo archived |
| Convertible to realtime-live | medium |
| Basis | MineDojo `bridge_env.py` (sync token) |
| Demo | [project page](https://minedojo.org/): 15 short looping MP4 clips of Minecraft tasks (Ender dragon fight, lava bucket, Nether portal, end city, and others) plus animated MineCLIP explainer videos. These are recordings; nothing runs live and nothing is human-playable. |

## Details

- **MineRL / MineDojo / MCU**: 20 Hz synchronous stepping; a wall-clock wrapper works only if the simulator sustains 20 Hz. Heavy and long-horizon.

## Demo

- [project page with videos] [minedojo.org](https://minedojo.org/): I rendered the page, played the clips and seeked them. It holds 15 autoplaying, looping MP4s served from `minedojo.org/videos/` (for example `defeat_ender_dragon.mp4` (20 s), `lava_bucket.mp4`, `build_light_up_enter_nether_portal.mp4`, `explore_an_end_city.mp4`, `grow_wheat.mp4`, `block_skeleton.mp4`). Their captions include "Fight against an Ender dragon", "Scoop a bucket of lava" and "Build a Nether Portal and enter it". At 0:12 the Ender dragon frame shows first-person Minecraft pixels with a bow. Two more clips explain MineCLIP. `mineclip_policy_learning.mp4` (14 s) shows a Simulator → Observation → Action loop, with "Stack the history RGB frames" fed to MineCLIP and the prompt "Shear sheep to obtain wool". `mineclip_paired_text.mp4` (9.7 s) pairs video with transcript text. Play-mode evidence (recording only): these are static video files with no live model calls, tick counter or step readout. The page does not say whether the task clips were played by humans or by agents, so they show what the environment looks like rather than how agents are timed. The page also links a Knowledge Base page with YouTube, Wiki and Reddit datasets, and docs at docs.minedojo.org.

Visited 10 November 2026 in a headless browser.

Related: [MineRL](minerl.md); [Malmo](malmo.md); [MCU / MineStudio](mcu-minestudio.md); [Voyager](voyager.md)
