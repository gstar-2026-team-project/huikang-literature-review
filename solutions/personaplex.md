# PersonaPlex

PersonaPlex is NVIDIA's follow-up to Moshi with role and voice conditioning.

| | |
|---|---|
| Year | 2026 |
| Authors / org | NVIDIA |
| Links | [arXiv 2602.06053](https://arxiv.org/abs/2602.06053) |
| Demo | [project page](https://research.nvidia.com/labs/adlr/personaplex/) (linked as "Demo" from the GitHub README): a 43 s intro video of a recorded live voice chat and five recorded stereo conversation clips (assistant, banking, medical reception, backchanneling, space emergency). These are recordings, not a hosted live demo; the repo's Web UI for live talk has to be self-hosted on a GPU with gated weights. |
| Category | realtime architecture |
| Method | as Moshi |
| Evaluation play mode | realtime-live (speech) |
| Open source | Weights released under the NVIDIA Open Model License (gated; HF API metadata and repo README) |
| Basis | paper §2: "user input audio is streamed in and the model's corresponding generated audio is captured and evaluated" |
| Channels (in / out) | as Moshi + role and voice prompts |
| Tick | 80 ms |

## Details

- Follow-up to Moshi: PersonaPlex (NVIDIA; role and voice conditioning).

## Demo

- [project page with video and audio] [NVIDIA ADLR PersonaPlex page](https://research.nvidia.com/labs/adlr/personaplex/) — Opened it, played the intro video (personaplex-intro.mp4, 43.1 s) and seeked to 0:30, and loaded the five example clips. The video, captioned "PersonaPlex and Rajarshi Roy sharing jokes.", shows a live voice-chat UI with "NVIDIA PersonaPlex" and "User" audio meters and a text panel ("What do you call a fake noodle?"). The "Examples" section has waveform players for static MP3s: assistant.mp3 (0:26, from "FullDuplexBench's interruption evaluation"), bank.mp3 (0:55), medical.mp3 (1:13), backchannel.mp3 (0:17) and astronaut.mp3 (3:19, "Space Emergency Scenario"). Each shows its text prompt, and the page says "you can hear the user speaking in the left channel and PersonaPlex in the right channel". Play-mode evidence (recordings): these are conversations recorded in real time, with overlapping speech, interruptions and backchannels against a running audio stream. Network traffic showed only static MP4/MP3 files and no model calls. The live Web UI in the [GitHub repo](https://github.com/NVIDIA/personaplex) is self-hosted ("Launch server for live interaction") and needs the gated Hugging Face weights, so it is not a public hosted demo. Speech conversation only, not a game.

Visited 10 November 2026 in a headless browser.

## What the team could reuse

- Baselines for the "interaction/realtime models" column: Moshi/PersonaPlex locally (from the architectures reuse list).

Related: [Moshi](moshi.md); [Kyutai interactivity alignment](kyutai-interactivity-alignment.md)
