# Full-Duplex-Bench (v1, v1.5, v2, v3)

Full-Duplex-Bench evaluates full-duplex spoken dialogue models by streaming user audio to them, pre-recorded in v1 / v1.5 and live multi-turn in v2 / v3.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2503.04721](https://arxiv.org/abs/2503.04721) |
| Demo | [FDB-v3 demo page](https://daniellin94144.github.io/FDB-v3-demo): results tables (Pass@1, latency 4.25-10.12 s, interrupt/filler rates) and recorded stereo user/agent audio for GPT-Realtime, Gemini 2.5/3.1 Live, Grok, Ultravox and Cascaded on 6 disfluent tool-use scenarios. Covers v3 only. Human-playable: no. |
| Play mode | realtime-live (speech), pre-recorded user audio streamed in |
| Clock | audio time |
| Basis | paper v1 Fig. 1: "We feed user audio streams to a full-duplex SDM, which produces time-synchronous output"; v1.5 §1 "simulates a live conversation by streaming pre-recorded user" audio |
| Year (full-duplex speech table) | 2025-26 |
| Play mode (full-duplex speech table) | realtime-live (speech), live multi-turn |
| Basis (full-duplex speech table) | paper v2 §2.2 "Streaming Interaction Framework"; v3 evaluates Gemini Live, GPT-Realtime and others on tool use during speech |
| Links (full-duplex speech table) | [arXiv 2510.07838](https://arxiv.org/abs/2510.07838), [arXiv 2604.04847](https://arxiv.org/abs/2604.04847) |

## Demo

- [replay-viewer] [Full-Duplex-Bench v3 demo page](https://daniellin94144.github.io/FDB-v3-demo) — Read the highlights, radar chart, main results table and disfluency/domain sections, and played the GPT-Realtime sample for the first E-Commerce example (merged_openai.wav, 43.3 s; reached 3.96 s) out of 42 audio elements. The table covers Tool Sel, Arg Acc, Pass@1, turn-take %, latency, interrupt % and filler % for GPT-Realtime, Gemini 2.5 Live, Gemini 3.1 Live, Grok, Ultravox and Cascaded (latency 4.25 s for Gemini 3.1 to 10.12 s for Cascaded); 6 scenarios (E-Commerce, Finance, Housing, Travel) each have 'User Input Only' plus one stereo recording per system (left user, right agent). Play-mode evidence (recording): static files such as audio/example_ecommerce_02/merged_openai.wav, no live model or microphone; the recordings come from live streaming sessions where user audio kept playing in real time, which the latency and interruption metrics measure.

Visited 10 November 2026 in a headless browser.

Related: [TML-Interaction-Small](../solutions/tml-interaction-small.md); [Kyutai interactivity alignment](../solutions/kyutai-interactivity-alignment.md); [Realtime-Venus](../solutions/realtime-venus.md); [Game-Time](game-time.md); [FLAIR](../solutions/flair.md)
