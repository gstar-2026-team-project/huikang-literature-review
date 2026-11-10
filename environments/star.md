# STAR

STAR is a 1v1 hex wargame with turn-based and real-time modes.

| | |
|---|---|
| Year | 2026 |
| Links | [arXiv 2603.09337](https://arxiv.org/abs/2603.09337) |
| Demo | [official video](https://www.youtube.com/watch?v=4bSB5S3ixLI) (also an animated GIF in the [repo README](https://github.com/star-nexus/star)): a 95 s screen recording of two LLM agents playing the RoTK hex map, with the game window's running "Game Time" clock next to the agents' terminals streaming tool calls. It is a recording; there is no replay viewer and no public page where a person can play. |
| Play mode | paused-live (turn_based) + realtime-live (real_time) |
| Clock | turn-based and real-time modes |
| Observation | text hex map |
| Action | unit orders |
| Players | 2 |
| Horizon | long |
| Human reference | none |
| Open source | open repo |
| Convertible to realtime-live | n/a |
| Basis | code: README "Real-time keeps the world ticking while the model thinks"; `starbench.py --mode turn_based|real_time`; paper §4.2-4.3 |

## Details

- **STAR** (Mar 2026), [arXiv 2603.09337](https://arxiv.org/abs/2603.09337): 1v1 hex wargame with turn-based and real-time modes; a thinking model falls from rank 1 to 17 in real time. The repo README defines the modes: "Real-time keeps the world ticking while the model thinks (latency changes outcomes); turn-based is the reproducible bench" (`starbench.py --mode turn_based|real_time`).

## Demo

- [official video] [Starbench RoTK: LLM Multi-Agent PvP Strategy ENV (YouTube)](https://www.youtube.com/watch?v=4bSB5S3ixLI) — Played the 95 s video muted and took frames at about 13 s, 42 s, 67 s and 90 s. The video description says "Starbench RoTK is a strategic PvP game designed to evaluate the strategic and tactical capabilities of large language model (LLM) agents." The left half shows the hex map with red and blue units, a minimap, a "BATTLE LOG" ("[10:01] wei dealt 9 damage to shu") and an "All factions active" header. The right half shows two agent terminals streaming `tool_calls` such as "Performing action 'attack'" / "Executing tool 'perform_action'" with JSON like `{"action": "attack", "params": {"unit_id":237,"target_id":234}}`, plus occasional "Tool call error: tool_invalid_tool". Play-mode evidence (recording): the on-screen "Game Time" moved from 03:12 at 13 s to 10:06 at 42 s while the agents issued actions, which suggests a continuously ticking clock (the real-time mode). The video is a recording and does not show model calls happening live.
- [video/GIF] [repo README](https://github.com/star-nexus/star) — Opened the GitHub page. The animated GIF `docs/assets/starbench_rotk.gif` (alt text "STAR Environment Demo") shows the same footage and has a "Watch High-Res Video on YouTube" button. The README also has a Leaderboard section and a "MCP Arena" section, but neither links to a hosted viewer or a playable page.

Visited 10 November 2026 in a headless browser.

Related: [StarBench](starbench.md) (a different, turn-based RPG benchmark)
