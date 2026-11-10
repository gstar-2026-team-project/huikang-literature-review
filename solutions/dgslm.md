# dGSLM

dGSLM is a textless model over two audio channels.

| | |
|---|---|
| Year | 2022 |
| Links | [arXiv 2203.16502](https://arxiv.org/abs/2203.16502) |
| Demo | [audio samples page](https://speechbot.github.io/dgslm/): official project page with pre-generated stereo audio samples (prompt, ground truth, dGSLM continuations, cascaded baseline, unconditional generations) shown as two-channel waveforms. Recordings only; no live model and nothing to talk to. |
| Category | realtime architecture |
| Method | none (textless) |
| Evaluation play mode | static |
| Open source | research |
| Basis | paper §4.3.2: 90-second continuations of 30-second prompts |
| Channels (in / out) | two audio channels |
| Tick | units |

## Demo

- [project-page-audio] [Generative Spoken Dialogue Language Modeling samples](https://speechbot.github.io/dgslm/) (linked as "[Paper] [Code] [Blog]" to the arXiv PDF, fairseq `examples/textless_nlp/dgslm` and the Meta AI blog) — Opened the page, clicked Play and seeked the dGSLM continuation player. "Conditional Examples" has 2 rows of wavesurfer stereo waveforms (one channel per speaker) with columns "Prompt", "Ground Truth", "dGSLM (Continuation 1)", "dGSLM (Continuation 2)", "Cascaded Continuation"; the page says "You will hear a ding sound at the end of the prompt duration". Measured durations: prompt 5.3 s, each continuation 30.0 s; seeking to 25 s and playing advanced to 29.0 s. "Unconditional Examples" has two 60.0 s clips (`audio/uncond_generation/Generation_1.wav`, `Generation_2.wav`). A further table "Conditional Samples from All Algorithms" has 49 rows (ID 0-48) of PLAY buttons for DLM5 (dGSLM), DLM4-DLM1, MS-TLM and Cascaded, served from `dl.fbaipublicfiles.com/textless_nlp/dgslm/samples/stereo/...` (checked one file: HTTP 200, audio/x-wav). Play-mode evidence (recorded): every sample is a static .wav (e.g. `audio/stereo/dGSLM/fe_03_11522_1s_5s_CONTINUATION2.wav`); no model calls on the network, no interactive or full-duplex live session. It shows offline generation of simultaneous two-channel speech with overlaps and laughter, consistent with the static label.
- Note: the samples page uses short prompts (about 5-10 s, per file names such as `fe_03_11501_63s_73s`) with 30 s continuations, while the Basis row cites 90-second continuations of 30-second prompts (paper §4.3.2); the page clips are illustrative, not the evaluation setting.

Visited 10 November 2026 in a headless browser.
