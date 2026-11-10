# Kaggle Game Arena

Kaggle Game Arena is a turn-based game arena with generous per-move limits (poker "Each action has a 60-minute time limit").

| | |
|---|---|
| Year | 2024-26 |
| Links | [arXiv 2609.31473](https://arxiv.org/abs/2609.31473) |
| Demo | [Game Arena](https://www.kaggle.com/game-arena) / [Chess leaderboard + replays](https://www.kaggle.com/benchmarks/kaggle/chess-text/versions/2): leaderboard with a step-through viewer of recorded model-vs-model turn-based games (Go, Chess, Poker, Werewolf, ...) that shows each move's reasoning. The game waits for the model: up to 60 min per move (actTimeout=3600), and recorded moves took a mean of 3-6 min and up to about 40 min. The hub also links a [YouTube commentary playlist](https://www.youtube.com/playlist?list=PLqFaTIg4myu_tpB0JXRJ5Hb-ApyXDxOlD). Human-playable: no. |
| Play mode | paused-live, turn-based |
| Clock | none or generous per-move limits |
| Observation | text / board |
| Action | moves |
| Players | 1-2+ |
| Horizon | long |
| Human reference | varies |
| Open source | varies |
| Convertible to realtime-live | not meaningful |
| Basis | Game Arena code `harness/model_generation_demo.py` (per-call API timeout, no game clock) |

## Details

- In the turn-based or untimed contrast set: Kaggle Game Arena ([arXiv 2609.31473](https://arxiv.org/abs/2609.31473): poker "Each action has a 60-minute time limit"). None of the contrast set has a native clock; a deadline could be imposed but the games do not reward reflexes. They are useful as the "same model, no clock" control.

## Demo

- [replay-viewer] [Kaggle Game Arena hub](https://www.kaggle.com/game-arena) — Loaded the hub, let the Featured Games embed auto-play (a Go replay of Claude Opus 5 vs Claude Fable 5.1 in kaggleusercontent.com/episode-visualizers/open_spiel_go), used play/pause, read the Game Log and downloaded its replay.json (episode 110749746). The hub has an aggregate leaderboard across 15+ turn-based games (Go, Chess, Reversi, Checkers, heads-up Poker, Werewolf, Word Art, Bargaining, Dark Hex, etc.) and per-game gameplay datasets; the viewer shows a 13x13 board, step counter (4/192), 1x speed, restart/prev/next, and per-move cards ('Plays on G7') with expandable 'Show thinking'. Play-mode evidence (recorded replay): replay.json has actTimeout=3600 (60 min per move), runTimeout=108000, illegalMoveForfeit=true and remainingOverageTime=12; info.moveDurations show 190 moves averaging 208 s, max 1340 s (about 11 hours in total); LiveVideoPath is null. The board does not change while a model thinks.
- [replay-viewer] [Chess (text) leaderboard and replays](https://www.kaggle.com/benchmarks/kaggle/chess-text/versions/2) — Opened the leaderboard, clicked a model's 'Replay' icon to open Game History (?episodeId=125711558, Grok 4.7 vs Gemini 4 Carbon), paused, stepped to move 9/86 and expanded 'Show thinking'; downloaded the replay.json. The view has a list of past games ('11d ago'), the board, and a Game Log with step counter, speed control, a 'Streaming View' toggle and full per-move reasoning (e.g. the 4...Nf6 Open Sicilian explanation); the leaderboard shows Avg. Tokens/Turn and Avg. Cost/Turn. Play-mode evidence (recorded replay): actTimeout=3600, illegalMoveForfeit=true; 84 moves with mean duration 332 s and max 2375 s (about 40 min); LiveVideoPath null.
- [video] [Kaggle Game Arena 2026 YouTube playlist](https://www.youtube.com/playlist?list=PLqFaTIg4myu_tpB0JXRJ5Hb-ApyXDxOlD) — Loaded the official playlist 'Kaggle Game Arena 2026: Poker, Werewolf, & Chess' and opened one video ('Poker Pros React to AI Models Playing Heads-Up Poker', 28:56) without playing it. Edited commentary of experts reacting to recorded LLM tournament games; no live model clock.

Visited 10 November 2026 in a headless browser.