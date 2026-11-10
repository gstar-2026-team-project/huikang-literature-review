# DreamerV3 / Dreamer 4

DreamerV3 and Dreamer 4 are world-model agents evaluated on simulator-stepped Minecraft and other domains.

| | |
|---|---|
| Year | 2023-25 |
| Links | [arXiv 2509.24527](https://arxiv.org/abs/2509.24527) |
| Demo | [project page](https://danijar.com/dreamer4/): prerecorded videos only. They show the agent mining diamonds in real Minecraft (plus 4 uncut YouTube runs), imagination-training rollouts with reward and value curves, and a human playing in the world model compared with Lucid and Oasis. Nothing on the page indicates real-time agent timing. Human-playable: no (a third-party reimplementation, [Open Dreamer](https://next-state.github.io/open-dreamer/), has a queued live world-model demo for humans). |
| Category | RL and decision model |
| Method | simulator-stepped |
| Evaluated on | Minecraft and others |
| Evaluation play mode | paused-live (agent evaluation) |
| Basis | paper (DreamerV3 v1) App.: MineRL, "36000 steps, corresponding to 30 minutes at the control frequency of 20Hz"; Dreamer 4 §4.1 follows the VPT protocol |

## Demo

- [project-page] [Dreamer 4 project page](https://danijar.com/dreamer4/) — Loaded the page, scrolled with screenshots and seeked 6 videos to 20% and 70%; every request was a recorded .mp4 from danijar.com/asset/dreamer4/, with no live inference. It has a teaser, an embedded YouTube video "Dreamer 4 / Diamonds from Offline Experience" described as "the agent being evaluated in the actual Minecraft environment" plus 4 linked "Diamond Challenge Uncut #1-#4" videos, "Imagination Training" clips (3 "Gather wood", 3 "Mine stone") with Reward and Value curve strips, "Human Interaction" clips of a human playing in the world model on 17 tasks compared with Lucid and Oasis, and 3 SOAR robotics counterfactual clips. Play-mode evidence: the agent clips are recorded offline evaluations in real Minecraft and nothing shows whether the clock kept running during policy computation; the page's "real-time interactive inference on a single GPU" refers to the world model with a human at the controls, not the agent. No latency or tick counters.
- [live-model] [Open Dreamer (third-party)](https://next-state.github.io/open-dreamer/) — Found by web search: a third-party JAX reimplementation of the Dreamer 4 world model by next-state (blog dated July 21, 2026, sponsored by Reactor), not the official work. It embeds an "OPEN DREAMER / LIVE DEMO / INTERACTIVE DEMO / GENERATED LIVE ON REACTOR" widget where a human plays in the generated Minecraft world after a "JOIN THE LINE" queue. Did not get into a session in headless Chrome; WASD had no visible effect, so a live session was not verified. No agent plays in it.

Visited 10 November 2026 in a headless browser.

Related: [MineRL](../environments/minerl.md); [VPT](vpt.md)
