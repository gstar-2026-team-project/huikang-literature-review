# UI-TARS-2

UI-TARS-2 is a VLM trained with multi-turn RL in a sandbox and evaluated on 15 browser games.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2509.02544](https://arxiv.org/abs/2509.02544) |
| Demo | [UI-TARS-2 Showcase](https://seed-tars.com/showcase/ui-tars-2/): official project page of seven recorded Agent TARS session replays (web search, coding, Jupyter, page deployment). No game footage, game replays or playable games; nothing shows the model playing against a clock. |
| Category | post-training |
| Method | multi-turn RL in a sandbox |
| Evaluated on | 15 browser games |
| Evaluation play mode | paused-live |
| Basis | paper §2.2: clients "receive synchronous observations"; timing APIs "allow time acceleration and pause" |
| What is trained | VLM |

## Demo

- [project-page] [UI-TARS-2 Showcase](https://seed-tars.com/showcase/ui-tars-2/) — Opened it and the card "Use Jupyter To Compare Numbers". The page has no video, iframe or canvas elements. It loads its seven cards from a static file (ui-tars-2-showcase.json), and each card links to a recorded "shared-conversations/agent-tars-...html" session replay. The tasks are "Search Bytedance Seed1.6 News And Deploy Web", "Weight Unit Conversion Query", "Hugging Face Dataset Char Count", "Twin - Island Nation Independence Inquiry", a music-theory course page and "Use Jupyter To Compare Numbers". None of them is a game. Play-mode evidence: none for the 15-game suite. These are recorded tool-use sessions, not live model calls.
- Also checked the seed-tars.com home page, which links the Game-TARS and UI-TARS-1.5 pages but has no UI-TARS-2 game media. The bytedance/UI-TARS README embeds GUI_demo.mp4 and Game_demo.mp4, but they sit under the UI-TARS-1.5 section, so they are not UI-TARS-2 footage.

Visited 10 November 2026 in a headless browser.

Related: [UI-TARS-2 game suite](../environments/ui-tars-2.md) (environment details); [Game-TARS](game-tars.md)
