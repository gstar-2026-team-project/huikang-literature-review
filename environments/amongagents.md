# AmongAgents (Among Us)

AmongAgents is an Among Us game that "repeatedly switches between two phases (Task Phase and Meeting Phase)".

| | |
|---|---|
| Year | 2024 |
| Links | [arXiv 2407.16521](https://arxiv.org/abs/2407.16521) |
| Demo | None found (searched: arXiv abstract page and comments, GitHub repo cyzus/among-agents README and homepage field, web search for "AmongAgents demo") |
| Play mode | paused-live, phase/step-based |
| Clock | task and meeting phases |
| Basis | paper §3: "The gameplay ... repeatedly switches between two phases (Task Phase and Meeting Phase)" |

## Details

- All the turn-based arenas convert trivially by adding a wall-clock deadline per message, as the UPenn paper does. No realtime Among Us benchmark was found.

## Demo

- None found. The arXiv comments only say "Wordplay @ ACL 2024"; the repo [cyzus/among-agents](https://github.com/cyzus/among-agents) has no homepage field, and its README is text only (setup, `python main.py`, `notebooks/run_game.ipynb`) with no videos, GIFs or replay viewer. A web search found only paper mirrors. The 2025 follow-up "Among Us: A Sandbox for Agentic Deception" (socialdeductionllm.github.io) is a separate work.

Searched 10 November 2026; no demo found.

Related: [Real-Time Deadlines (UPenn negotiation)](real-time-deadlines-negotiation.md)
