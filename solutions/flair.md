# FLAIR

FLAIR uses interleaved or latent reasoning in a speech LLM, evaluated on speech benchmarks and Full-Duplex-Bench.

| | |
|---|---|
| Year | 2025-26 |
| Links | [arXiv 2603.17837](https://arxiv.org/abs/2603.17837) |
| Demo | None found (searched: arXiv abstract page and comments ("Accepted by ICML 2026"), URLs in the paper PDF, ICML 2026 poster page, GitHub repository search, web search for FLAIR / "The Silent Thought" demo, code or project page) |
| Category | realtime architecture (thinking while speaking) / post-training |
| Method | interleaved or latent reasoning |
| Evaluated on | spoken QA |
| Evaluation play mode | realtime-live (speech) |
| Basis | FLAIR §4 (speech benchmarks, Full-Duplex-Bench) |
| What is trained | speech LLMs |

## Details

- **Thinking while speaking** (STITCH [arXiv 2507.15375](https://arxiv.org/abs/2507.15375), SHANKS [arXiv 2510.06917](https://arxiv.org/abs/2510.06917), Mini-Omni-Reasoner [arXiv 2508.15827](https://arxiv.org/abs/2508.15827), FLAIR [arXiv 2603.17837](https://arxiv.org/abs/2603.17837)). Reasoning chunks are interleaved with spoken chunks, or generated while the user is still talking, so reasoning costs no extra latency. Speech only.

## Demo

- None found. The arXiv page ("The Silent Thought: Modeling Internal Cognition in Full-Duplex Spoken Dialogue Models via Latent Reasoning") links no code, project page or audio samples, and its only comment is "Accepted by ICML 2026". The paper PDF links no repository or demo. The ICML 2026 poster page (icml.cc/virtual/2026/poster/62081) has slides but no video or demo link. GitHub and web searches turned up no repository, Hugging Face Space or audio demo page; one paper-tracking site lists the code as "TBD".

Searched 10 November 2026; no demo found.

Related: [STITCH](stitch.md); [SHANKS](shanks.md); [Mini-Omni-Reasoner](mini-omni-reasoner.md); [Full-Duplex-Bench](../environments/full-duplex-bench.md)
