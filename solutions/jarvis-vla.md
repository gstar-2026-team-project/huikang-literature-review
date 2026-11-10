# JARVIS-VLA

JARVIS-VLA is a Minecraft model listed with the VPT line on the 20 Hz native interface with a synchronous simulator.

| | |
|---|---|
| Year | 2022-25 |
| Category | RL and decision model |
| Method | 20 Hz native interface; synchronous simulator |
| Evaluated on | Minecraft |
| Evaluation play mode | paused-live |
| Basis | paper (VPT) App. C: client and server "run in the same thread ... slower or faster than real time"; code: MineRL `_multiagent.py` synchronous token |
| Demo | [project page](https://craftjarvis.github.io/JarvisVLA/): official project page with about 70 recorded MP4 rollouts of the model doing Minecraft tasks from instructions (cook, harvest, kill, mine, combat, smelt, craft), two reflection clips, two long rollouts and six failure cases. These are recordings, not a live run, and nothing on the page can be played by a human. |

## Demo

- [project-videos] [JARVIS-VLA project page](https://craftjarvis.github.io/JarvisVLA/): I rendered the page, listed its 69 `<video>` elements (all static files under `/JarvisVLA/videos/...`, none autoplaying) and played and seeked several of them. Short task clips are 640x360 and run about 2-15 s, for example "Smelt iron ingots from iron ores" `highlight/iron_ingot.mp4` (10.2 s) and "Craft iron swords with iron ingots" `highlight/iron_sword.mp4` (4.4 s). Each frame has a task label overlay such as "craft_item:iron_ingot" or "kill_entity:sheep", and the GUI clips show the agent moving the cursor in furnace and crafting windows. The "Long rollout" section has `long_video/mining.mp4` (333.3 s; the frame at 200 s has the label "mine_block:diamond_ore" and shows the agent digging down with a pickaxe) and "survive in night" `long_video/survive_night.mp4` (66.7 s; the frame at 40 s has the label "kill_entity:zombie" at night). "Failure cases analysis" has six clips such as `failed/fail_creeper.mp4` (33.3 s). One clip (`craft_on_table/spruce_boat.mp4`) did not load, and the console showed one 404. Play-mode evidence: these are recorded videos. They have no wall-clock, tick or latency overlay, and no live model calls were made, so they cannot show whether the agent kept up with a running clock. The long clips' round durations (33.3, 66.7 and 333.3 s) suggest a fixed number of frames was recorded, not wall-clock capture. That fits the paused-live label, but it is an inference.

Visited 10 November 2026 in a headless browser.

Related: [VPT](vpt.md); [MineRL](../environments/minerl.md)
