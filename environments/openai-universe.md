# OpenAI Universe

OpenAI Universe was a 2016 platform that ran any program behind a remote desktop as an environment that runs in real time rather than stepping synchronously with the agent's actions.

| | |
|---|---|
| Year | 2016 |
| Authors / org | OpenAI |
| Links | [announcement](https://openai.com/index/universe/), [repo](https://github.com/openai/universe) |
| Demo | [launch post (archived)](https://web.archive.org/web/20161207112259/https://openai.com/blog/universe/): recorded video clips, mostly of human demonstrators, plus recorded RL agents (Pong 'plays at real time', racing Flash games, Mini-WoB, slither.io). The original universe.openai.com is offline (an [archived catalog](https://web.archive.org/web/20161206150325/https://universe.openai.com/) remains). Human-playable: no. |
| Play mode | realtime-live |
| Clock | WALL over VNC, 60 fps throttle |
| Observation | pixels |
| Action | VNC key/mouse events |
| Players | 1 |
| Horizon | short |
| Human reference | n/a |
| Open source | MIT, archived 2018 |
| Convertible to realtime-live | dead; design reference |
| Basis | repo README: "Universe environments run in real-time, rather than stepping synchronously with the agent's actions"; Throttle wrapper 60 fps |

## Details

- OpenAI Universe (2016).
- OpenAI, announced 5 December 2016. [Announcement](https://openai.com/index/universe/) (the page returns HTTP 403 to automated fetches, so its content here comes from search-result snippets and press coverage); [repo](https://github.com/openai/universe) (MIT, README read).
- Tasks: any program that can run behind a remote desktop. At launch: Atari games over VNC, Flash games, browser tasks (Mini World of Bits) and some PC games, described at launch as over 1,000 environments; the README says only "some environments include a reward signal". Exact counts are not given in the repo.
- Play mode: realtime-live. The README states that environments "run in real-time, rather than stepping synchronously with the agent's actions" and that "the environment keeps running in the background even if the agent does not call `env.step()`"; the agent cannot take thinking breaks.
- Clock model: wall clock. The game runs in a Docker container (the "remote") and the agent is a VNC client. A client-side throttle targets 60 fps (one frame every 16.7 ms) and sleeps if `step` is called faster. `reset` is asynchronous and returns empty observations until the environment is ready. The announcement reports driving dozens of environments at 60 fps with about 100 ms latency, mostly from server-side encoding. (The announcement page refuses automated fetches, HTTP 403; this figure is from its search-engine snippet. The play-mode label rests on the README.)
- Observation: screen pixels. Action: a list of VNC keyboard and mouse events, for example `('KeyEvent', 'ArrowUp', True)`, the same interface a human uses. Reward and diagnostics (including latency and client/remote timings in `info`) travel over a separate WebSocket channel.
- Players and horizon: single agent; short game episodes and browser tasks.
- Scoring and human reference: game score where a reward channel existed; no standard human baselines.
- Models evaluated: RL agents of the time (a starter A3C agent). No LLM results.
- Availability: archived on 6 April 2018, "deprecated in favor of the Retro library". It would not build today without effort.
- What went wrong: no official post-mortem was found. Gym Retro, its replacement, steps emulators synchronously with direct memory access instead of VNC, which removes exactly the realtime and remote-desktop parts. Reasons commonly given by users at the time, none confirmed in a primary source: results varied with network and encoding latency so runs were hard to reproduce, many environments had no reward or a noisy scraped one, and the Docker-plus-VNC stack was heavy to run at scale.
- What to take from it: it is the direct precedent for an agent playing over a realtime pixel-and-keyboard channel, and its design choices are still the right checklist. Keep the environment local to the agent to avoid network jitter. Log latency per step, as Universe did. Offer a deterministic clock (token clock or injected latency) next to the wall clock so results can be reproduced. Give every task a programmatic reward read from game state, not scraped from pixels. Keep a paused mode as a control. Expect that a realtime-only platform will be abandoned for a faster synchronous one unless realtime is the point of the benchmark.

## Demo

- [video] [Universe launch post (archived)](https://web.archive.org/web/20161207112259/https://openai.com/blog/universe/) — Opened the Dec 7 2016 Wayback snapshot and played all 11 embedded clips (10-50 s, served from archived openai-sci-demonstrations S3 assets), taking frames at about 4 s and 60%. Most clips are captioned as human play ('A sample of Universe game environments played by human demonstrators', Atari over VNC, Flash games, Mini World of Bits, flight booking); others show the score-OCR model at 60 fps and trained RL/behavior-cloning agents: 'Trained agent playing gym-core.PongDeterministic-v3. The video plays at real time.', three racing Flash game agents with in-game timers, WoB agents, and a slither.io agent with Reward/Value plots ('Your length: 236, Your rank: 207 of 492'). Play-mode evidence (recording): the Pong caption says it plays at real time, and the text says the agent gets frames 60 times per second over VNC while the environment keeps running; remote training uses '32 simultaneous environments at 5 frames per second'. No LLMs (predates them).
- [project-page] [universe.openai.com (archived)](https://web.archive.org/web/20161206150325/https://universe.openai.com/) — Loaded the Dec 2016 snapshot and the Mar 2017 /envs snapshot (the Dec 2017 snapshot redirects to GitHub). A landing page ('Perceive like a human... React like a human', '1000+ environments') and an environment catalog (Flash Games / Internet / PC Games / World of Bits, e.g. DuskDrive-v0, CoasterRacer-v0, NeonRace-v0 tagged 'rl-ready unsupervised-ready'). Static catalog only; nothing playable, no agent runs or replays.
- [dead-or-unreachable] [universe.openai.com](https://universe.openai.com) — net::ERR_NAME_NOT_RESOLVED; the domain no longer exists.
- [dead-or-unreachable] [OpenAI Universe announcement](https://openai.com/index/universe/) — HTTP 403 with a Cloudflare 'Verify you are human' challenge (also for /blog/universe/); not bypassed. The archived copy has the same content.
- [project-page] [openai/universe GitHub repo](https://github.com/openai/universe) — Read the README: archived Apr 6 2018 and deprecated in favor of Retro; a Python library wrapping programs in Docker and VNC as Gym environments (gym-core Atari, flashgames, wob.mini). Code only, no hosted demo.

Visited 10 November 2026 in a headless browser.

## Fit

realtime yes; verifiable partly; single yes; human-easy yes; short yes. Not usable as code.

Related: [stable-retro / Gym Retro](stable-retro.md) (its replacement); [MiniWoB++](miniwob-plusplus.md); [ALE / Atari](ale-atari.md)
