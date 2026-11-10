# MiniCPM-o 4.5

MiniCPM-o 4.5 is a 9B model on a Qwen3-8B backbone that uses time-division multiplexing on a shared time axis with a listen/speak control token per window.

| | |
|---|---|
| Year | 2026 |
| Authors / org | OpenBMB |
| Links | [arXiv 2604.27393](https://arxiv.org/abs/2604.27393) |
| Demo | [live demo](https://minicpmo45.modelbest.cn/omni) (camera + mic or uploaded file, full-duplex over a WebSocket to the running model, one listen/speak decision about every second) and [omni cases page](https://openbmb.github.io/minicpm-o-4_5-omni/) of recorded real-world videos (elevator/subway reminders, street walk, building blocks); also an official [YouTube video](https://www.youtube.com/watch?v=6UzC-O1Q-1U). Nothing shows the model playing a game. |
| Category | realtime architecture |
| Method | Listen/speak control token per window; no reasoning stream |
| Evaluation play mode | offline replay (LiveSports-3K-CC); static elsewhere |
| Open source | Open, Apache-2.0 per model card |
| Basis | paper §6.1 LiveSports-3K-CC "an audio-free full-duplex benchmark"; model card "decides at a frequency of 1Hz to speak or not" |
| Channels (in / out) | video, audio, text / text, speech |
| Tick | 1 s windows |

## Details

- **MiniCPM-o 4.5** (OpenBMB). 9B, Qwen3-8B backbone. Time-division multiplexing on a shared time axis; the paper ablated 1.0 s, 0.2 s and 0.1 s windows and chose 1.0 s because shorter windows hurt quality. First-token latency about 0.58 s on an RTX 4090. The best open candidate with vision, but worst-case reaction above one second is slower than a human. It is the fast model in Latent Bridge.

## Demo

- [live-demo] [MiniCPM-o 4.5 Omni Full-Duplex](https://minicpmo45.modelbest.cn/omni) (linked as "Live demo" from the [OpenBMB/MiniCPM-o](https://github.com/OpenBMB/MiniCPM-o) README) — No sign-in is needed. I started a Live session with Chrome's fake camera (a green test pattern with a running timecode) and a fake mic, ran it for about 20 s, then pressed Stop. It shows the camera feed, a mic waveform, presets ("English Call", "中文通话", "MBTI 分析师"), length-penalty and vision-HD settings, and a Conversation log ("Session created: sess_25e4a28977f6", "Live: mic=AudioWorklet@16000Hz, cam=back"). Play-mode evidence (live model): the page opens `wss://api.modelbest.cn/v1/realtime?mode=video&...&model=MiniCPM-o-4.5-Realtime`; the server replied `session.created` with `"mode":"full_duplex"`, then sent about one `response.output.delta` with `"kind":"listen"` per second while the session ran. Each one added 79 tokens to the KV cache (85, 162, 241 ... 1663), with `generate_ms` of about 3-12 ms. Faced with a silent test pattern, the model kept choosing listen and never spoke. This matches the 1 s window with a listen/speak token. The FAQ says File mode accepts a local video or audio file instead of the camera. No game is offered.
- [video] [Omni Cases page](https://openbmb.github.io/minicpm-o-4_5-omni/) — I played and seeked "Elevator Arrival Reminding" (`videos/proactive_visual_01.mp4`, 0:36) to 0:10, 0:19, 0:28 and 0:36: a handheld phone view of an elevator floor display, then a window view. Other tabs are "Subway Arrival Reminding", "Air Fryer Ding Reminding", "Shopping Mall Companion", "Street Walk Companion", "Building Blocks" (real-time captioning and memory) and four voice-clone cases. Play-mode evidence (recording): the disclaimer says "All AI responses in the videos are generated in real-time by the model"; these are screen recordings of live sessions, not games. A sibling [Audio Cases page](https://openbmb.github.io/minicpm-o-4_5/) has recorded voice role-play and dialogue mp3 clips.
- [video] [official YouTube demo](https://www.youtube.com/watch?v=6UzC-O1Q-1U) — The README links it as "the MiniCPM-o 4.5 full-duplex multimodal interaction demo". I found the link but did not play it.

Visited 10 November 2026 in a headless browser.

## What the team could reuse

- Baselines for the "interaction/realtime models" column: MiniCPM-o 4.5 locally (from the architectures reuse list).
- Serialisation ideas for post-training a text model: a listen/act control token per window.

Related: [Latent Bridge](latent-bridge.md)
