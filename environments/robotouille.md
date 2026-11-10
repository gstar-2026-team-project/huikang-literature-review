# Robotouille

Robotouille is a cooking benchmark where "asynchronous" means in-game cooking delays, not model latency.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2502.05227](https://arxiv.org/abs/2502.05227) |
| Demo | [project page](https://portal-cornell.github.io/robotouille/): three short looping recorded videos of the pygame kitchen (a montage of many procedurally generated kitchens, one synchronous and one asynchronous episode) plus dependency-graph figures. Recordings only; no replay viewer, live model or human-playable page. |
| Play mode | paused-live |
| Clock | STEP with in-game delays |
| Observation | text (pygame render) |
| Action | discrete |
| Players | 1 |
| Horizon | short |
| Human reference | none |
| Open source | open |
| Convertible to realtime-live | plausible |
| Basis | code: `robotouille/robotouille_simulator.py` (`propose_actions` then `env.step`); paper §2: delays count environment steps |

## Details

- Robotouille ([arXiv 2502.05227](https://arxiv.org/abs/2502.05227)): "asynchronous" means in-game cooking delays, not model latency. ReAct GPT-4o: 47% synchronous, 11% asynchronous.
- Convertibility (Overcooked family): easy. A scripted partner makes it effectively single player.

## Demo

- [project-page-video] [Robotouille project page](https://portal-cornell.github.io/robotouille/) (linked from the repo README as "Project Website") — opened it, played and seeked the three autoplaying, looping videos and screenshotted frames; `static/videos/all_tasks.mp4` (14 s) is a montage of many kitchen layouts with robot chefs, `synchronous_run.mp4` (12.3 s, caption "Synchronous Example", "Make a lettuce tomato cheeseburger") and `asynchronous_run.mp4` (11.1 s, caption "Asynchronous Example", "Make a lettuce tomato fried chicken sandwich", with stoves and fryers cooking) each show one robot chef completing a task, next to a dependency-graph image. Play-mode evidence (recording): the clips are pre-rendered MP4s with no step counter, timer or model readout, and the page does not say which agent produced them; network traffic showed only static files (videos, images, analytics), no model calls. Results are shown as static images (results.png, failure_modes.png).

Visited 10 November 2026 in a headless browser.

Related: [Overcooked-AI](overcooked-ai.md); [Collab-Overcooked](collab-overcooked.md); [TimeArena](timearena.md)
