# CivRealm

CivRealm is a turn-based Civilization-style environment with a step/turn loop.

| | |
|---|---|
| Year | 2024-26 |
| Links | [repo](https://github.com/bigai-ai/civrealm) |
| Demo | [docs site](https://bigai-ai.github.io/civrealm): documentation only, with static screenshots of Freeciv-web and a guide to observing your own local run at localhost:8080. No hosted video, replay or live demo. The game is turn-based and waits for the agent (begin_turn arrives only after all players finish; wait_for_observer setting). Human-playable: no hosted version. |
| Play mode | paused-live, turn-based |
| Clock | none or generous per-move limits |
| Observation | text / board |
| Action | moves |
| Players | 1-2+ |
| Horizon | long |
| Human reference | varies |
| Open source | varies |
| Convertible to realtime-live | not meaningful |
| Basis | CivRealm README step/turn loop |

## Details

- In the turn-based or untimed contrast set: CivRealm ([repo](https://github.com/bigai-ai/civrealm) step/turn loop). None of the contrast set has a native clock; a deadline could be imposed but the games do not reward reflexes. They are useful as the "same model, no clock" control.

## Demo

- [project-page] [CivRealm docs site](https://bigai-ai.github.io/civrealm) — Loaded the MkDocs documentation site and followed its Visualization, LLM Agent and Game Settings pages. The home page has one static hero image of a Freeciv Mediterranean map (punic_war_base.jpg) and no video, iframe, canvas, hosted game or replay viewer; the Visualization page only explains how to watch your own local run (Freeciv-web server at localhost:8080, join as observer, send '/observe'), and the LLM Agent page documents the FreecivLLM-v0 Gymnasium env and the BaseLang/Mastaba baselines. Play-mode evidence (docs only, nothing run): the step loop is turn-based and the server sends begin_turn only after every player finishes its turn; settings include begin_turn_timeout ("they may take more than 60 seconds for each of their turns"), wait_for_observer (holds the game in 'Pregame' until an observer joins) and sleep_time_after_turn, so the clock does not run while the model thinks.
- [project-page] [CivRealm GitHub repo](https://github.com/bigai-ai/civrealm) — Opened the repo and searched the raw README for GIF, MP4, video, YouTube and demo links. The README has only badges and no demo media. No play-mode evidence; code only.
- [project-page] [BIGAI paper listing](https://eng.bigai.ai/?p=7130) — Opened the page and read its text. It has the abstract, authors and links to the ICLR 2024 OpenReview PDF and the code, with no media. No play-mode evidence.

Visited 10 November 2026 in a headless browser.