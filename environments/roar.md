# ROAR

ROAR is a Unity arena shooter run as a "Multi-Agent Asynchronous Gym" in which the environment advances every fixed interval without waiting for inference.

| | |
|---|---|
| Year | 2026 |
| Authors / org | Wang, Zhao, Yu, Zhou, Ma, Liu, Zhang, Chu, Koh, Ushaw, Davison (Newcastle University, University of Auckland, CTW Inc.) |
| Links | [arXiv 2610.24282](https://arxiv.org/abs/2610.24282), code [tb6147877/ROAR](https://github.com/tb6147877/ROAR) (MIT, prebuilt Unity executables) |
| Demo | [GitHub README](https://github.com/tb6147877/ROAR): recorded GIFs of Gemini-3.1 Pro and GPT-5.4 playing, shown turn-based vs real-time (40 ms tick). In the real-time clip the in-game countdown keeps running while the models think (04:59 to 01:55 over 153 s), and the agents get hit by the turret or die in the toxic zone. In the turn-based clips the game waits. Downloadable Unity builds (Linux/Windows) run locally; human-playable: yes (local executable only, not in the browser). |
| Play mode | realtime-live + paused-live |
| Clock | WALL: env thread steps every 40 ms or 250 ms of wall-clock time and never waits (code read); turn-based control |
| Observation | RGB, depth, JSON text, audio |
| Action | 7-dim move/aim/fire |
| Players | 1 or 4 |
| Horizon | 5 min |
| Human reference | none (rule bot) |
| Open source | MIT, Unity builds |
| Convertible to realtime-live | n/a |
| Basis | code: `roar_evaluation/async_env_runner.py` (env thread sleeps to `perf_counter` deadline, consumes action buffer, `env.step`); turn-based: `roar_benchmark.py` `start_run_turn_based` |

## Details

- Wang, Zhao, Yu, Zhou, Ma, Liu, Zhang, Chu, Koh, Ushaw, Davison (Newcastle University, University of Auckland, CTW Inc.). [arXiv 2610.24282](https://arxiv.org/abs/2610.24282); code [tb6147877/ROAR](https://github.com/tb6147877/ROAR) (MIT, prebuilt Unity executables).
- Tasks: Unity arena shooter with four levels: co-op (4 agents), competitive last-survivor, 2v2, and a basic single-agent level.
- Play mode: "Multi-Agent Asynchronous Gym". The environment and each agent run in separate threads; the environment advances every fixed interval without waiting for inference; a no-op applies if no fresh action is in the buffer. Tested at 250 ms and 40 ms ticks, plus a turn-based baseline. Code read (`roar_evaluation/async_env_runner.py`): the environment thread sleeps until `next_time` on `time.perf_counter()`, reads each agent's action buffer, calls `env.step`, then adds `step_interval` (default 0.04 s) to `next_time`. An action is consumed once; if none has been written since the last tick the default action is used. So the tick is enforced against the wall clock and the environment never waits for a model. The turn-based baseline is a plain `env.step(action)` loop (`roar_benchmark.py`, `start_run_turn_based`).
- Observation: RGB 512x512, depth, JSON text state, flat vector, and audio (sound-source list or raw mix). Action: 7-dim (move, yaw, pitch, fire, jump, minimap). 5-minute episodes. Score in 0-1. No human baseline; a heuristic bot and a random policy are the references.
- Results (turn-based / 250 ms / 40 ms): Gemini-3.1 Pro 0.87 / 0.44 / 0.34 (P50 latency 3.2 s); GPT-5.4 0.47 / 0.26 / 0.19; Gemma-4 31B 0.39 / 0.33 / 0.19; small local models (65-97 ms latency) about 0.07-0.10; heuristic bot about 0.33. Under realtime the best model is level with a rule bot. ReAct-style scaffolds help turn-based play but not realtime.
- Shortlist rank 7 (ROAR single-agent level): open Unity build with pixels, text and audio, 40 ms and 250 ms ticks. The best fit for testing the project's expectation that input and output over several channels at once (pixels, text, audio) is hard for LLMs, once the simpler environments are working.

## Demo

- [video] [ROAR GitHub README](https://github.com/tb6147877/ROAR) — Downloaded the 4 README GIFs (assets/tbs.gif, rts.gif, tb.gif, rt.gif), counted frames and duration, and checked frames at start, 1/3, 2/3 and end; also opened the environments/ folder (Linux and Windows Unity builds). Single-agent basic level (collect 3 coins, turret hazard) with Gemini-3.1 Pro: tbs.gif is turn-based (234 frames, 19.5 s) and the agent collects 3 coins while the in-game timer goes from about 04:52 to 04:36; rts.gif is real-time with a 40 ms fixed interval (1263 frames, 105 s) and the agent ends with 16 HP and 0 coins at timer 02:53 after turret hits. Mixed 2v2 battle, Gemini-3.1 Pro (knights) vs GPT-5.4 (clowns), 4-pane split screen: tb.gif is turn-based (17.9 s) with the timer near 04:38; rt.gif is real-time at 40 ms (1841 frames, 153 s) with the timer going from 04:59 to 01:55 and three panes ending in "You Lost!" as the toxic zone closes, captioned as Gemini eliminated by the toxic zone "due to delayed actions". Play-mode evidence (recorded GIFs, not live): in rt.gif the in-game countdown drops about 184 s over 153 s of footage, so the clock runs while the models think, while the turn-based clips advance only about 16-22 s of game clock, consistent with pausing during inference. No in-browser play; the README says humans can "try out yourself" with the downloadable executables.
- [project-page] [ROAR arXiv abstract](https://arxiv.org/abs/2610.24282) — Read the abstract page of "ROAR: Benchmarking LMM Agents under Real-Time Constraints in Multiplayer Action-Shooter Games" (NeurIPS 2026). It describes cooperative, competitive, mixed and single-agent levels and the Multi-Agent Asynchronous Gym, and links only the PDF, HTML and code (no project page or video). Play-mode evidence (text only): the environment advances at fixed intervals while agents reason in separate threads.
- [dead-or-unreachable] [Multi_Agent_Asynchronous_Gym repo](https://github.com/tb6147877/Multi_Agent_Asynchronous_Gym) — Opened the author's sibling repo. It is an empty placeholder with one initial commit (.gitignore, LICENSE and a title-only README), no code or media. No play-mode evidence.

Visited 10 November 2026 in a headless browser.

## Fit

realtime yes; verifiable yes; single-player level exists; human-easy plausible, unmeasured; short (5 min). The multi-channel observation (pixels, text, audio) matches the project's expectation that several input channels at once are hard for LLMs (see the [home page](../README.md)).

Related: [TowerMind](towermind.md) (same group; ROAR is its realtime follow-up); [Unity ML-Agents](unity-ml-agents.md)
