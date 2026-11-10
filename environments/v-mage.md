# V-MAGE

V-MAGE is a set of five pygame-style games with 30+ levels, played from pixels with explicit frame-pausing during inference.

| | |
|---|---|
| Year | 2025 |
| Authors / org | Zheng et al. (CSU-JPG) |
| Links | [arXiv 2504.06148](https://arxiv.org/abs/2504.06148), [repo](https://github.com/CSU-JPG/V-MAGE) (no licence stated) |
| Demo | [project page](https://csu-jpg.github.io/V-MAGE/): recorded GIF clips of GPT-4o, Gemini 2.0 Flash and Qwen2.5-VL-72B playing SuperMario, Race and FlappyBird, plus an Elo leaderboard. [Playground](https://huggingface.co/spaces/Fengx1nn/V-MAGE-DEMO) and [Eval demo](https://huggingface.co/spaces/Fengx1nn/V-MAGE-EVAL-DEMO) HF Spaces are asleep (the project page's own Space links return 404). Their code shows play advances one step at a time: the game waits for each human or model action, then runs N frames. Human-playable: yes when awake (button-driven, not real-time). |
| Play mode | paused-live |
| Clock | explicit frame pausing |
| Observation | pixels (3 frames) |
| Action | discrete keys |
| Players | 1 |
| Horizon | short levels |
| Human reference | 5 players |
| Open source | open repo, no licence stated |
| Convertible to realtime-live | high |
| Basis | code: `game/pygame_base.py` (game stepped only when `new_action_event` is set); paper §3 "the game is paused while the model processes the visual inputs" |

## Details

- Zheng et al. (CSU-JPG), [arXiv 2504.06148](https://arxiv.org/abs/2504.06148); [repo](https://github.com/CSU-JPG/V-MAGE) (no licence stated).
- Five pygame-style games, 30+ levels: FlappyBird, RaceGame, SuperMario, PongGame, Tempest Run. Pixels only. Explicit frame-pausing during inference; frames skipped per request is tunable. Human baseline from five participants. Models are far below humans even when paused (Race level 4: GPT-4o 22.9 against human 100).
- Convertibility: very good. Small Python games with their own frame loop. Because models are near random when paused, unpausing mainly adds a floor effect unless the game is slowed.
- Shortlist rank 4: part of the small arcade suite on a three-clock wrapper (with Atari, Flappy Bird and SuperTux 1-1; see [ALE / Atari](ale-atari.md)).

## Demo

- [project-page] [V-MAGE project page](https://csu-jpg.github.io/V-MAGE/) — Loaded the page (first try hit a DNS error, reload worked) and downloaded 3 of its 9 'Game Demos' GIFs (GPT4o SuperMario-LV1, GPT4o Race-merged, Qwen2.5VL-72B FlappyBird-LV7) to inspect frames. The page has a 3x3 GIF grid of GPT-4o, Gemini 2.0 Flash and Qwen2.5VL-72B on SuperMario-LV1, Race-merged and FlappyBird-LV7, captioned 'Game playing examples of MLLMs sampled from the evaluation process', plus an Elo leaderboard (top GPT-5-2025-08-07 at Elo 1710 and 43.4% of human; Random 1426). Play-mode evidence (recording): the GIFs (37 to 314 frames, no per-frame delay) are stitched game-step screenshots with no timestamps or latency; the Mario frame shows the in-game TIME counter at 002. Nothing is interactive.
- [dead-or-unreachable] [V-MAGE-Playground Space](https://huggingface.co/spaces/Fengx1nn/V-MAGE-Playground) — The project page's 'Playground' button links here; it returns a Hugging Face 404 (HF API 401). The live Space is Fengx1nn/V-MAGE-DEMO.
- [dead-or-unreachable] [V-MAGE-Evaluation Space](https://huggingface.co/spaces/Fengx1nn/V-MAGE-Evaluation) — The project page's 'Evaluation' button links here; it returns a Hugging Face 404. The live Space is Fengx1nn/V-MAGE-EVAL-DEMO.
- [dead-or-unreachable] [V-MAGE-DEMO Space](https://huggingface.co/spaces/Fengx1nn/V-MAGE-DEMO) — Found via the HF API; the Space is sleeping ('This Space is sleeping due to inactivity', hf.space returns 503) and was not restarted, so nothing was played. Per its public app.py, run_game.py and game/pygame_base.py, it is a Gradio app where a human picks a game (RaceGame, SuperMario, FlappyBird, TempestRun, PongGame) and level and sends actions with buttons; the screen refreshes every 0.5 s. Play-mode evidence (code): the main loop advances only after an action arrives via new_action_event or a pygame key, runs sample_frames frames, then logs 'waiting for action.' and waits again, so the game clock stops while waiting for input.
- [dead-or-unreachable] [V-MAGE-EVAL-DEMO Space](https://huggingface.co/spaces/Fengx1nn/V-MAGE-EVAL-DEMO) — Found via the HF API; runtime stage SLEEPING and hf.space returns 503, so it was not run. Per app.py it is a Gradio UI with Game, Level, 'Sample Rate (Frames/Action)' (default 3), Model Name / Base URL / API Key fields, manual action buttons and a history panel; a 'Model Inference' button is labelled 'Press to let the model execute the next action'. Play-mode evidence (code): one model action per button press with the same game loop, so the game stays frozen during inference and then advances N sample frames.

Visited 10 November 2026 in a headless browser.

## Fit

Fit after conversion: 5 of 5.
