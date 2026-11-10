# DPT-Agent

DPT-Agent is a scaffold in which an FSM rewritten by the LLM acts every tick, with asynchronous reflection and theory of mind.

| | |
|---|---|
| Year | 2025 |
| Authors / org | Zhang et al. |
| Links | [arXiv 2502.11882](https://arxiv.org/abs/2502.11882), [code](https://github.com/sjtu-marl/DPT-Agent) (MIT) |
| Demo | [project page](https://sjtu-marl.github.io/DPT-Agent-page/): two short recorded GIFs (7 s and 15 s) of DPT-Agent (red hat) cooking alongside a human (blue hat) in a pixel-art Overcooked burger kitchen, with the time_left counter running down (clips appear sped up), plus static results tables; [AGI-Eval leaderboard](https://agi-eval.cn/evaluation/detail?id=56): score and latency tables, no replays. Human-playable online: no (the repo ships a local human-vs-LLM Flask app on localhost:5001). |
| Category | scaffold |
| Method | FSM (rewritten by the LLM) acts every tick; asynchronous reflection and theory of mind |
| Evaluated on | Overcooked at 4 Hz |
| Evaluation play mode | realtime-live (part scripted) |
| Results | 46.6 against ReAct 15.5 |
| Open source | MIT |
| Basis | code: `llm_agent_run_dpt_exp1.py` (`env.step` loop paced by `asyncio.sleep(0.25)`); paper: "each timestep corresponds to 0.25 seconds in the real world" |

## Details

- **DPT-Agent** (Zhang et al., ACL 2025; [code](https://github.com/sjtu-marl/DPT-Agent), MIT). System 1 is an FSM over macro actions with A* for atomic moves; the LLM periodically rewrites the FSM logic and the FSM keeps acting when no new code arrives. System 2 runs asynchronously. Reasoning models score negative under plain ReAct in realtime (o3-mini-high: -43.0) and 55.2 with DPT. Human study with 68 participants.

## Demo

- [project-page] [DPT-Agent project page](https://sjtu-marl.github.io/DPT-Agent-page/) — Opened the page, clicked the three results tabs and downloaded the two demo GIFs: "Map 1: DPT-Agent (in red hat) collaborating with human (in blue hat) through division of labor" (1.gif, 105 frames, 7.0 s) and "Map 2: ... by using the central counter" (2.gif, 225 frames, 15.0 s), both a pixel-art Overcooked burger kitchen with an order queue and a "score / time_left" bar. The tabs show static ReAct and Reflexion tables with Score, Score Efficiency and Latency (e.g. GPT-4o ReAct 7.10 s). Play-mode evidence (recording): time_left falls during play (GIF1 377 to 335 over 7 s; GIF2 246 to 160 over 15 s, about 6 units per playback second), so the clips are sped up or count env steps; there is no thinking or latency overlay and no model calls, only static files. No video, playable game or replay viewer.
- [leaderboard] [AGI-Eval Overcooked leaderboard](https://agi-eval.cn/evaluation/detail?id=56) — Opened the page linked from the GitHub README: an "Overcooked Challenge: Real-time Simultaneous Human-AI Collaboration" leaderboard (Chinese) ranking models per setting (e.g. "Single Agent - DPT-Agent w/o ToM": DeepSeek-R1-70b 60.00, QwQ-32b 51.00) with Score, Score Efficiency and Latency columns (e.g. 9.09 s, 14.96 s). Play-mode evidence: numbers only; no replays or video.

Visited 10 November 2026 in a headless browser.

## What the team could reuse

- Reuse: an FSM safety net and an open 4 Hz harness.
- Baselines: FSM safety net (DPT) (from the scaffolds reuse list).

Related: [DPT-Agent Overcooked](../environments/dpt-agent-overcooked.md) (evaluated on; environment details); [HLA](hla.md); [AgileThinker](agile-thinker.md)
