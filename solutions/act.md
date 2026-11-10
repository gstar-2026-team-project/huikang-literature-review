# ACT (action chunking)

ACT predicts many actions per inference and executes them open-loop.

| | |
|---|---|
| Category | RL and decision model (robotics latency method) |
| Demo | [ACT / ALOHA project page](https://tonyzhaozh.github.io/aloha/) (Zhao, Kumar, Levine, Finn, RSS 2023): official project page with recorded videos of ACT policies running on the ALOHA bimanual robot in real time, plus reactiveness, distractor-robustness and policy-input camera clips. Recordings only; nothing playable or live. |

## Details

- **Action chunking** (ACT, pi0): predict many actions per inference and execute open-loop.

## Demo

- [project-page videos] [Learning Fine-Grained Bimanual Manipulation with Low-Cost Hardware](https://tonyzhaozh.github.io/aloha/) — Opened the page, played `teleop_all.mp4` (106.7 s, human teleoperation) and `slot_battery.mp4` (23.9 s), seeked to 60% and took a screenshot. The frame is captioned "SLOT BATTERY / REAL-TIME POLICY ROLLOUT". The page says "The videos below show real-time rollouts of ACT policies, imitating from 50 demonstrations for each task. The ACT policy directly predicts joint positions at 50Hz with a fixed chunk size of 90", with episodes of 600-1000 steps and 96%, 84%, 64% and 92% success on the four tasks (slot battery, open lid, prep tape, put on shoe). The carousels "Reactiveness" (`reactive_cup.mov`, `reactive_battery.mov`, `reactive_cup_fail.mov`) and "Robustness" (`distractor_battery.mov`, `distractor_tape.mov`) show the policy recovering from human disturbances and failing in some clips. "Observations during policy execution" shows the four 480x640 camera streams the policy takes as input. Play-mode evidence: these are recorded real-robot rollouts against the physical real-time clock (50 Hz control). There is no LLM and no game.

Visited 10 November 2026 in a headless browser.

Related: [pi0](pi0.md); [Real-Time Chunking](real-time-chunking.md)
