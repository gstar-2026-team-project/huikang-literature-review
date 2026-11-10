# GameArena

GameArena is a game-based evaluation scored on "each round's decision".

| | |
|---|---|
| Links | [arXiv 2412.06394](https://arxiv.org/abs/2412.06394) |
| Demo | [AI Space Escape on Roblox](https://www.roblox.com/games/114904064694961/AI-Space-Escape) (human-playable live game; humans play Akinator, Taboo and Bluffing against live LLM guards, but it needs a Roblox account and app, so it was not played here) and [project blog](https://lmgame.org/#/blog/ai_space_escape/) (static screenshots and rankings, no video or replay viewer). |
| Play mode | paused-live (turn- or step-based) |
| Basis | [arXiv 2412.06394](https://arxiv.org/abs/2412.06394): "each round's decision" |

## Details

- In the turn-based or untimed contrast set: GameArena ([arXiv 2412.06394](https://arxiv.org/abs/2412.06394): "each round's decision"). None of the contrast set has a native clock; a deadline could be imposed but the games do not reward reflexes. They are useful as the "same model, no clock" control.

## Demo

- [human-playable] [AI Space Escape on Roblox](https://www.roblox.com/games/114904064694961/AI-Space-Escape) — opened the Roblox experience page (found via the artifact repo [lmgame-org/ai-space-escape-engine](https://github.com/lmgame-org/ai-space-escape-engine), described as "a (Roblox) artifact of the following paper"); playing requires Roblox sign-up and the desktop app, so I did not play. Page shows "By lmgame", "Visits 2,409", "Server Size 1", "Updated 5/2/2025", and badges "Escaped the Facility" (won ever 26) and "Lost in Space" (won ever 1245). The description says "The clock is ticking", a story-level escape timer for the human, not a per-turn deadline on the model. Play-mode evidence: live LLM calls from the repo's backend (`src/serve.py`, API keys in config) answer each human turn; each round is a conversational turn, consistent with paused-live.
- [project-page] [GameArena blog on lmgame.org](https://lmgame.org/#/blog/ai_space_escape/) — read the page: static images only (a Taboo screenshot captioned "Figure 1: the Taboo reasoning challenge in our Roblox game: AI Space Escape", a model ranking table with Akinator/Bluffing/Taboo scores, user-study charts). No video, replay or trajectory viewer.

Visited 10 November 2026 in a headless browser.

Related: [Kaggle Game Arena](kaggle-game-arena.md) (a different arena)
