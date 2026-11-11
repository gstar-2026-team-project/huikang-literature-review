# Malmo

Malmo is Microsoft's Minecraft platform; natively it runs at 20 Hz with observations coming in asynchronously.

![Malmo Python agent loop driving a Minecraft character](../assets/gifs/malmo.gif)

*A screen-capture clip from the Microsoft Research promo video: a Python agent loop (`sendCommand("move 1")`, `getWorldState()`) runs in the editor, the Minecraft window shows the character moving, and the console prints observations and rewards (a recording, not sped up). Source: [Microsoft Research, Project Malmo video (YouTube)](https://www.youtube.com/watch?v=KkVj_ddseO8).*

| | |
|---|---|
| Year | 2016-22 |
| Demo | [official video](https://www.youtube.com/watch?v=KkVj_ddseO8) (embedded on the [project page](https://www.microsoft.com/en-us/research/project/project-malmo/)): a 1:41 Microsoft Research promo of Malmo in Minecraft with B-roll of agent code and missions running. It is a recording, not a replay viewer, and nobody can play it; the project's [Videos tab](https://www.microsoft.com/en-us/research/project/project-malmo/videos/) lists talks and challenge videos. |
| Play mode | paused-live (MineRL, MineDojo, MCU/MineStudio) + realtime-live (native Malmo) |
| Clock | STEP at 20 Hz |
| Observation | pixels (+ some state) |
| Action | mouse/keyboard |
| Players | 1 |
| Horizon | minutes to hours |
| Human reference | n/a |
| Open source | MIT; Malmo archived |
| Convertible to realtime-live | medium |
| Basis | Malmo `Schemas/Mission.xsd` MsPerTick "default is 50ms per tick (20Hz)", `AgentHost.h` observations "coming in asynchronously" |

## Demo

- [official-video] [Project Malmo, Enabling AI technology that can collaborate with humans (YouTube)](https://www.youtube.com/watch?v=KkVj_ddseO8). I opened it on YouTube because the youtube-nocookie embed on the [project page](https://www.microsoft.com/en-us/research/project/project-malmo/) gave "Error 153" in headless Chrome. I then played it muted and sought to 15 s, 45 s and 90 s (duration 100.96 s). It is a Microsoft Research promo, "Project Malmo – Enabling AI technology that can collaborate with humans" (14K views, 9 years old). It shows a researcher at a laptop running a Minecraft mission projected on a wall, and close-ups of Python agent code (`agent_host.sendCommand("jump 1")`, `time.sleep(0.5)`, `world_state = agent_host.getWorldState()`, loops over `world_state.video_frames`, and a console running `python run_mission.py` that prints "rewards received"). Play-mode evidence (recording only): the code polls world state after sleeping for wall-clock time, which fits the asynchronous, realtime-live native Malmo loop. It shows no LLM agent and no tick counter.
- [video-list] [Project Malmo Videos tab](https://www.microsoft.com/en-us/research/project/project-malmo/videos/). I rendered the list. It has talks and challenge videos, including "Tech Showcase: Project Malmo – Experimentation Platform for the Next Generation of AI Research" (2:28, July 17, 2017), "The Malmo Collaborative AI Challenge" (17:01) and "MineRL Competition 2019" (1:06). There is no replay viewer, playable page or live demo. The GitHub repo (archived; homepage field points to the project page) has no media in its README.

Visited 10 November 2026 in a headless browser.

Related: [MineRL](minerl.md); [MineDojo](minedojo.md); [MCU / MineStudio](mcu-minestudio.md)
