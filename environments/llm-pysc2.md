# LLM-PySC2

LLM-PySC2 gives LLMs the full pysc2 action space, with each step waiting up to a maximum time for all agents.

| | |
|---|---|
| Year | 2024 |
| Links | [arXiv 2411.05348](https://arxiv.org/abs/2411.05348) |
| Demo | [GitHub README GIFs](https://github.com/NKAI-Decision-Team/LLM-PySC2): eight short GIFs (9-21 s each) of LLM-controlled Protoss units in SMAC and llm_pysc2 battles, captured from the StarCraft II replay viewer (timeline "0:08 / 0:38"). They are recordings of replays, not a live model on a clock, and nothing is human-playable. |
| Play mode | paused-live |
| Clock | bounded wait per step |
| Observation | text + image |
| Action | full pysc2 actions |
| Players | 1 vs AI |
| Horizon | 2 min micro to full game |
| Human reference | none |
| Open source | open |
| Convertible to realtime-live | pysc2 `realtime=True` |
| Basis | code: `llm_pysc2/agents/llm_pysc2_agent_main.py` (step waits up to `MAX_LLM_WAITING_TIME = 15` s; no_op on timeout); pysc2 `SC2Env` realtime=False |

## Details

- LLM-PySC2 ([arXiv 2411.05348](https://arxiv.org/abs/2411.05348)): the step waits up to a maximum waiting time for all agents; "asynchronous" refers to parallel queries.
- Convertibility (StarCraft II family): SC2 has a verified `realtime=True`; SMAC-style micro battles are under two minutes with objective outcomes. Units keep executing orders, so degradation under a clock is gradual for macro play and sharp for micro.

## Demo

- [video] [LLM-PySC2 GitHub README GIFs](https://github.com/NKAI-Decision-Team/LLM-PySC2): I opened the repo README, listed its images and opened the GIFs in `docs/figures/` (llm_smac_demo1-3.gif, llm_pysc2_demo1-5.gif), screenshotting frames and counting their frames. The caption reads "Demos of LLM-Pysc2 with SMAC tasks". The GIFs are 400x225 and run 9.0-20.8 s (for example, llm_pysc2_demo4.gif has 135 frames over 9.0 s). They show Protoss Stalker and Zealot groups fighting Zerg or Terran armies on snow and tiled SMAC maps. Play-mode evidence (recording): the SC2 replay-viewer panel with a timeline ("0:08 / 0:38" on the first frame of llm_pysc2_demo4.gif) and a player selector is visible, so these are screen captures of saved replays. They show no LLM latency or step readout, so they cannot show whether the game paused for the bounded per-step wait. The repo has no homepage field and the arXiv page lists no demo.

Visited 10 November 2026 in a headless browser.

Related: [PySC2 / python-sc2](pysc2-python-sc2.md); [TextStarCraft II](textstarcraft-ii.md); [AVA / AVACraft](ava-avacraft.md); [SMAC / SMACv2](smac.md); [RTSGameBench](rtsgamebench.md)
