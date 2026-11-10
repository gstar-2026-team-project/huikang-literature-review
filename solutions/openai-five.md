# OpenAI Five

OpenAI Five played Dota 2 at 30 fps, acting on every fourth frame and reacting in 217 ms on average.

| | |
|---|---|
| Year | 2019 |
| Links | [arXiv 1912.06680](https://arxiv.org/abs/1912.06680) |
| Demo | [OpenAI Five (archived)](https://web.archive.org/web/20191219212314/https://openai.com/blog/how-to-train-your-openai-five/): recorded Twitch VODs and still-downloadable .dem replays of live real-time matches against OG; the archived blog states 80 ms average reaction (later 200 ms) acting every 4th frame at 30 fps. The live [research page](https://openai.com/research/openai-five) is behind a Cloudflare check; OpenAI Five Arena (Apr 2019) is closed. Human-playable: no. |
| Category | RL and decision model |
| Method | acts every 4th frame (7.5 Hz); 217 ms average reaction |
| Evaluated on | Dota 2 |
| Evaluation play mode | realtime-live vs humans |
| Basis | paper §2: "OpenAI Five only acts on every 4th frame"; "react to a game event in 217ms on average" |

## Details

- **OpenAI Five.** Dota 2 at 30 fps; the agent acts on every fourth frame and reacts in 217 ms on average. The nominal reaction time was raised from 80 ms to 200 ms for the 2018 benchmark as a fairness constraint. State vector from the bot API, not pixels.
- Human reference numbers used as constraints: OpenAI Five 217 ms average reaction.

## Demo

- [dead-or-unreachable] [OpenAI Five research page](https://openai.com/research/openai-five) — Cloudflare "Just a moment..." (HTTP 403) in headless Playwright and WebFetch; not bypassed. Read the archived copy (web.archive.org/web/20191231015352/https://openai.com/blog/openai-five/) instead: it embeds YouTube eHipy_j29Xw and says Dota runs at 30 fps, OpenAI Five observes every 4th frame, averages 150-170 APM (theoretical maximum 450) and has "an average reaction time of 80ms, which is faster than humans" (67 ms for the 1v1 bot); per web search, the later OpenAI Five Benchmark post raised this to 200 ms. Play-mode evidence: live real-time play on the game clock under a fixed reaction delay; the demos are recorded.
- [replay-viewer] [How to Train Your OpenAI Five (archived)](https://web.archive.org/web/20191219212314/https://openai.com/blog/how-to-train-your-openai-five/) — Opened the archived page: two Twitch VOD embeds of the OG finals (v410533063 at 44m51s and 3h28m13s), downloadable Dota 2 .dem replays for OG Game 1, OG Game 2 and a co-op game (cdn.openai.com/how-to-train-your-openai-five/og_game_1_04132013569395266.dem still returns HTTP 200, about 43.6 MB), and "OpenAI Five planning view" links. OpenAI Five Arena, the April 2019 public event where anyone could play with or against the bot, is closed (arena.openai.com does not resolve). Play-mode evidence: recorded replays and streams of live matches; nothing playable now.
- [video] [OG vs OpenAI Five fan highlights](https://www.youtube.com/watch?v=pkGa8ICQJS8) — Opened "OG vs OpenAI FIVE - TI8 champions vs bots final" (NoobFromUA, 18:33) and seeked to 900 s; the captured frame shows the thumbnail and title card. Recorded footage of real-time matches against humans.
- Note: the file's Basis cites the paper's "react to a game event in 217ms on average", while the archived OpenAI Five blog states "an average reaction time of 80ms" (67 ms for the 1v1 bot) and the later Benchmark post 200 ms; the figures come from different versions of the system.

Visited 10 November 2026 in a headless browser.

Related: [Dota 2 bot API / dotaservice](../environments/dota-2-bot-api.md)
