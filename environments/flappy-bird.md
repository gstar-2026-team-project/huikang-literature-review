# Flappy Bird (flappy-bird-gymnasium)

Flappy Bird in flappy-bird-gymnasium is a tiny one-button game with text-serialisable state.

| | |
|---|---|
| Year | 2016- |
| Links | [flappy](https://github.com/markub3327/flappy-bird-gymnasium) |
| Demo | [README GIF](https://github.com/markub3327/flappy-bird-gymnasium/blob/main/imgs/dqn.gif): official recorded GIF of the bundled DQN agent playing (score counter past 200). A recording, not an LLM and not a running-clock evaluation; human play is local only (`flappy_bird_gymnasium` command), no web-playable page. |
| Play mode | paused-live (Dino browser is realtime-live) |
| Clock | STEP at about 30 fps |
| Observation | numeric state or pixels |
| Action | 1-few buttons |
| Players | 1 |
| Horizon | seconds |
| Human reference | easy |
| Open source | MIT |
| Convertible to realtime-live | high |
| Basis | code: flappy-bird-gymnasium `flappy_bird_env.py` `step` (render_fps 30) |

## Details

- **Flappy Bird** ([flappy-bird-gymnasium](https://github.com/markub3327/flappy-bird-gymnasium)), **PLE**, **MinAtar**, **PyBoy**: tiny, text-serialisable state, one or two buttons. Ideal for latency-versus-score curves.
- Shortlist rank 4: part of the small arcade suite on a three-clock wrapper (with Atari, V-MAGE games and SuperTux 1-1; see [ALE / Atari](ale-atari.md)).

## Demo

- [video/GIF] [README DQN GIF](https://github.com/markub3327/flappy-bird-gymnasium/blob/main/imgs/dqn.gif) — rendered the repo page and screenshotted the looping GIF at several moments, and downloaded the file (`imgs/dqn.gif`, 576x1020, 246 frames, 20 ms frame delay); shows the bundled Deep Q Network agent flying through pipes with the on-screen score at "201". Play-mode evidence (recording): a pre-trained RL agent, not an LLM, and no timing or step readout; it says nothing about how the env would behave under a wall clock. The README "Playing" section offers human play (`flappy_bird_gymnasium`), random (`--mode random`) and DQN (`--mode dqn`) modes, but only as a local pygame window; no project page, hosted playable page or Hugging Face Space was found (`gh api` homepage field is empty).

Visited 10 November 2026 in a headless browser.

Related: [PLE](ple.md); [Chrome Dino](chrome-dino.md); [MinAtar](minatar.md); [PyBoy](pyboy.md)
