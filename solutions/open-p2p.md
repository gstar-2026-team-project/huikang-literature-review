# Open-P2P

Open-P2P is a keyboard/mouse action model for 3D PC games that runs at 20 Hz on a consumer GPU.

| | |
|---|---|
| Year | 2026 |
| Links | [arXiv 2601.04575](https://arxiv.org/abs/2601.04575) |
| Demo | [project page](https://elefant-ai.github.io/open-p2p/): official recorded videos of the model playing commercial 3D games (16-game montage, a Roblox FPS match against a human, 150M-1.2B model comparison, instruction-following and action-conditioning ablations). Recordings of real-time play; no live model, replay viewer or human-playable page. |
| Category | RL and decision model |
| Method | 20 Hz on a consumer GPU |
| Evaluated on | 3D PC games |
| Evaluation play mode | realtime-live |
| Basis | code: repo README (Recap "executes inputs in real time"; < 50 ms end-to-end requirement); paper §3 "the model must operate in real time (20 Hz)" |

## Details

- **NitroGen** (about 500M parameters, vision to gamepad, 40,000 hours of video) and **Open-P2P** (150M-1.2B, 8,300 hours of labelled keyboard/mouse data, open code and checkpoints) are the ready "fast but will not think" baselines. OmniGameArena and Realtime-Bench already include decision models alongside frontier VLMs.

## Demo

- [project-page videos] [Open P2P project page](https://elefant-ai.github.io/open-p2p/) (the repo's homepage field and the paper link to it) — Rendered the page, played and seeked all five videos, and screenshotted mid-video frames. The first video, captioned "Direct footage of Open P2P interacting with commercial games in real-time." (`games_we_can_play.mp4`, 30 s, 1920x1080), is a 4x4 grid of 16 games: Roblox shooters and obbies, DOOM, Quake, a Need for Speed-style racer, and others. "AI Agent vs Human Player" (`highlight.mp4`, 112 s) shows a Roblox FPS duel; at 0:57 the in-game round timer read 0:53 with the score at 1-0. The caption says "Watch it to the end to see it exhibit real human like behaviour of switching to side-arm when it runs out of ammo". `model_comparison.mp4` (162 s) shows the 150M / 300M / 600M / 1.2B models side by side on nine game checkpoints (DOOM, Quake, Roblox), the human-judged evaluation set from paper §4.2. `instruct_comparison.mp4` (25 s) compares "Press the red button" with no instruction in Quake. `action_comparison.mp4` (32 s) compares conditioning on prior actions with not doing so, in DOOM. Play-mode evidence (recording): the in-game timers and HUDs run at normal game speed, which fits the realtime-live label (20 Hz inference against the running game). The network log showed only static mp4 files and no model calls. The page has no playable or live component. Model weights are at [huggingface.co/elefantai/open-p2p](https://huggingface.co/elefantai/open-p2p).

Visited 10 November 2026 in a headless browser.

Related: [NitroGen](nitrogen.md); [OmniGameArena](../environments/omnigamearena.md)
