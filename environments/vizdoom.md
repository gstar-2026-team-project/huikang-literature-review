# ViZDoom

ViZDoom is a Doom-based platform whose `ASYNC_PLAYER` mode advances at 35 tics/s without waiting for the agent, while `PLAYER` mode waits for it.

| | |
|---|---|
| Year | 2016 |
| Authors / org | Kempka, Wydmuch, Runc, Toczek, Jaskowski, 2016; Farama |
| Links | [repo](https://github.com/Farama-Foundation/ViZDoom), [competitions paper](https://arxiv.org/abs/1809.03470) |
| Demo | [docs](https://vizdoom.farama.org/): documentation only, with pre-rendered scenario GIFs and no agent videos or replays (the [original site](https://vizdoom.cs.put.edu.pl/) with the competition pages is unreachable). Third-party [HF Space](https://anakin87-tiny-doom-defender.hf.space/) streams two ~1M-parameter models playing Defend the Center live (MJPEG frames plus an SSE step/action/kills feed). Human-playable: no. |
| Play mode | paused-live (`PLAYER`) + realtime-live (`ASYNC_PLAYER`) |
| Clock | 35 tics/s wall clock in async, scalable |
| Observation | pixels, depth, labels, audio buffer, game vars |
| Action | buttons, mouse deltas |
| Players | 1 or multi |
| Horizon | scenarios under 1 min |
| Human reference | humans easy |
| Open source | MIT |
| Convertible to realtime-live | native flag |
| Basis | code: `src/vizdoom/src/viz_message_queue.cpp` `VIZ_MQTic` (blocking receive unless async); docs `enums.md` ASYNC "without waiting for the agent actions"; late agent: last button state persists |

## Details

- Kempka, Wydmuch, Runc, Toczek, Jaskowski, 2016; Farama. [Repo](https://github.com/Farama-Foundation/ViZDoom) (MIT); [competitions paper](https://arxiv.org/abs/1809.03470).
- `PLAYER` mode waits for the agent (paused-live). `ASYNC_PLAYER` advances at 35 tics/s without waiting; a slow agent misses frames. The tic rate can be changed, and the README lists time scaling in async mode, so the clock can be slowed for slow agents. The Visual Doom AI Competitions ran in async mode, so realtime play has been standard here since 2016. On missed tics the last button state persists: the engine polls the message queue without blocking in async mode (`viz_message_queue.cpp` `VIZ_MQTic`) and button state set by `setAction` carries over.
- Observation: screen, depth, labels (object segmentation), audio buffer, game variables. Each can be switched on separately. Action: button vectors and mouse deltas.
- Tasks: scenario WADs such as basic, defend_the_center, health_gathering, take_cover (from the bundled `scenarios/*.cfg`); custom scenarios are scriptable. Episodes last seconds.
- LLM use: "Will GPT-4 Run DOOM?" (paused; see [Will GPT-4 Run DOOM](will-gpt-4-run-doom.md)); Game-TARS reports ViZDoom results (figures only); "Playing DOOM with 1.3M Parameters" ([arXiv 2604.07385](https://arxiv.org/abs/2604.07385)) reports a tiny classifier at 31 ms beating LLMs on defend_the_center (all agents, LLMs included, ran in ViZDoom `Mode.PLAYER`, `scripts/benchmark.py:95`, so the game waited for each LLM call; latency was measured, 0.6-13 s per decision, but not charged).
- DeepMind Lab: ViZDoom covers the same ground.
- Shortlist rank 3 (ViZDoom basic scenarios in `ASYNC_PLAYER`): native 35 tics/s wall clock with adjustable tic rate, MIT, seconds-long episodes, and separately switchable pixel, depth, label, audio and game-variable channels, which suits multi-channel input experiments. Sweep the tic rate to get a score-versus-speed curve.

## Demo

- [project-page] [ViZDoom docs](https://vizdoom.farama.org/) — Read the home, Default scenarios, Enums and APIs/wrappers pages and inspected the header GIF and DeadlyCorridor GIF frames. Documentation only: no playable game, replay viewer or agent videos. The header GIF (75 frames) shows four synchronized buffers from one corridor run (screen, labels such as DoomPlayer / Zombieman / ChaingunGuy, depth, automap); the scenarios page has 24 short looping GIFs (about 44 frames each) with no caption saying who plays. Play-mode evidence (docs text): the Enums page says PLAYER and SPECTATOR modes wait for the agent action while ASYNC modes run at a constant 35 tics/s by default (set_ticrate) without waiting.
- [dead-or-unreachable] [Original ViZDoom website](https://vizdoom.cs.put.edu.pl/) — Tried the site linked from the docs (formerly hosting the 2016-2018 Visual Doom AI Competition pages and videos) and its competition subpage: page load timed out / ERR_CONNECTION_TIMED_OUT, and earlier ERR_NAME_NOT_RESOLVED over http.
- [live-model] [Tiny Doom Defender HF Space (third-party)](https://anakin87-tiny-doom-defender.hf.space/) — Watched it live for about 24 s, sampling counters every 4 s; read app.js and the /stats Server-Sent Events stream. Two small models play Defend the Center on the same seed side by side: SauerkrautLM-Doom-MultiVec-1.3M (ASCII + depth input) and tiny-doom-defender (1.1M ModernBERT, pixel input, SFT then PPO), each with an MJPEG feed, kills, step counter, current action and mean kills per episode. The episode counter was about 93,342; over 20 s episode 93342 went from step 6 to 129 (Sauerkraut) and 7 to 148 (tiny), about 6-7 steps/s each at different rates. Play-mode evidence (live): frames are server-generated MJPEG streams and /stats pushes step, action and kills per step; the differing step rates fit synchronous stepping per model decision, but the page does not say whether PLAYER or ASYNC_PLAYER mode is used and shows no latency. These are ~1M-parameter encoder classifiers, not LLMs; spectator view only.

Visited 10 November 2026 in a headless browser.

## Fit

5 of 5. The strongest all-round base among classic platforms.

Related: [Will GPT-4 Run DOOM](will-gpt-4-run-doom.md); [Game-TARS](game-tars.md); [DeepMind Lab](deepmind-lab.md); [Game-TARS](../solutions/game-tars.md)
