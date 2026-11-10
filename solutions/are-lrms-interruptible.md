# Are LRMs Interruptible? (interruptibility diagnostic)

"Are LRMs Interruptible?" is a diagnostic that injects interrupts and context updates mid-reasoning.

| | |
|---|---|
| Year | 2025 |
| Authors / org | Wu et al., Berkeley |
| Links | [arXiv 2510.11713](https://arxiv.org/abs/2510.11713), [code](https://github.com/dynamic-lm/interrupt-lrm) (Apache-2.0) |
| Demo | [project page](https://dynamic-lm.github.io/): static paper site with result plots, an animated results figure, and viewers that show saved reasoning traces with and without interruption (interruptions inserted offline at fixed fractions of a precomputed trace, no live model); [dataset](https://huggingface.co/datasets/dynamic-lm/update-interrupt-benchmark) and [code](https://github.com/dynamic-lm/interrupt-lrm). It has no game environment. Human-playable: no. |
| Category | scaffold |
| Method | Diagnostic: interrupts and context updates mid-reasoning |
| Evaluated on | math and code QA |
| Evaluation play mode | static |
| Results | Up to 60% accuracy drop |
| Open source | Apache-2.0 |
| Basis | paper §3: "we primarily use relative cut points" in the reasoning trace; GSM-8K, Math-500, AIME, LiveCodeBench |

## Details

- **Interruptibility diagnostic** (Wu et al., Berkeley, ICML 2026; [code](https://github.com/dynamic-lm/interrupt-lrm), Apache-2.0). Hard interrupts, "answer faster" requests, and context updates injected at a fraction of the reasoning trace. Failure modes: reasoning leaks into the answer after a hard interrupt, "panic" under speed-up requests, and "self-doubt" after updates (about 80% of update errors). Token-fraction timing on static tasks; no training tried. This is the only systematic study of a thought process steered mid-thought.

## Demo

- [project-page] [dynamic-lm project page](https://dynamic-lm.github.io/) — Loaded the page (UC Berkeley, ICML 2026), viewed the result-plot carousel (answer length, panic rate, doubt rate), seeked the 18.5 s looping hard_interrupt.mov to 1/5/10/20 s, and clicked 'Next' in the 'Examples of Hard Interrupt' viewer. The video is an animated plot of Pass@1 and answer length vs interrupt position (0.1 to 0.9) on GSM8K, MATH500, AIME 24/25 and LiveCodeBench for Qwen3-8B, GPT-OSS-20B and Magistral-S-1.2; the example viewers load static JSON (examples_leakage.json, examples_panic.json, examples_doubt.json) and show full vs interrupted-at-0.3 traces for problems such as AIME 2024 I P3 and LCB 'Symmetric Painting'. Links to the [dataset](https://huggingface.co/datasets/dynamic-lm/update-interrupt-benchmark) and [code](https://github.com/dynamic-lm/interrupt-lrm). Play-mode evidence: nothing runs live; the page states "we run a single inference session to obtain the full reasoning chain r and then interrupt ... at different stages", the network log shows no model API calls, and there is no game.

Visited 10 November 2026 in a headless browser.

## What the team could reuse

- The interruptibility protocol and datasets as a static pre-test for mid-thought steering.
