# CodeClash

In CodeClash agents edit code between rounds and the code competes in arenas.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2511.00839](https://arxiv.org/abs/2511.00839) |
| Demo | [CodeClash Trajectory Viewer](https://viewer.codeclash.ai/): recorded tournament logs (1901 completed runs), with per-round winners, cost and the full agent edit-phase transcripts and diffs. Also: [project site](https://codeclash.ai/) with an Elo leaderboard and [arena pages](https://codeclash.ai/arenas/) showing recorded game animations (e.g. a RobotRumble turn stepper). All recordings; no live model play against a clock; not human-playable. |
| Play mode | scripted |
| Clock | code competes in arenas |
| Observation | code |
| Action | code edits |
| Players | 2 |
| Horizon | rounds |
| Human reference | humans win |
| Open source | open |
| Convertible to realtime-live | out of scope |
| Basis | paper §2: "LMs do not play the games directly"; code `codeclash/tournaments/pvp.py:99-101` (edit phase then competition phase) |

## Details

- **CodeClash** ([arXiv 2511.00839](https://arxiv.org/abs/2511.00839)): agents edit code between rounds; code competes. Out of scope.

## Demo

- [replay viewer] [CodeClash Trajectory Viewer](https://viewer.codeclash.ai/) — Opened the picker ("1901 runs listed", filters for BattleSnake, CoreWar, Halite, HuskyBench, RoboCode, RobotRumble) and the run `PvpTournament.RobotRumble.r15.s1000.p2.gemini-2.5-pro.gpt-5-mini.251006010532`, then expanded a trajectory. It shows a round table (round 0 "Winner: gemini-2.5-pro with 50.8% (p=0.60) (190-413-397)", then gpt-5-mini winning rounds 1-6 at 1000-0.0) and per-player edit-phase stats ("API CALLS: 11", "COST: $0.15", "EXIT STATUS: Submitted"), plus a 24-message transcript where the model runs shell commands such as `ls -laR` and `cat robot.js` under a step budget ("This is the output of step 1 (30 limit). You've used 0.0 USD (1.0 USD limit)"), with full diffs and modified files. Play-mode evidence (recorded): static per-run HTML files under `/game/completed/`; the network log showed only static JS/CSS loads, no model calls; models act only between rounds by editing code, never during the match.
- [project page] [CodeClash site](https://codeclash.ai/) and [arena pages](https://codeclash.ai/arenas/) — Read the home page (Elo leaderboard "Updated Nov. 3, 2025", Claude Sonnet 4.5 first at 1385 ± 18; "Each round has two phases: edit, then compete") and the RobotRumble arena page, which embeds `robotrumble.gif`, an animated recorded match with a "Turn 3" counter and slider, plus a CC:Ladder of 58 human bots. Play-mode evidence (recording): the animation is a pre-rendered turn-based replay of bot code; the page says "your bot must execute within 60 seconds or forfeit" per match, so the clock bounds the code, not a model.

Visited 10 November 2026 in a headless browser.

Related: [CodeClash](../solutions/codeclash.md)
