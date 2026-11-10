# Latent Bridge

Latent Bridge links a frozen fast VLM at 15 Hz and a frozen slow VLM at 1 Hz with a trained latent channel.

| | |
|---|---|
| Year | 2026 |
| Authors / org | Li, Shi |
| Links | [arXiv 2606.24470](https://arxiv.org/abs/2606.24470), [code](https://github.com/19PINE-AI/latent-bridge-games) |
| Demo | [site](https://01.me/research/latent-bridge-games/): pre-rendered side-by-side MP4 replays (F/T/L) for 7 Atari games plus MetaDrive, with burned-in tick/action/score and slow-model guidance overlays, a 3:46 narrated video and interactive result charts; the recorded runs come from a lockstep loop in which the emulator waits for the fast model and blocks on the slow model every 15 ticks (code: [GitHub](https://github.com/19PINE-AI/latent-bridge-games)); human-playable: no. |
| Category | scaffold |
| Method | Frozen fast VLM at 15 Hz + frozen slow VLM at 1 Hz, linked by a trained latent channel |
| Evaluated on | 7 Atari games |
| Evaluation play mode | paused-live (synchronous tick loop; slow model every 15 ticks) |
| Results | Wins on 2 of 7 games against a text bridge |
| Basis | code: `src/eval/benchmark.py:110-186` (`fast.predict_action` -> `env.step` -> inline `slow.emit`), `src/env/atari_wrapper.py` 4 frames per tick |

## Details

- **Latent Bridge** (Li, Shi; [code](https://github.com/19PINE-AI/latent-bridge-games)). MiniCPM-o 4.5 acts each 67 ms tick; Qwen3-VL-8B-Thinking deliberates at about 1 Hz and its latest output is reused for about 15 ticks. Only a 33M-parameter MLP mapping slow-model residuals to 8 soft tokens is trained. Headline scores use an uncached path of about 157 ms per tick, and in the released benchmark the emulator waits for the fast model: `src/eval/benchmark.py` runs a synchronous tick loop (fast prediction, then `env.step` of 4 frames) and calls the slow model's `emit()` inline every 15 ticks, so the 15 Hz and 1 Hz rates are tick ratios, not wall-clock (paused-live). The paper's statement that "the fast loop never blocks" on the slow model holds only in tick terms. Scores are far below RL and human levels (MsPacman 628). Honest negative results on 5 of 7 games.
- MiniCPM-o 4.5 is the fast model in Latent Bridge.

## Demo

- [replay-viewer] [Latent Bridge games site](https://01.me/research/latent-bridge-games/) — Seeked the 3:46 narrated video (combined_narrated.mp4) to 7 timestamps, read its SRT, clicked the 'Watch it play' tabs (Road Runner, Ms. Pac-Man, MetaDrive) and 'Replay all three', and seeked per-strategy clips (roadrunner_T.mp4 at 1/2/4/20 s, mspacman_L.mp4 at 3/15 s). The site shows pre-rendered side-by-side F (fast-only), T (text bridge) and L (latent bridge) MP4s for 7 Atari games plus MetaDrive, each with a burned-in 'game / tick N / action=K / score=S' header and a 'slow-model guidance' panel, plus state snapshots, emissions, result charts (T>F predictor r=0.93), system prompts and a latency table (F about 33 ms/decision, L about 38 ms per fast tick, slow 1.5 s). Play-mode evidence (recording): requests are only static demos/*.mp4 files and one JS bundle, the button reads 'Pre-rendered 3-up', and nothing is playable; ticks advance about 12 per second of video (Ms. Pac-Man L at tick 180 at 0:15), and at tick 49 T and L already show slow-model text while F shows '(no emission yet)'. The site says "The fast loop never blocks on the slow model".
- [project-page] [GitHub repo](https://github.com/19PINE-AI/latent-bridge-games) — Read the README and inspected src/eval/benchmark.py and src/env/atari_wrapper.py. Code for Stage A/B/C training and F/T/L evaluation; checkpoints not shipped; the README mentions an optional local Flask/SSE live server but no hosted instance exists. Play-mode evidence (code): env.step() runs only after fast.predict_action returns, and slow.emit() runs inline every 15 ticks (TEXT_STATE_EVERY_N_TICKS = 15), so the emulator waits for both models; '15 Hz / 1 Hz' is counted in game ticks, slow output is used from the next tick, and per-tick latency and an 'on-clock fraction' (67 ms budget) are logged as metrics only.
- Note: the file labels play mode as paused-live (synchronous tick loop), which matches the repo code, but the project site states "The fast loop never blocks on the slow model" (synchronous ~15 Hz / asynchronous ~1 Hz), which the recorded runs' lockstep code does not do.

Visited 10 November 2026 in a headless browser.

Related: [ALE / Atari](../environments/ale-atari.md) (evaluated on); [MiniCPM-o 4.5](minicpm-o-4-5.md)
