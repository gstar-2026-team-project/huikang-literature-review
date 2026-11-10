# LiveCC

LiveCC is a streaming video LLM.

| | |
|---|---|
| Category | realtime architecture (streaming video LLM) |
| Demo | [project page](https://showlab.github.io/livecc/) with a 2:07 teaser video of recorded LiveCC-7B-Instruct commentary on streamed videos (whiteboard recording, NBA, how-to, Dota 2, SpaceX), with a "Video Time" overlay; the [Hugging Face Space](https://huggingface.co/spaces/chenjoya/livecc) live demo is paused. Recording only; the model watches and comments but does not play. |

## Details

- **Streaming video LLMs** (VideoLLM-online, Flash-VStream, Dispider, StreamBridge, LiveCC, StreamingVLM, OmniMMI/M4, Proact-VL). The only "action" is when to speak. Evaluations replay recorded video and mostly score offline.

## Demo

- [official video] [LiveCC project page](https://showlab.github.io/livecc/) — Opened the page, played and seeked the teaser video (teaser.mp4, 127 s) and screenshotted frames at 0:10, 1:15 and 1:35. The video is captioned "📷 Recording | 🏀 NBA Playoffs (Apr 21) | 🛠️ How-To | 🎮 Dota2 7.38c (Mar 27) | 🚀 SpaceX (Apr 21)" and "(Note: The video's original audio has been muted)". Each segment carries an overlay such as "Video Time: 16.1s | Model: LiveCC-7B-Instruct" with streaming commentary words ("decreased from 900 ..." over a Dota 2 teamfight; "inside of the laptop. ..." over a how-to clip). Play-mode evidence: a pre-recorded video of the model commenting along a video timestamp; the model only produces commentary and takes no game actions, so the Dota 2 segment is spectating, not playing.
- [live demo, unavailable] [Hugging Face Space chenjoya/LiveCC](https://huggingface.co/spaces/chenjoya/livecc) — Linked from the repo README as "Demo"; the page shows "This Space has been paused." so it could not be used. The README describes it as a Gradio app (`python demo/app.py --js_monitor`) that monitors the video timestamp to stream commentary.

Visited 10 November 2026 in a headless browser.

Related: [VideoLLM-online](videollm-online.md); [Dispider](dispider.md)
