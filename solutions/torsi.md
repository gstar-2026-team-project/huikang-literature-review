# TORSI

TORSI is a scaffold in which a slow teacher writes guidance offline and a fast student plays live alone.

| | |
|---|---|
| Year | 2026 |
| Authors / org | Pan et al. |
| Links | [arXiv 2610.20665](https://arxiv.org/abs/2610.20665) |
| Demo | None found (searched: arXiv [abs](https://arxiv.org/abs/2610.20665) and HTML for project, code and video links; [Hugging Face papers page](https://huggingface.co/papers/2610.20665), which returns 404; [papers.cool](https://papers.cool/arxiv/2610.20665); and web searches for 'The World Won't Wait', RealtimeBench and TORSI). The paper only has static Figure 1 frame strips showing live-clock failures, such as Snake's 824 ms response against a 667 ms tick. It mentions released replay logs but gives no URL. Human-playable: no. |
| Category | scaffold |
| Method | Slow teacher writes guidance offline; fast student plays live alone |
| Evaluated on | RealtimeBench (6 arcade games) |
| Evaluation play mode | realtime-live, wall clock |
| Results | Fast student 13.51 to 24.19 |
| Open source | no code yet |
| Basis | paper §3: "While a response is pending, the game keeps running with the previous control still active"; §4 the student acts "without teacher calls" |

## Details

- **TORSI** (Pan et al., Oct 2026; no code yet). A slow teacher (GPT-6.1-sol) works offline on saved states and student trajectories in paused or slowed games and writes textual skills and rules; guidance is adopted only if it improves validation scores. The fast student (Jev, 0.52 s latency) then plays live with no teacher calls. Test average 13.51 to 24.19, against prompt optimisers ACE 13.22, AHE 16.59, GEPA 14.52. Guidance transfers to other fast models. No weight updates.

## Demo

- [project-page] [arXiv abstract and HTML](https://arxiv.org/abs/2610.20665) — Opened the abstract page and the HTML version (2610.20665v1) and searched the text and all links for a repo, project page, video or demo; none exists, and the only GitHub/HF links are third-party game engines and model checkpoints (gym-super-mario-bros, nes-py, SimpleNES, jev-snake, jev-tetris, JevBird, river-run-typesafe, three.js). The paper says "The release includes task definitions, per-episode outcomes, frozen agent specifications, reusable guidance, and replay logs" but gives no URL. Play-mode evidence (static paper figures, rendered from recorded replay logs): Figure 1 shows the game running during inference, with Mario hitting an enemy while the response is pending, a Temple jump colliding at 0.00/+0.33/+0.48 s, and a Snake turn failing at ticks 201 to 203 because the 824 ms response exceeds the 667 ms tick; Table 7 gives clock rates (Mario 10 FPS, Snake 1.5 moves/s, Tetris 450-200 ms per row, River 60 FPS). For TORSI specifically, the paper describes the slow teacher (GPT-6.1-sol) practising in paused or reset games and the fast student (Jev) playing live with no teacher calls (average score 13.51 to 24.19); Figure 6 uses Mario poses "replayed from archived feedback, teacher practice, and held-out episodes".
- [project-page] [papers.cool entry](https://papers.cool/arxiv/2610.20665) — Opened it; it is an abstract aggregator with PDF and Kimi links only, no media and no code or demo link. No play-mode evidence.
- [dead-or-unreachable] [Hugging Face papers page](https://huggingface.co/papers/2610.20665) — Returns 404 "Paper not found"; no HF model, dataset or Space cites the paper.

Visited 10 November 2026 in a headless browser.

## What the team could reuse

- Reuse: the natural no-training baseline that post-training should beat.
- Baselines: offline guidance (TORSI) (from the scaffolds reuse list).

Related: [RealtimeBench (TORSI)](../environments/realtimebench.md) (evaluated on; environment details); [AgileThinker](agile-thinker.md)
