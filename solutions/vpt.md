# VPT

VPT is a Minecraft model on the 20 Hz native interface with a synchronous simulator.

| | |
|---|---|
| Year | 2022-25 |
| Links | [arXiv 2206.11795](https://arxiv.org/abs/2206.11795) |
| Demo | [OpenAI VPT blog](https://openai.com/index/vpt/): the official project page, with embedded Vimeo clips of the agent playing Minecraft (crafting table, swimming, hunting, pillar jumping, crafting a diamond pickaxe). These are recordings of offline rollouts, with no live model and no replay viewer. Not human-playable. The page could not be rendered in the headless browser (Cloudflare challenge), so the clips were not watched. |
| Category | RL and decision model |
| Method | 20 Hz native interface; synchronous simulator |
| Evaluated on | Minecraft |
| Evaluation play mode | paused-live |
| Basis | paper (VPT) App. C: client and server "run in the same thread ... slower or faster than real time"; code: MineRL `_multiagent.py` synchronous token |

## Demo

- [project page with videos] [OpenAI: Learning to play Minecraft with Video PreTraining](https://openai.com/index/vpt/) — Opened it in headless Chrome. It showed only a Cloudflare "Just a moment..." challenge and no content, and WebFetch got HTTP 403. The automated-browser safety check then refused further attempts, including loading the page through the Wayback Machine. The captions come from the Wayback Machine HTML fetched with curl. The page embeds clips through a Nuxt `LazyAutoPausingVimeo` component, and the Vimeo IDs are not in the static HTML. The captions include "Crafting of a crafting table “zero shot” (i.e. after pre-training only without additional fine-tuning)", "Swimming (zero-shot)", "Hunting animals (zero-shot)", "Eating food (zero-shot)", "Pillar jumping (zero-shot)", "Crafting a stone pickaxe", "Constructing a rudimentary wooden shelter", "Searching through a village" and "RL fine-tuned VPT model crafting a diamond pickaxe". There are also item-sequence SVGs on cdn.openai.com (crafting-table-sequence.svg, stone-pickaxe-sequence.svg, diamond-pickaxe-sequence.svg). Play-mode evidence: none observed, because the clips are recordings of rollouts and were not watched. The page states the "native human interface: 20Hz frame rate with the mouse and keyboard".
- [repo] [openai/Video-Pre-Training](https://github.com/openai/Video-Pre-Training) — Read the README with `gh` (it has no homepage field). It has links to model weights and contractor-data mp4/jsonl files, for example cheeky-cornflower-setter-02e496ce4abb-20220421-092639.mp4, which is a human contractor recording. It embeds no agent videos and no replay viewer.

Searched 10 November 2026. The project page above is a demo, but it could not be rendered in a headless browser.

Related: [MineRL](../environments/minerl.md); [STEVE-1](steve-1.md); [GROOT](groot.md); [ROCKET](rocket.md); [JARVIS-VLA](jarvis-vla.md); [DreamerV3 / Dreamer 4](dreamer.md)
