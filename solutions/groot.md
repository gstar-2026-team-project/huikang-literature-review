# GROOT

GROOT is a Minecraft model listed with the VPT line on the 20 Hz native interface with a synchronous simulator.

| | |
|---|---|
| Year | 2022-25 |
| Category | RL and decision model |
| Method | 20 Hz native interface; synchronous simulator |
| Evaluated on | Minecraft |
| Evaluation play mode | paused-live |
| Basis | paper (VPT) App. C: client and server "run in the same thread ... slower or faster than real time"; code: MineRL `_multiagent.py` synchronous token |
| Demo | [Project page](https://craftjarvis.github.io/GROOT/): a 40 s autoplaying banner video. It is a montage of six recorded Minecraft agent clips with task captions (for example "CARVE PUMPKINS", "COLLECT DIRT", "MINE HORIZONTALLY"), plus static result figures. It is a recording: there is no live model, replay viewer or human-playable page, and nothing on the page shows timing. |

## Demo

- [project page / video] [GROOT project page](https://craftjarvis.github.io/GROOT/) (homepage of [CraftJarvis/GROOT](https://github.com/CraftJarvis/GROOT)): Rendered the page, dumped its text, played the only video (`static/videos/banner_video.mp4`: 1920x1080, 40.5 s, autoplay and loop) and took screenshots at 3, 15 and 35 s. The video is a 3x2 grid of first-person Minecraft gameplay clips around a GROOT logo, captioned "CARVE PUMPKINS", "COLLECT DIRT", "DYE THE SHEEP THEN SHEAR IT", "USE A BOW", "MINE HORIZONTALLY", "SET A FOREST ON FIRE", "COOK FOOD", "COLLECT SEAGRASS", "TAKE THE TREASURE FROM THE CHEST", "BUILD A PILLAR" and "USE A SHIELD TO WARD OFF ZOMBIES". The rest of the page is the abstract, an architecture figure and static result figures (t-SNE goal space, diamond-task timelines, SkillForge Elo). There are no iframes, canvases or GIFs. Play-mode evidence: it is an edited recording with no clock, tick or latency overlay, so it says nothing about live versus paused play.

Visited 10 November 2026 in a headless browser.

Related: [VPT](vpt.md); [MineRL](../environments/minerl.md)
