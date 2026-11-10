# Will GPT-4 Run DOOM

"Will GPT-4 Run DOOM?" has a model play Doom from screenshots described as text, with the model call inside the engine frame callback so the engine cannot tick.

| | |
|---|---|
| Year | 2024 |
| Links | [arXiv 2403.05468](https://arxiv.org/abs/2403.05468) |
| Demo | None found (searched: the paper's video page [adewynter.github.io/Doom](https://adewynter.github.io/Doom) returns a GitHub Pages 404; the author's homepage and the github.com/adewynter/Doom repo exist but no working video page was found). Human-playable: no. |
| Play mode | paused-live |
| Clock | model call runs inside the engine frame callback, so the engine cannot tick |
| Observation | screenshot to text |
| Action | key holds |
| Players | 1 |
| Horizon | 1 level |
| Human reference | one human |
| Open source | open |
| Convertible to realtime-live | use ViZDoom |
| Basis | code: `WillItRunDoom.ipynb` `draw_frame()` calls the model synchronously in the cydoomgeneric callback; paper §5.1 "not ready for real-time play" |

## Details

- ViZDoom lists "Will GPT-4 Run DOOM?" (paused) among LLM uses of Doom.

## Demo

- [dead-or-unreachable] [Will GPT-4 Run DOOM? video page](https://adewynter.github.io/Doom) — Opened the video page cited by the paper (arXiv 2403.05468), found by web search. It returns a GitHub Pages 404. The author's homepage (adewynter.github.io) still lists the paper and an i3D 2026 talk, and the repo github.com/adewynter/Doom exists, but no working video page was found.

Visited 10 November 2026 in a headless browser.

Related: [ViZDoom](vizdoom.md)
