# SmartPlay

SmartPlay is a text game benchmark stepped once per model query.

| | |
|---|---|
| Year | 2023 |
| Links | [arXiv 2310.01557](https://arxiv.org/abs/2310.01557) |
| Demo | None found (searched: GitHub microsoft/SmartPlay README and homepage field (empty; README has only static teaser and figure images), arXiv abstract page, Hugging Face paper page and Spaces search, web search for "SmartPlay demo" / project page / video). |
| Play mode | paused-live |
| Clock | STEP |
| Observation | text |
| Action | categorical |
| Players | 1 |
| Horizon | mixed |
| Human reference | yes |
| Open source | open |
| Convertible to realtime-live | not meaningful |
| Basis | code: `examples/experiment.py` (`query_model` then `env.step`) |

## Details

- In the turn-based or untimed contrast set: paused-live (turn- or step-based), from code (`examples/experiment.py`). None of the contrast set has a native clock; a deadline could be imposed but the games do not reward reflexes. They are useful as the "same model, no clock" control.

## Demo

- None found. The [microsoft/SmartPlay](https://github.com/microsoft/SmartPlay) repo has no homepage set, and its README shows only a static teaser image and a games figure, with no videos, GIFs or replays. The arXiv page has no project link. The Hugging Face paper page links no SmartPlay Space ("Spaces citing this paper" lists only a generic recommender), and web searches turned up no project page or official video.

Searched 10 November 2026; no demo found.
