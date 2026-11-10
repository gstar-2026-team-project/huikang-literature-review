# OSWorld 2.0

OSWorld 2.0 is a computer-use benchmark of 108 long tasks, step-looped, with 6 streaming tasks whose UI keeps animating.

| | |
|---|---|
| Year | 2026 |
| Links | [arXiv 2606.29537](https://arxiv.org/abs/2606.29537) |
| Demo | [project page](https://osworld-v2.xlang.ai/) with a 21 s overview video and leaderboard, and a [task showcase](https://osworld-v2.xlang.ai/task-showcase/) replay viewer that steps through recorded screenshot trajectories (8 tasks, per-step actions and thinking, rubric scores). Recordings only; not human-playable and no live model calls. |
| Play mode | paused-live (step loop) with 6 streaming tasks whose UI keeps animating |
| Clock | screenshot, then action; the page changes in between |
| Basis | paper §3: agents "observe the screen as a discrete sequence of screenshots"; "the environment can change continuously between the moment the agent takes a screenshot and the moment it executes an action"; mid-task emails or TeamChat messages are injected "during execution" |

## Details

- OSWorld 2.0: 108 long tasks; 10 dynamic-environment tasks and 6 streaming-interaction tasks (a moving pop-up, so clicks land on stale coordinates). Far too long-horizon for the team.

## Demo

- [project-page/video] [OSWorld 2.0 project page](https://osworld-v2.xlang.ai/) — Rendered the page and played the autoplaying overview video (`static/videos/osworld2-overview-no-cover.mp4`, 20.7 s), seeking to 12.8 s. The frame is a 4x4 grid of desktop recordings: slides, a pixel-art city game, CAD, video editing, Gmail, a PCB editor. The page also has an interactive leaderboard loaded from `static/data/leaderboard/official-results.json`, plotting score against output tokens, turns, actions or cost (top row "Claude Opus 5 max v2026.08.08 103K 31.4% 68.3%"), and a step-by-step failure-case gallery (for example `task103-step251.png`). Play-mode evidence: recorded media only.
- [replay-viewer] [Task showcase](https://osworld-v2.xlang.ai/task-showcase/) — Opened Task 052 "Travel Booking" (tag "Streaming Interaction", GPT-5.5, "100% 138 Steps") and pressed Play at 1x. It stepped through recorded screenshots, loaded from `static/data/showcase/runs/052_gpt-5-5.json` and `assets/showcase/052/gpt-5-5/step_*.jpg`. At "Step 7 / 138" the frame shows a "TravelHub Limited Offer" pop-up over the Paris results, a red "CLICK" marker and the thinking line "Analyzing overlay and popup behavior". Rubric gates include "Ad closed: The blocking advertisement must be closed." The other seven tasks shown are 004, 008, 024, 035 ("Dynamic Environment"), 053, 098 and 103, with a model selector (GPT-5.5, Qwen 3.7-Plus, Claude Sonnet 4.6 Max, MiniMax M3, Claude Opus 4.7, Claude Sonnet 4.6) and 0.5x/1x/2x playback. Play-mode evidence: a recorded replay indexed by step, consistent with the step loop. The playback speed is a viewer setting and shows no wall-clock timing for the agent.
- [trajectory-viewer] [Explore all task trajectories](https://osworld-v2.xlang.ai/task-trajectories/) — Redirects to osworld-v2-monitor.xlang.ai, which returned "Cloudflare Tunnel error" (Error 1033) when visited, so it could not be used. Raw trajectories are also linked as zips in the Hugging Face dataset `xlangai/osworld2.0-trajectory`.

Visited 10 November 2026 in a headless browser.

Related: [OSWorld-Human](osworld-human.md)
