# LLM Colosseum

LLM Colosseum has two LLMs fight in Street Fighter III via DIAMBRA while the game keeps stepping.

| | |
|---|---|
| Year | 2024 |
| Authors / org | OpenGenerativeAI |
| Links | [GitHub](https://github.com/OpenGenerativeAI/llm-colosseum) |
| Demo | [phospho web demo](https://llm-colosseum.phospho.ai): in-browser MAME emulator where two LLMs (GPT-4o-mini/Pixtral/Llama 3.2) fight live in SF3. The game loop runs at 8 ticks/s and the round timer keeps running while async vision calls are in flight (in Nov 2026 the backend returned empty responses, so the fighters idled). Also: [HF leaderboard](https://huggingface.co/spaces/junior-labs/llm-colosseum) (runtime error), [demo video](https://www.youtube.com/watch?v=Kk8foX3dm2I). Human-playable: no (keyboard character select only). |
| Play mode | realtime-live |
| Clock | env loop steps continuously with no-move default; LLM calls in threads (code read) |
| Observation | text or screenshot |
| Action | named-move macros |
| Players | 2 |
| Horizon | about 1 min |
| Human reference | none |
| Open source | MIT + ROM |
| Convertible to realtime-live | n/a |
| Basis | code: `eval/game.py` (`env.step` loop; LLM calls in `PlanAndAct` threads; empty slot = action 0) |

## Details

- [OpenGenerativeAI/llm-colosseum](https://github.com/OpenGenerativeAI/llm-colosseum) (MIT; user supplies the SF3 ROM). No paper.
- Two LLMs fight in Street Fighter III via DIAMBRA. Realtime-live, confirmed in code. In `eval/game.py` the main loop calls `env.step(actions)` continuously, filling in action 0 (no move) for any player without a pending action and deleting actions once executed. Each player has a `PlanAndAct` daemon thread that calls `robot.plan()` (the LLM call), then `robot.act()`, whenever its action slot is empty. In `agent/robot.py` the LLM is called only when the move queue is empty and one queued button is popped per step. The game therefore keeps stepping while a model is thinking. The loop is not paced to a fixed frame rate.
- Observation: text state or screenshot. Action: a short list of named moves expanded to button sequences (a macro layer). ELO over 546 fights: gpt-4o text 1912.5 top; Claude 3 Sonnet last at 1029.3 (latency and refusals).
- DIAMBRA also supports play against the built-in CPU, which would give a single-player absolute score.

## Demo

- [live-model] [phospho LLM Colosseum web demo](https://llm-colosseum.phospho.ai) — Ran it live in headless Chrome 3 times (Add Coins, Add Players, lock both players on default OpenAI GPT-4o-mini, Fight!), watching 25-35 s per run, intercepting /api/chat/completions and polling window.game; read dist/bundle.js. One run failed with 'Failed to download game data!'. It is a MAME/WASM Street Fighter III 3rd Strike match (Alex vs Ryu) where each robot sends a 320x240 PNG to /api/chat/completions and turns the returned moves into keystrokes; selectable models are GPT-4o-mini, Pixtral-12B and Llama 3.2 90b/11b, with an optional user API key. On the visit the backend returned HTTP 200 with empty bodies, so action queues stayed [] and both fighters idled. Play-mode evidence (run live): Game.startFight runs setInterval(mainLoop, 1000/8) and starts async plan() without awaiting it; the round timer went 83 to 59 over about 22 s while no model had returned a move, game.frame rose about 8/s (35, 70, 105, 140, 175, 208 at 4.4 s polls), and API calls fired continuously with 0.3-2.5 s round trips (about 40 calls in 25 s).
- [leaderboard] [LLM Colosseum HF Space](https://huggingface.co/spaces/junior-labs/llm-colosseum) — Opened it and read app.py. The Space shows 'Runtime error'. Per app.py it is a Gradio Elo leaderboard from a static CSV (elo-20240326.csv) with an embedded YouTube demo (Kk8foX3dm2I). Play-mode evidence: none observable.
- [video] [Mistral 7B vs GPT4 on Street Fighter III](https://www.youtube.com/watch?v=Kk8foX3dm2I) — Watched the unlisted 41 s video, seeking to 5, 30 and 60 s. It is a Mac screen recording of two DIAMBRA Arena sfiii3n windows (Ken vs Ken) from the original Python version, with scores and round timers. Play-mode evidence (recording): round timers count down continuously (61 and 64 at t=30 s); no latency overlay.

Visited 10 November 2026 in a headless browser.

Related: [DIAMBRA Arena](diambra-arena.md) (LLM Colosseum is its existing realtime harness); [Win Fast or Lose Slow: StreetFighter](streetfighter-win-fast-or-lose-slow.md); [DSGBench](dsgbench.md)
