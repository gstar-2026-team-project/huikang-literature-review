# stable-retro / Gym Retro

stable-retro (Gym Retro) steps console emulators one frame at a time at 60 Hz.

| | |
|---|---|
| Year | 2018 |
| Links | [repo](https://github.com/Farama-Foundation/stable-retro) |
| Demo | [video](https://www.youtube.com/watch?v=hkOcxJvJVjk): RetroArchAI screencast, 2025. A PyTorch model trained with stable-retro overrides one player's input in NHL94 and Virtua Fighter 32x, with the emulator running live against a human. RL net, not an LLM. Human-playable: yes, locally (not in browser). |
| Play mode | paused-live |
| Clock | STEP, 60 Hz |
| Observation | pixels, RAM vars |
| Action | console buttons |
| Players | 1 |
| Horizon | per level |
| Human reference | n/a |
| Open source | MIT + ROMs |
| Convertible to realtime-live | high |
| Basis | code: `stable_retro/retro_env.py` `step` "Advance one emulator frame" |

## Details

- Gym Retro replaced OpenAI Universe: it steps emulators synchronously with direct memory access instead of VNC, which removes exactly the realtime and remote-desktop parts (see [OpenAI Universe](openai-universe.md)).

## Demo

- [video] [RetroArch + pytorch models that can override player input](https://www.youtube.com/watch?v=hkOcxJvJVjk) — Watched frames at 0:40, 1:40, 2:20, 6:29 and 12:10 of the videogames.ai / MatPoliquin video (Jan 2025, 16:14; chapters NHL94 example 0:20, Virtua Fighter 32x 2:05, install, source code tour, build). Frames show the RetroArch window with the NHL94 setup menu ('Two - Head to Head', Montreal vs Pittsburgh) and Virtua Fighter with Akira vs Jacky, a 27-second round timer and 'PRESS START BUTTON'. Play-mode evidence (recording): the emulator runs at normal speed in RetroArch while a trained PyTorch model (stable-retro scripts) overrides one player's input against a human, so the game does not wait for the model; it is a small RL net, not an LLM, and nothing on screen shows latency.
- Note: the file labels play mode as paused-live (step advances one emulator frame), but the demo video shows a stable-retro-trained model playing in RetroArch with the emulator running live at normal speed against a human.

Visited 10 November 2026 in a headless browser.

Related: [OpenAI Universe](openai-universe.md); [gym-super-mario-bros](gym-super-mario-bros.md); [LMGame-Bench](lmgame-bench.md)
