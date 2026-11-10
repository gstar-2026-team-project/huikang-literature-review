# Think in Games

Think in Games trains Qwen 14B/32B with SFT and GRPO to predict macro actions for Honor of Kings replay snapshots.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2508.21365](https://arxiv.org/abs/2508.21365) |
| Demo | None found (searched: arXiv abstract and HTML paper links, Hugging Face papers/Spaces, GitHub, web search for "Think in Games" demo; only press coverage, no project page, repo or video) |
| Category | post-training |
| Method | SFT + GRPO on replay labels |
| Evaluated on | Honor of Kings macro prediction |
| Evaluation play mode | offline, not gameplay |
| Basis | paper §3.1: "label the main player's action as the ground truth for each game state" (offline prediction) |
| What is trained | Qwen 14B/32B |

## Details

- **Think in Games** does not play Honor of Kings live; it predicts macro actions for replay snapshots (66.67% to 86.84% with GRPO).

## Demo

- None found. Searched the arXiv 2508.21365 abstract (no comments field or code link), the paper HTML's external links (only citations), Hugging Face (no models, datasets or Spaces linked to the paper), GitHub repo search, and web search for "Think in Games" Honor of Kings demo/GitHub (only Tencent press coverage and paper summaries).

Searched 10 November 2026; no demo found.

Related: [Think in Games (Honor of Kings replays)](../environments/think-in-games.md) (environment details)
