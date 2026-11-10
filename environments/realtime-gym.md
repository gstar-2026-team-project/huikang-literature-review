# Real-Time Reasoning Gym (RealtimeGym)

Real-Time Reasoning Gym (RealtimeGym) runs Freeway, Snake and Overcooked (scripted partner) at three cognitive-load levels with an environment that steps once every N generated tokens.

| | |
|---|---|
| Year | 2025 |
| Authors / org | Wen, Ye, Y. Zhang, Yang, Zhu (Stanford SALT and others) |
| Links | [arXiv 2511.04898](https://arxiv.org/abs/2511.04898), code [SALT-NLP/RealtimeGym](https://github.com/SALT-NLP/RealtimeGym) (MIT) |
| Demo | [interactive demo](https://realtimegym.saltlab.stanford.edu/): replay viewer of recorded trajectories (Freeway, Snake, Overcooked; load and time-pressure settings) showing the Reactive, Planning and AgileThinker agents side by side with per-step reasoning traces. Not human-playable. |
| Play mode | realtime-live |
| Clock | TOKEN (4k-32k tok/step) or WALL seconds |
| Observation | text |
| Action | 1 discrete move/step |
| Players | 1 (scripted partner) |
| Horizon | 100 steps |
| Human reference | none |
| Open source | MIT |
| Convertible to realtime-live | n/a |
| Basis | paper §2: "the environment steps forward at a fixed rate, even when the agent has not finished thinking"; README `--time_unit token` / `seconds`, `agent.act() or DEFAULT_ACTION` |

## Details

- Real-Time Reasoning Gym (RealtimeGym) (Nov 2025, ICLR 2026).
- Wen, Ye, Y. Zhang, Yang, Zhu (Stanford SALT and others). [arXiv 2511.04898](https://arxiv.org/abs/2511.04898); code [SALT-NLP/RealtimeGym](https://github.com/SALT-NLP/RealtimeGym) (MIT).
- Tasks: Freeway, Snake, Overcooked (scripted partner), each at three cognitive-load levels.
- Play mode: realtime-live. The environment steps once every N generated tokens (32k, 16k, 8k, 4k tokens per step are the pressure levels). If no action is ready the default applies (repeat previous direction, or idle). The repo also has `--time_unit seconds` for wall clock. The paper's wall-clock validation used steps of about six minutes, so the game is slowed to LLM speed, not run at human game speed.
- Observation: text. Action: one discrete move per step. 100 steps per episode. Scores normalised to 0-1. No human baseline. Only DeepSeek models in the main results, because the AgileThinker scaffold needs visible reasoning traces.
- Results: at medium load the planning agent (DeepSeek-R1) falls from 0.92 to 0.05 as pressure rises; the reactive agent stays flat but low; AgileThinker goes 0.90 to 0.58.
- Shortlist rank 6 (RealtimeGym: Freeway, Snake, Overcooked): use as the training-friendly text environment: token clock gives reproducible rollouts for RL, and AgileThinker is a ready baseline. Add a human baseline and faster tick settings.

## Demo

- [replay-viewer] [RealtimeGym interactive demo](https://realtimegym.saltlab.stanford.edu/) — Not playable by a human; it is a replay viewer. You choose the game (Freeway, Snake, Overcooked), task ID 0-7, cognitive load (Easy/Medium/Hard) and time pressure (Low to Extreme), and Play steps through recorded trajectories loaded from static JSON (console: "Attempting to load: static/data/freeway_hard_4k_seed3_reactive.json"; "Playing at speed: 250 ms per step"). The Reactive Agent, Planning Agent and AgileThinker are shown side by side, each with score, next action and an expandable "Agent Reasoning" trace. At Freeway / Hard / Extreme (4k tokens per step), step 49 of 100, all three were at score 51. Play-mode evidence (recorded replay): consistent with the paper's token clock; the replay is indexed by environment step, and the reasoning shown per step is what the agent produced within that step's token budget. The 250 ms/step playback speed is a viewer setting, not the evaluation clock.

Visited 10 November 2026 in a headless browser.

## Fit

realtime yes (simulated); verifiable yes; single yes; human-easy yes but unmeasured; short yes. Reusable: the token-clock harness, the two knobs (load and pressure), default-action-on-timeout, and three shipped agents.

Related: [AgileThinker](../solutions/agile-thinker.md) (the scaffold shipped with the gym); [Overcooked-AI](overcooked-ai.md); [tmrl / rtgym](tmrl-rtgym.md)
