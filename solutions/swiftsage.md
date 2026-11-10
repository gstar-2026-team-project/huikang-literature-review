# SwiftSage

SwiftSage pairs a small cloned fast model with a GPT-4 planner and a heuristic switch.

| | |
|---|---|
| Year | 2023 |
| Links | [arXiv 2305.17390](https://arxiv.org/abs/2305.17390) |
| Demo | [project page](https://swiftsage.github.io): static paper page with figures only. It has no video, trajectory viewer or live run. The V2 [HF Space](https://huggingface.co/spaces/swiftsage-ai/SwiftSage) is a text-reasoning Q&A demo, not a game, and currently shows a runtime error. Human-playable: no. |
| Category | scaffold |
| Method | Small cloned fast model + GPT-4 planner, heuristic switch |
| Evaluated on | ScienceWorld |
| Evaluation play mode | paused-live |
| Results | (not extracted) |
| Basis | paper §2: ScienceWorld text environment, one action per step |

## Demo

- [project-page] [SwiftSage project page](https://swiftsage.github.io) — Expanded every '[show more]' section and dumped the page: static NeurIPS 2023 page with four images (methods.png, ss_pipeline.png, eval.png, curves_all.png), no video, iframe, canvas or interactive element. Nothing to play or replay. It describes the Swift module (T5-large behavior cloning) and Sage module (GPT-4) switched by a heuristic with an action buffer, framing the benefit as fewer LLM calls and lower cost; ScienceWorld is turn-based and waits for each action.
- [dead-or-unreachable] [SwiftSage V2 HF Space](https://huggingface.co/spaces/swiftsage-ai/SwiftSage) — Waited 20 s; it shows a red 'Runtime error' badge, 'Exit code: ?. Reason:' and 'Failed to retrieve error logs: SSE is not enabled'. Even when working it was the V2 Gradio demo for text reasoning (math and QA with LLM-written Python), not a game.
- [dead-or-unreachable] [ScienceWorld demo](https://sciworld.apps.allenai.org/) — The environment demo linked from the project page timed out after 45 s (ERR_CONNECTION_TIMED_OUT); it would only have been the environment, not a SwiftSage run.

Visited 10 November 2026 in a headless browser.