# ALE / Atari

The Arcade Learning Environment (ALE) steps Atari 2600 games synchronously at 60 Hz with frameskip, and is highly convertible to realtime with a wrapper.

| | |
|---|---|
| Year | 2013 |
| Authors / org | Bellemare et al. 2013; Farama |
| Links | [docs](https://ale.farama.org/environments/) |
| Demo | [environment docs with gameplay GIFs](https://ale.farama.org/environments/): each game page has a short looping gameplay GIF (e.g. [Freeway](https://ale.farama.org/environments/freeway/)); a recording, not a model playing against a clock. A [WebAssembly page](https://ale.farama.org/wasm/) documents running ALE in the browser, but no hosted playable instance. |
| Play mode | paused-live |
| Clock | STEP, 60 Hz, frameskip 4 |
| Observation | pixels or RAM |
| Action | 18 discrete |
| Players | 1 |
| Horizon | minutes |
| Human reference | standard human scores |
| Open source | GPL-2.0 |
| Convertible to realtime-live | high (wrapper) |
| Basis | code: `src/ale/python/env.py` `step` "repeats action frameskip # of steps"; docs v5 frameskip=4, sticky 0.25 |

## Details

- ALE: Bellemare et al. 2013; Farama. [Docs](https://ale.farama.org/environments/). v5 environments use frameskip 4 and sticky actions 0.25. RGB or 128-byte RAM observations.
- Convertibility: high. Open source, microsecond step cost, 60 Hz native. Already run unpaused with RL: fixed action delays (Firoiu et al.) and Physical Atari. At 2 s latency a model misses 120 frames, so start with slow games (Freeway, Pong at reduced speed) or scale the clock and plot score against tick rate.
- Shortlist rank 4 (a small arcade suite on a three-clock wrapper: Atari (Freeway, Pong, Breakout), Flappy Bird, V-MAGE games, SuperTux 1-1): all open, short, single-player and human-easy, with human references (Atari human scores, V-MAGE players, speedrun records). Wrap with `rtgym` or the RealtimeGym harness and offer wall, token and paused clocks. Text-state variants (RAM, numeric features) allow a text-only model track alongside pixels.

## Demo

- [official-video] [ALE environments docs](https://ale.farama.org/environments/) — Opened the index (a gallery of game thumbnails, "See More Environments") and the [Freeway page](https://ale.farama.org/environments/freeway/); the per-game page embeds `_images/freeway.gif`, a 160x210 GIF of 301 frames at 50 ms each (about 15 s) showing the raw Atari screen with traffic moving and the chickens near the bottom. No caption names the policy; the score stays at 0, consistent with a random or idle agent. Play-mode evidence: a pre-recorded clip of the emulator output; nothing shows an agent acting under a clock.
- [docs] [WebAssembly (WASM) Support](https://ale.farama.org/wasm/) — Read the page: "Atari 2600 emulation directly in web browsers without any server-side components", via npm `@farama/ale-wasm`, with a downloadable "example html file" (`example.html`, loads a local `ale.js`, so it does not run from the docs site). Its sample game loop calls `ale.act(action)` once per `requestAnimationFrame`, so the browser build is stepped by the caller as in Python. No hosted playable demo found.

Visited 10 November 2026 in a headless browser.

## Fit

Fit after wrapper: 5 of 5 with capped episodes (first to 5 points in Pong, one life of Breakout).

Related: [Atari-GPT](atari-gpt.md); [Physical Atari](physical-atari.md); [DQN / Atari line](../solutions/dqn-atari.md); [Latent Bridge](../solutions/latent-bridge.md); [tmrl / rtgym](tmrl-rtgym.md)
