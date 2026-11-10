# ProactiveVideoQA (PAUC)

ProactiveVideoQA is an offline-replay video benchmark whose PAUC metric scores responses by when they occur.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2507.09313](https://arxiv.org/abs/2507.09313) |
| Demo | None found (searched: arXiv abstract page (no comments field), GitHub repo yellow-binary-tree/ProactiveVideoQA (no homepage field; README has only a static dataset overview image), Hugging Face dataset wangyueqian/ProactiveVideoQA and Spaces search, web search for "ProactiveVideoQA demo"). |
| Play mode | offline replay, timing-scored |
| Clock | responses scored by when they occur |
| Basis | paper §1: "Since model responses are generated at varying timestamps, we further propose PAUC" |

## Details

- None of the streaming video benchmarks has actions; slow inference is not punished unless the metric is timing-aware (PAUC). The PAUC idea is reusable for "respond at the right time".

## Demo

- None found. The arXiv abstract page has no comments field. Its project homepage is the GitHub repo [yellow-binary-tree/ProactiveVideoQA](https://github.com/yellow-binary-tree/ProactiveVideoQA), which has no homepage field. Its README links only to the paper, the code and the [Hugging Face dataset](https://huggingface.co/datasets/wangyueqian/ProactiveVideoQA), and its only media is a static "Dataset Overview" image. A Hugging Face Spaces search for "ProactiveVideoQA" returned no Spaces, and a web search found no project page, video or demo.

Searched 10 November 2026; no demo found.

Related: [StreamingBench](streamingbench.md)
