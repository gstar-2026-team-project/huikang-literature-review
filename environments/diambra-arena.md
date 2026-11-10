# DIAMBRA Arena

DIAMBRA Arena is a step-locked platform for arcade fighting games such as Street Fighter III.

| | |
|---|---|
| Year | 2022 |
| Links | [repo](https://github.com/diambra/arena) |
| Demo | [site](https://www.diambra.ai), [docs](https://docs.diambra.ai), [YouTube](https://www.youtube.com/@diambra_ai/videos): the site has no in-browser demo (the [leaderboard](https://www.diambra.ai/leaderboard) API fails with a CORS error, the [web app](https://app.diambra.ai/) needs a wallet, and 'AIvsAI live' is a dead link when logged out). The YouTube channel has recorded videos of RL agent submissions (e.g. SB3 PPO vs CPU in UMK3) in step-locked emulation (step_ratio frames per env.step). Human-playable: no (local Docker plus ROMs only). |
| Play mode | paused-live |
| Clock | STEP |
| Observation | pixels + RAM |
| Action | gamepad |
| Players | 1-2 |
| Horizon | round |
| Human reference | n/a |
| Open source | DIAMBRA licence + ToU, ROMs |
| Convertible to realtime-live | low effort (LLM Colosseum) |
| Basis | code: `diambra/arena/arena_gym.py` `step` RPC; `env_settings.py` `step_ratio: int = 6` |

## Details

- **DIAMBRA Arena**: step-locked; LLM Colosseum is the existing realtime harness.
- DIAMBRA also supports play against the built-in CPU, which would give a single-player absolute score.

## Demo

- [project-page] [diambra.ai](https://www.diambra.ai) — Loaded the marketing page for the 'AIvsAI competition platform for developers' (9 fighting-game environments, roadmap, team bios) and sampled its only media, a 3.54 s muted looping ASCII-art clip (diambracut.mp4) with no gameplay. Clicking 'AIVSAI LIVE >' (an href='#' link) loaded nothing for a logged-out visitor. No gameplay or agent runs shown.
- [dead-or-unreachable] [Leaderboard](https://www.diambra.ai/leaderboard) — Shows an empty table (Rank / User / Score / Game / Difficulty / Characters / Date / Submission) and 'Error: Failed to fetch'; the console shows the call to api.diambra.ai/api/v1alpha1/leaderboard blocked by CORS. No replays reachable.
- [dead-or-unreachable] [Web app](https://app.diambra.ai/) — Shows Home, Marketplace and Guide tabs, a 'Connect Wallet' button and 'Error loading agents.' (console: ERR_NAME_NOT_RESOLVED; footer 2018-2024). Did not connect a wallet; nothing is playable or viewable.
- [project-page] [Docs](https://docs.diambra.ai) — Read the home page, environment settings (/envs/), the Street Fighter III page and the LLM Colosseum project page. Documents a Gym/Gymnasium API over emulated arcade fighting games (1P/2P, pixels plus RAM observations, discrete gamepad actions); use requires registration, Docker and your own ROMs. Play-mode evidence (docs): "step_ratio int default 6 [1,6]: Defines how many steps the game (emulator) performs for every environment step", so env.step advances a fixed number of frames and the game waits for the agent. The LLM Colosseum page (a separate project) describes LLMs that "fight in realtime in Street Fighter III".
- [video] [DIAMBRA YouTube channel](https://www.youtube.com/@diambra_ai/videos) — Listed the channel (114 videos) and watched 'DeepRL Sektor model found a smart exploit for Ultimate Mortal Kombat 3' and 'DIAMBRA AI Competition Platform' at 5, 20 and 40 s. Recording: at 20 s the UMK3 broadcast overlay reads 'AI' (user alexpalms, Score 1524, Submission ID 523, Agent arena-stable-baselines) vs 'COM Difficulty Easy', WINS: 07, timer 67. These are trained RL policies (not LLMs) against the built-in CPU; the in-game timer is emulator time, not wall-clock. The Twitch channel showed no live stream.

Visited 10 November 2026 in a headless browser.

Related: [LLM Colosseum](llm-colosseum.md); [Win Fast or Lose Slow: StreetFighter](streetfighter-win-fast-or-lose-slow.md); [DSGBench](dsgbench.md)
