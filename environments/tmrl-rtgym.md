# tmrl / rtgym (TrackMania)

tmrl runs TrackMania at 20 Hz with an elastic wall-clock time step, and `rtgym` is a ready-made wall-clock wrapper for any step-locked environment.

| | |
|---|---|
| Year | 2021 |
| Links | [tmrl](https://github.com/trackmania-rl/tmrl), [rtgym](https://github.com/yannbouteiller/rtgym) |
| Demo | [video](https://www.youtube.com/watch?v=c1xq7iJ3f9E): French Underscore_ show, 2022. A tmrl SAC policy drives TrackMania live through a virtual gamepad (caption 'VUE DE L'IA', race timer running). The rtgym 'Time-step timed out' warning on screen shows the real-time clock does not wait. Pros race it afterward. Not an LLM. Human-playable: no. |
| Play mode | realtime-live |
| Clock | 20 Hz elastic wall-clock step |
| Observation | screenshots or LIDAR + speed |
| Action | analog gas/brake/steer |
| Players | 1 |
| Horizon | 30-60 s lap |
| Human reference | easy |
| Open source | MIT + game client |
| Convertible to realtime-live | n/a |
| Basis | code: rtgym `rtgym/envs/real_time_env.py` `time_step_duration 0.05`; README "Time-steps are being elastically constrained"; tmrl README "runs at 20Hz by default" |

## Details

- **tmrl / rtgym** ([tmrl](https://github.com/trackmania-rl/tmrl), [rtgym](https://github.com/yannbouteiller/rtgym), both MIT): TrackMania at 20 Hz with an elastic wall-clock time step; the last actions are appended to the observation. Fits 5 of 5 in principle; needs the game client and a GPU. `rtgym` is a ready-made wall-clock wrapper for any step-locked environment.
- The common conversion of a paused-live environment is a wrapper that steps the simulator in a timer thread at its native rate and applies the agent's latest action, or a default, when no new one has arrived. `rtgym` implements this (see the general conversion notes in the [index](README.md#converting-paused-live-environments)).

## Demo

- [video] [On a entraîné une I.A sur Trackmania pendant 200h](https://www.youtube.com/watch?v=c1xq7iJ3f9E) — Watched frames at about 1:40, 6:42, 9:00, 12:33, 13:40 and 15:30 of the Underscore_ episode (Jun 2022, 16:45) with tmrl author guests (chapters: AI's first race 8:40, pros vs the AI 13:06, final race). Frames show TrackMania on the TSH / Grand League track with an in-game race timer (00:16.52, 00:26.33, 00:34.35), the caption 'VUE DE L'IA', and a PowerShell window running tmrl/rtgym with logs such as 'Loading model', 'virtual joystick' and an rtgym 'Time-step' timeout warning. Play-mode evidence (recording): the trained SAC policy drives through a virtual gamepad while the game clock runs, and the 'Time-step timed out' warning shows rtgym keeps a fixed real-time step and does not wait for the agent; not an LLM.

Visited 10 November 2026 in a headless browser.

## Fit

Fits 5 of 5 in principle; needs the game client and a GPU.

Related: [Real-Time Reasoning Gym](realtime-gym.md)
