# DPT-Agent Overcooked

DPT-Agent's harness is an open realtime Overcooked variant at 0.25 s per timestep in which human and agent act simultaneously.

| | |
|---|---|
| Year | 2025 |
| Authors / org | S. Zhang, X. Wang et al. (SJTU) |
| Links | [arXiv 2502.11882](https://arxiv.org/abs/2502.11882), code [sjtu-marl/DPT-Agent](https://github.com/sjtu-marl/DPT-Agent) (MIT) |
| Demo | [project page](https://sjtu-marl.github.io/DPT-Agent-page/): two short recorded GIFs (7 s and 15 s) of DPT-Agent (red hat) cooking alongside a human (blue hat) in a pixel-art Overcooked burger kitchen, with the time_left counter running down (clips appear sped up), plus static results tables; [AGI-Eval leaderboard](https://agi-eval.cn/evaluation/detail?id=56): score and latency tables, no replays. Human-playable online: no (the repo ships a local human-vs-LLM Flask app on localhost:5001). |
| Play mode | realtime-live (part scripted) |
| Clock | WALL, 0.25 s/step |
| Observation | text state |
| Action | macro actions via FSM |
| Players | 2 (human or bot partner) |
| Horizon | 125 s |
| Human reference | humans as partners |
| Open source | MIT |
| Convertible to realtime-live | n/a |
| Basis | code: `llm_agent_run_dpt_exp1.py:248` `env.step(decision)` in a loop paced by `await asyncio.sleep(0.25)` (line 298), LLM reflection in separate async tasks |

## Details

- Realtime Overcooked: DPT-Agent (2025), ACL 2025.
- DPT-Agent: S. Zhang, X. Wang et al. (SJTU), ACL 2025. [arXiv 2502.11882](https://arxiv.org/abs/2502.11882); code [sjtu-marl/DPT-Agent](https://github.com/sjtu-marl/DPT-Agent) (MIT). Overcooked variant, 0.25 s per timestep, human and agent act simultaneously, 500 timesteps.
- Realtime-live. For DPT-Agent this is in code: `llm_agent_run_dpt_exp1.py` steps the game in a loop paced by `asyncio.sleep(0.25)` while the LLM modules run as separate async tasks. The LLM never issues atomic actions: an FSM does. DPT-Agent is partly scripted in this review's sense, since the LLM rewrites FSM code.
- **PokeAgent speedrun winners** and **DPT-Agent's FSM** are scripted solutions inside realtime environments (see [PokeAgent Challenge, speedrunning track](pokeagent-speedrun.md)).
- Convertibility (Overcooked family): easy. DPT-Agent already runs overcooked-ai at 4 Hz wall clock. A scripted partner makes it effectively single player.
- Later, for pairwise work: DPT-Agent's realtime Overcooked (from the shortlist).

## Demo

- [project-page] [DPT-Agent project page](https://sjtu-marl.github.io/DPT-Agent-page/) — Opened the page, clicked the three results tabs and downloaded the two demo GIFs: "Map 1: DPT-Agent (in red hat) collaborating with human (in blue hat) through division of labor" (1.gif, 105 frames, 7.0 s) and "Map 2: ... by using the central counter" (2.gif, 225 frames, 15.0 s), both a pixel-art Overcooked burger kitchen with an order queue and a "score / time_left" bar. The tabs show static ReAct and Reflexion tables with Score, Score Efficiency and Latency (e.g. GPT-4o ReAct 7.10 s). Play-mode evidence (recording): time_left falls during play (GIF1 377 to 335 over 7 s; GIF2 246 to 160 over 15 s, about 6 units per playback second), so the clips are sped up or count env steps; there is no thinking or latency overlay and no model calls, only static files. No video, playable game or replay viewer.
- [leaderboard] [AGI-Eval Overcooked leaderboard](https://agi-eval.cn/evaluation/detail?id=56) — Opened the page linked from the GitHub README: an "Overcooked Challenge: Real-time Simultaneous Human-AI Collaboration" leaderboard (Chinese) ranking models per setting (e.g. "Single Agent - DPT-Agent w/o ToM": DeepSeek-R1-70b 60.00, QwQ-32b 51.00) with Score, Score Efficiency and Latency columns (e.g. 9.09 s, 14.96 s). Play-mode evidence: numbers only; no replays or video.

Visited 10 November 2026 in a headless browser.

## Fit

realtime yes; verifiable yes; two-player by design; human-easy; short. DPT-Agent's harness is an open 4 Hz realtime Overcooked.

Related: [DPT-Agent](../solutions/dpt-agent.md) (the scaffold); [HLA Overcooked](hla-overcooked.md); [Overcooked-AI](overcooked-ai.md)
