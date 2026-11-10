# microRTS

microRTS is a small RTS game whose competition gives a 100 ms compute budget per game cycle.

| | |
|---|---|
| Year | 2013 |
| Links | [wiki](https://github.com/Farama-Foundation/MicroRTS/wiki) |
| Demo | [video](https://www.youtube.com/watch?v=_jVOMNqw3Qs): Ontañón's 2018 install walkthrough (git clone, README) for the microRTS AI competition. No gameplay in the sampled frames. Human-playable: no. |
| Play mode | paused-live with 100 ms per-cycle budget (competition) / paused-live (gym) |
| Clock | per game cycle |
| Observation | feature planes |
| Action | per-cell actions |
| Players | 2 (vs bot) |
| Horizon | thousands of cycles |
| Human reference | n/a |
| Open source | open; Python binding deprecated |
| Convertible to realtime-live | low |
| Basis | code: `src/tournaments/Tournament.java` (synchronous `getAction`, timed; overrun beyond budget + tolerance = timeout loss); rules page "computation budget of 100 milliseconds per game cycle"; MicroRTS-Py `vec_env.py` `gameStep` |

## Details

- **microRTS competition**: 100 ms compute budget per game cycle (rules page, saved). The game itself waits for `getAction` (`Tournament.java`) but overruns lose by timeout, so it is paused-live with a hard thinking budget.

## Demo

- [video] [Setting up microRTS](https://www.youtube.com/watch?v=_jVOMNqw3Qs) — Watched frames at about 0:28, 1:43 and 3:14 of Santiago Ontañón's video (Mar 2018, 4:19) made for the 2018 microRTS AI competition. Frames show a macOS desktop with the microRTS GitHub README and a terminal running git clone / cd into the project. No gameplay or agent play in the sampled frames; the visible README says microRTS is "deterministic and real-time (players can issue actions simultaneously, and actions are durative)".

Visited 10 November 2026 in a headless browser.