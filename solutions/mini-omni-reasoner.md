# Mini-Omni-Reasoner

Mini-Omni-Reasoner interleaves reasoning with spoken output in a speech LLM.

![Mini-Omni-Reasoner demo streaming its spoken response and inner thoughts side by side](../assets/gifs/sol-mini-omni-reasoner.gif)

*Screen recording (cropped, real speed) of the official demo answering an uploaded spoken math question: the "Response" text and the "Inner Thoughts" reasoning stream in together after a 0.267 s response time. Source: [Mini-Omni-Reasoner README demo video](https://github.com/xzf-thu/Mini-Omni-Reasoner#demo).*

| | |
|---|---|
| Year | Aug 2025 |
| Links | [arXiv 2508.15827](https://arxiv.org/abs/2508.15827) |
| Demo | [README demo video](https://github.com/xzf-thu/Mini-Omni-Reasoner#demo): a 40 s official screen recording of a Streamlit-style UI answering one uploaded spoken math question, with the spoken "Response" and the "Inner Thoughts" reasoning shown side by side. A recording, not a live demo, and no game. |
| Category | realtime architecture (thinking while speaking) / post-training |
| Method | interleaved or latent reasoning |
| Evaluated on | spoken QA |
| Evaluation play mode | realtime-live (speech) |
| Basis | Mini-Omni-Reasoner §4.4 (Spoken-MQA) |
| What is trained | speech LLMs |

## Details

- **Thinking while speaking** (STITCH [arXiv 2507.15375](https://arxiv.org/abs/2507.15375), SHANKS [arXiv 2510.06917](https://arxiv.org/abs/2510.06917), Mini-Omni-Reasoner [arXiv 2508.15827](https://arxiv.org/abs/2508.15827), FLAIR [arXiv 2603.17837](https://arxiv.org/abs/2603.17837)). Reasoning chunks are interleaved with spoken chunks, or generated while the user is still talking, so reasoning costs no extra latency. Speech only.

## Demo

- [official video] [README demo video](https://github.com/xzf-thu/Mini-Omni-Reasoner#demo) (GitHub user-attachment b5455d9a-…, .mov, 39.9 s, 1942x1080; README note "need to unmute first") — played it muted and screenshotted frames at 6, 14, 22, 30 and 38 s. It is a screen recording of a demo UI ("Controls", "Upload your audio file", "Send and Run"): sample.wav (171.8 KB) is uploaded, the page shows "Mini-Omni-Reasoner - Response in 0.267s", and the "Response" column ("…Jerry is 10 years old now, so in three years, he'll be 13.") appears next to an "Inner Thoughts" column with the LaTeX reasoning (j = 2(j − 5), j = 10, 10 + 3 = 13). The video ends on a title slide with the paper title and authors. Play-mode evidence: a recording of one single-turn spoken QA, with the 0.267 s response latency shown on screen. No running clock, no game and no interaction. The README Quickstart still says "Coming soon", and there is no Hugging Face Space or live demo.

Searched the arXiv abstract (comments link only to the GitHub repo), the repo README and homepage field (empty), and the web. Visited 10 November 2026 in a headless browser.

Related: [STITCH](stitch.md); [SHANKS](shanks.md); [FLAIR](flair.md)
