# gpt-realtime-2 (Realtime API)

gpt-realtime-2 is OpenAI's Realtime API model, with reasoning-effort levels and harness turn detection.

| | |
|---|---|
| Year | 2026 |
| Links | [docs](https://developers.openai.com/api/docs/models/gpt-realtime-2) |
| Demo | [gpt-realtime-2 docs](https://developers.openai.com/api/docs/models/gpt-realtime-2): the official Realtime Playground needs sign-in (Cloudflare check), the launch post's embedded voice session was blocked by a bot check, and the [Realtime Console](https://github.com/openai/openai-realtime-console) is self-hosted with your own key. No public game-playing demo; human-playable: no. |
| Category | realtime architecture |
| Method | Reasoning-effort levels; higher effort raises latency |
| Evaluation play mode | realtime-live (speech) service; no game evaluation by the vendor |
| Open source | API only, no fine-tuning |
| Basis | docs: model page, VAD guide (`server_vad` / `semantic_vad`), prompting guide (reasoning effort); fine-tuning "Not supported" |
| Channels (in / out) | text, audio, images / text, audio |
| Tick | harness turn detection |

## Details

- **Realtime APIs.** In the OpenAI Realtime API and Gemini Live, interactivity is largely in the harness (voice activity detection, turn detection), not learned full duplex. In Realtime-Bench, GPT-Realtime-2 scores 12-18% and Gemini 3.1 Flash Live 6-18% under wall clock: quick but not good enough. Proactive audio is configurable on Gemini 2.5 Flash Live, permanently on for the 3.8 Live models and not supported on 3.1 Flash Live Preview (Live API capabilities guide, saved).

## Demo

- [project-page] [gpt-realtime-2 model page](https://developers.openai.com/api/docs/models/gpt-realtime-2) — Loaded the catalog page: a speech-to-speech reasoning model with configurable reasoning effort (higher effort can increase latency), 128k context, $4/$24 text and $32/$64 audio per 1M tokens, endpoints v1/realtime and v1/live/sessions, and a "Try in Playground" link. No video, iframe or game content.
- [dead-or-unreachable] [OpenAI Realtime Playground](https://platform.openai.com/playground/realtime) — Showed a Cloudflare "Verify you are human" check; it needs an OpenAI login and API credits, so it was not used and no play-mode evidence was gathered.
- [dead-or-unreachable] [gpt-realtime-2 launch post](https://openai.com/index/advancing-voice-intelligence-with-new-models-in-the-api/) — A Cloudflare bot check ("Just a moment...") blocked the headless browser and it was not bypassed. Search results say it embeds a "Try GPT-Realtime-2" voice session, a conversational voice chat, not game play.
- [project-page] [OpenAI Realtime Console](https://github.com/openai/openai-realtime-console) — Read the README: a local starter console (WebRTC event log, client-side function calling) that needs your own API key; no hosted public instance and no game.

Visited 10 November 2026 in a headless browser.

## What the team could reuse

- Baselines for the "interaction/realtime models" column: gpt-realtime-2 through its API. Game pixels must be pushed as frames, and actions must be parsed from text or speech.

Related: [Realtime-Bench](../environments/realtime-bench.md); [Gemini Live](gemini-live.md)
