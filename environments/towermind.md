# TowerMind

TowerMind is an open Unity tower defence with pixel, JSON and vector observations.

| | |
|---|---|
| Year | 2026 |
| Links | [arXiv 2601.05899](https://arxiv.org/abs/2601.05899) |
| Demo | [GitHub README GIF](https://github.com/tb6147877/TowerMind) captioned "GPT-4.1 playing TowerMind": a short recording (about 6 s) of the model building towers on one level, not a live run or replay viewer. A [Colab notebook](https://colab.research.google.com/drive/13AJxze6069ADPAa_NZcVmOo28gSWKiMj?usp=sharing) sets up and runs the environment yourself; nothing is human-playable in the browser. |
| Play mode | paused-live |
| Clock | STEP, 16 game steps/action |
| Observation | pixels, JSON, vector |
| Action | grid + action type |
| Players | 1 |
| Horizon | level |
| Human reference | expert-normalised |
| Open source | MIT, Unity binary |
| Convertible to realtime-live | yes |
| Basis | code: `llm_example/llm_run.py` (`agent.act` then `env.step`, `time_scale=20`); ML-Agents step API is synchronous (see Unity ML-Agents row) |

## Details

- **TowerMind** ([arXiv 2601.05899](https://arxiv.org/abs/2601.05899)): open Unity tower defence with pixel, JSON and vector observations; ROAR is the same group's realtime follow-up.
- The Basis cell's "see Unity ML-Agents row" refers to [Unity ML-Agents](unity-ml-agents.md).

## Demo

- [official-video] [TowerMind GitHub README](https://github.com/tb6147877/TowerMind) (code repo from the arXiv page; the repo homepage field points back to arXiv) — rendered the README and downloaded `assets/play_gif.gif` (512x512, 59 frames at 100 ms, about 5.9 s); captioned "GPT-4.1 playing TowerMind". Frame 0 shows an empty map with gold 500, a counter of 5 and base health 20. The last frame shows about nine towers placed along the paths, enemies on the road, gold 25, the counter at 0 and health still 20. Play-mode evidence (recording): the GIF has no clock, step counter or reasoning overlay, so it cannot show whether the game pauses while the model thinks. It is probably a sped-up or edited recording of an evaluation run.
- [runnable notebook] [TowerMind Colab example](https://colab.research.google.com/drive/13AJxze6069ADPAa_NZcVmOo28gSWKiMj?usp=sharing) (linked from the README) — opened it read-only without signing in; "A simple Colab example to help you quickly try out TowerMind!" It clones the repo, unzips the Linux build (`td.x86_64`), and installs Miniconda and xvfb to run the Gym interface. You run it yourself; there are no saved outputs or videos, and there is no human-playable or live hosted demo.

Visited 10 November 2026 in a headless browser.

Related: [ROAR](roar.md); [Unity ML-Agents](unity-ml-agents.md)
