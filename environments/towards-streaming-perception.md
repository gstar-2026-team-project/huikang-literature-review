# Towards Streaming Perception

Towards Streaming Perception defines "streaming accuracy", scoring the most recent finished output against the current world state.

| | |
|---|---|
| Year | 2020 |
| Authors / org | Li, Wang, Ramanan |
| Links | [arXiv 2005.10420](https://arxiv.org/abs/2005.10420) |
| Demo | [project page](https://www.cs.cmu.edu/~mengtial/proj/streaming/) + [visual walkthrough](https://mtli.github.io/streaming/streaming-visuals.html): talk videos and pre-rendered dashcam videos comparing offline and streaming (latency-aware) detectors and forecasting, with the Argoverse-HD annotation viewer and an [eval.ai challenge leaderboard](https://eval.ai/web/challenges/challenge-page/800/overview). Human-playable: no. |
| Play mode | realtime-live (benchmark-level: output scored against the current world state) |
| Clock | wall clock of the video stream |
| Basis | paper §1: defines "streaming accuracy" and "a clear metric to compare different methods along the Pareto optimal latency-accuracy curve" |

## Details

- Also a framing paper from RL on modelling the clock: Li, Wang, Ramanan, Towards Streaming Perception (2020), [arXiv 2005.10420](https://arxiv.org/abs/2005.10420): scores the most recent finished output against the current world state, the ancestor of "action age".

## Demo

- [video] [Streaming Perception project page](https://www.cs.cmu.edu/~mengtial/proj/streaming/) — Played the embedded 10-minute (600 s) and 2-minute (120 s) talk videos for about 5 s each, opened the linked Visual Walkthrough page, played 'Detectors Only' and seeked into 'Single GPU vs Infinite GPUs' and 'Forecasting', and opened the Argoverse-HD val annotation viewer. The walkthrough shows dashcam footage with detection boxes and captions such as "Accurate Detector (Offline) Excellent but not practical (AP 38.0)" and "Infinite GPU Final Solution More responsive (AP 20.3)", with streaming boxes lagging behind moving cars unless forecasting is used. Play-mode evidence (recording): pre-rendered MP4s (e.g. vid/Detectors%20Only.mp4, vid/Compute%20(Final%20Solutions).mp4) visualizing streaming evaluation, where the video clock keeps running while the detector computes and stale outputs are scored against the current frame; not live inference, no game, no LLM.

Visited 10 November 2026 in a headless browser.

Related: [Framing papers](README.md#framing-papers-from-rl-on-modelling-the-clock)
