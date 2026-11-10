# FPX (Win Fast or Lose Slow)

FPX is mixed-precision quantisation used as a latency knob, evaluated on Street Fighter and HFTBench.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2505.19481](https://arxiv.org/abs/2505.19481) |
| Demo | [project page](https://www.competitive-agent.com/): pre-recorded screen-capture videos of LLM-vs-LLM Street Fighter III matches (DIAMBRA) in which the round timer keeps running while the models think, selectable by FPX speedup (1.0x = 1301ms to 2.4x = 542ms latency for the red player), plus animated HFTBench yield charts (FPX vs FP16) and an offline latency-tradeoff dial; [code](https://github.com/HaoKang-Timmy/LatencySensitiveBench) embeds one more clip. Human-playable: no. |
| Category | scaffold |
| Method | Mixed-precision quantisation as a latency knob |
| Evaluated on | Street Fighter, HFTBench |
| Evaluation play mode | realtime-live |
| Results | 3B at 195 ms beats 7B; 14B best for trading |
| Basis | code: `StreetFighter/GameEngine/Engine/game.py` (continuous `env.step`, action 0 when none pending); `HFTBench/Environment/TradingEnv.py` (measured delay worsens fill price) |

## Demo

- [video] [competitive-agent.com project page](https://www.competitive-agent.com/) — Loaded the page and clicked each speed button (1.0x, 1.6x, 2.1x, 2.4x) of the StreetFighter "FPX Speed Demonstration" widget, which swaps between 4 pre-recorded .mov clips of about 34-37 s each; seeked the 1.0x and 2.4x clips and captured frames. The clips are macOS desktop screen recordings of Street Fighter III (Ken vs Ken, model vs model, via DIAMBRA), captioned e.g. "1.0x Speed For Red Player / Latency: 1301ms (14B Model)" and "Latency: 542ms" at 2.4x. Play-mode evidence (recording): the round timer counts down on its own (62 at 0:11, 32 at 0:33 in the 1.0x clip; 54 at 0:35 in the 2.4x clip) and scores change (2500 vs 1700, then 3900 vs 6200), so the game does not wait for the model; the network log shows only .mov fetches and no model calls. Not human-playable.
- [video] [competitive-agent.com project page](https://www.competitive-agent.com/) — Loaded the page and screenshotted the HFTBench section: a Chart.js animated cumulative-yield chart (FPX vs FP16), a GIF of yield bars, a results table of daily yield, and a draggable "Latency-Quality Trade-off" speed dial. The dial only moves points along precomputed win-rate/yield curves and calls no model. Play-mode evidence: none for HFTBench; there is no replay or recording of a trading run, only charts.
- [project-page] [LatencySensitiveBench repo](https://github.com/HaoKang-Timmy/LatencySensitiveBench) — Read the README. Its Visualization section embeds one more recorded StreetFighter clip (video1_8vsfpx.mp4) and has an HFTBench heading; run instructions use DIAMBRA Arena (`run_api.py --agent1 Qwen/Qwen3-4B --agent2 Qwen/Qwen3-8B`), which needs a DIAMBRA account and the game ROM. Play-mode evidence: only a recorded video plus instructions for running locally; nothing hosted to play or run live.

Visited 10 November 2026 in a headless browser.

Related: [Win Fast or Lose Slow: StreetFighter](../environments/streetfighter-win-fast-or-lose-slow.md); [HFTBench](../environments/hftbench.md)
