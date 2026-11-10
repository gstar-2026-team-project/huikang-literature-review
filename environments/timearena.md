# TimeArena

TimeArena is a text environment with simulated action durations that tests multitasking as planning.

| | |
|---|---|
| Year | 2024 |
| Links | [arXiv 2402.05733](https://arxiv.org/abs/2402.05733) |
| Demo | [project page](https://time-arena.github.io/) with two "Demo videos" ("Parallel Processing", "Serial Processing"): animated pixel-art recordings of one tea-room episode with a simulated clock (T=...min), action, feedback and score overlays. Recordings on a simulated clock, not a model playing live; not human-playable. |
| Play mode | paused-live |
| Clock | simulated action durations |
| Observation | text |
| Action | text actions |
| Players | 1 |
| Horizon | 40 simulated min |
| Human reference | none |
| Open source | site |
| Convertible to realtime-live | map sim minutes to seconds |
| Basis | code: `LLM_test.py` (`Agent.act` then `current_time += 1` simulated minutes) |

## Details

- TimeArena ([arXiv 2402.05733](https://arxiv.org/abs/2402.05733)): simulated action durations; model latency not counted. Tests multitasking as planning.
- Convertibility (Overcooked family): easy. TimeArena converts by mapping simulated minutes to wall seconds.

## Demo

- [video] [TimeArena project page](https://time-arena.github.io/) — I played and seeked both videos under "Demo videos": "Parallel Processing" (`uploads/videos/parallel.mp4`, 3:30) and "Serial Processing" (`uploads/videos/normal.mp4`, 3:38). Each is a pixel-art animation of a character in a "TEA ROOM" (kettle, sink, washing machine, each with a ring-timer alarm clock showing an action in progress), with a text overlay of score, simulated time, action and feedback. Parallel video: "T=7min" at 1:03 with "Score: 0"; "T=16min" at 2:06 with "Action: Pour tea into cup", "Feedback: Cup is filled!", "Task1 completed!"; "T=39min" at 3:20 with "Score: 95.38". Serial video ends at "T=65min" with "Score: 95.38". The page does not say whether a model, a human or an oracle chose the actions. Play-mode evidence (recording): the clock overlay advances in simulated minutes per action, not wall time, so the same final score takes 39 versus 65 simulated minutes; this matches the paused-live label. The page's code card says "Coming soon!" but links [ykzhang721/TimeArena](https://github.com/ykzhang721/TimeArena).

Visited 10 November 2026 in a headless browser.

Related: [Overcooked-AI](overcooked-ai.md); [Collab-Overcooked](collab-overcooked.md); [Robotouille](robotouille.md)
