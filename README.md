# Literature review: LLMs that sense, think and act in realtime

Research date: 10 November 2026.

## Scope

This review supports a project to (1) build or collect realtime environments, (2) show that current models do badly on them while humans do fine, and (3) post-train models to improve. It covers:

- **[environments/](environments/README.md)**: game environments and benchmarks from RL-era platforms to 2026 LLM/VLM benchmarks, plus near neighbours (trading, negotiation, computer use, full-duplex speech, streaming video, robotics). It has one file per environment; the [index](environments/README.md) has the comparison tables, the environments grouped by play mode, and a shortlist for first environments.
- **[solutions/](solutions/README.md)**: agent scaffolds, realtime model architectures, RL and decision models, and post-training methods. It has one file per work; the [index](solutions/README.md) has a summary table per category, the reuse notes, and a list of gaps.

Out of scope: code execution as the way of solving a task, image and sound generation, pre-training or new architectures from scratch.

## Most relevant recent research

The works closest to this project, newest first within each group. Each name links to its file, which has the play-mode basis and full details.

**Benchmarks that run a clock while the model thinks** (the project's step 2)

| Work | Date | What it tests | Clock | Headline result |
|---|---|---|---|---|
| [LOLPlay](environments/lolplay.md) | Nov 2026 | 36 League of Legends tasks from 1080p screenshots, mouse and keyboard | wall clock | best 25% task success (GPT-6 Astra); higher reasoning effort never helped; two humans 36/36 |
| [Realtime-Bench](environments/realtime-bench.md) | Oct 2026 | 30 web and 20 game tasks (Pong, timed chess, Gomoku, highway) through a computer-use interface | wall, token and paused clocks on the same tasks | Claude Opus 5 high effort: 70% paused, 30% token clock, 14% wall clock; best wall-clock 44% |
| [RealtimeBench](environments/realtimebench.md) (with [TORSI](solutions/torsi.md)) | Oct 2026 | six arcade games (Mario, Snake, Tetris, runner, shooter, Flappy-style) from text state | paused, live, 1.5x and 2x | GPT-6.1-sol about 44 paused, 1.5 live; ranking flips between paused and live; no code yet |
| [ROAR](environments/roar.md) | Oct 2026 | Unity arena shooter with pixels, depth, text and audio | 250 ms and 40 ms wall-clock ticks, plus turn-based | Gemini-3.1 Pro 0.87 turn-based, 0.34 at 40 ms, level with a rule bot |
| [OmniGameArena](environments/omnigamearena.md) | Jun 2026 | 12 Unreal Engine 5 games | paused, and inference time charged to the game clock | GPT-5.5 SharedFloor 0.368 paused, 0.048 with latency charged |
| [GameWorld-RT](environments/gameworld.md) | Apr 2026 | 34 browser games with state-verified scoring and human baselines | paused (main) and wall clock (RT) | humans 55-77% success; RT run on two Qwen3-VL models only |
| [Real-Time Reasoning Gym](environments/realtime-gym.md) | Nov 2025 | Freeway, Snake, Overcooked at three cognitive loads | one environment step per N generated tokens | planning agent 0.92 to 0.05 as pressure rises; [AgileThinker](solutions/agile-thinker.md) 0.90 to 0.58 |

**Related benchmarks that show what to avoid or copy**

- [SpeedrunBench](environments/speedrunbench.md) (Oct 2026): scores frames to goal against human world records. Offline the model edits an input trace (scripted) and gets within 3-7% of the record; online the game waits for each action (paused-live) and runs are 4-12 times the record. Its demo races a human against a recorded model run.
- [PokeAgent speedrun track](environments/pokeagent-speedrun.md) (2025-26): the game runs while the agent reasons, but the winner used LLM-written scripted sub-policies, not live play.
- [Orak](environments/orak.md) (2025): pauses every game during inference; its StarCraft II ablation without the pause drops all models from 75-100 to 0.
- [OpenAI Universe](environments/openai-universe.md) (2016): the original realtime pixel-and-keyboard platform, abandoned for synchronous emulators; its design is still the checklist.

**Methods for thinking while acting** (the project's step 3)

- [AgileThinker](solutions/agile-thinker.md) (ICLR 2026): a planning model streams its reasoning while a reactive model reads the partial trace and acts before each deadline. The clearest published fast-plus-slow design for LLM game agents.
- [TORSI](solutions/torsi.md) (Oct 2026): a slow teacher writes guidance offline and a fast student plays live alone; lifts the fast student from 13.5 to 24.2 on RealtimeBench.
- [Thinking Machines interaction models](solutions/tml-interaction-small.md) (2026): a full-duplex model working in 200 ms micro-turns with an asynchronous background model; strong on speech timing benchmarks but never evaluated as a game player.
- [Lumine](solutions/lumine.md) (2025): an imitation-trained Genshin Impact agent at 5 Hz perception and 30 Hz action chunks that plays its long missions in real time.
- [Timely-RL](solutions/timely-rl.md) (2026) and [Kyutai interactivity alignment](solutions/kyutai-interactivity-alignment.md) (2026): RL with a deadline or timing reward, on static tasks and on speech. The nearest existing post-training recipes; nobody has yet trained against a live game clock.
- [Real-Time Chunking](solutions/real-time-chunking.md) (2025): robotics' method for acting while the next chunk is computed, not yet ported to LLM game agents.

## Play-mode definitions

Every environment and evaluation is classified by how the agent actually plays:

- **Realtime-live**: the model chooses actions itself during play and the environment clock keeps running while it thinks (wall clock, or a token or compute budget that advances the game). Slow thinking costs you. This is the target.
- **Paused-live**: the model chooses each action itself but the environment waits for it (turn per frame, emulator paused during inference, scored in frames or steps).
- **Scripted**: the model writes a program, policy, macro or offline action trace that then plays; the model is not in the loop during play.

Many benchmarks have more than one mode; each is recorded separately.

## Key takeaways

1. **Step 2 is partly published already.** Between November 2025 and November 2026 a cluster of benchmarks appeared that run the same tasks paused and under a clock: Real-Time Reasoning Gym, GameWorld-RT, OmniGameArena, Realtime-Bench, RealtimeBench, ROAR and LOLPlay. The pattern is consistent: frontier reasoning models lose most of their score when the clock runs (for example 70% paused to 14% wall clock for one model in Realtime-Bench; about 44 to 1.5 in RealtimeBench), more reasoning effort helps when paused and hurts or does nothing live, and fast small or realtime-API models are quick but too weak.
2. **Pausing is the norm and is often stated only in an appendix.** Orak, Cradle, V-MAGE, NitroGen, CombatVLA, Game-TARS (web games), GameWorld (main), OmniGameArena (main) and VideoGameBench-Lite all pause the game during inference. Several "human-level" game results hold only under pause.
3. **Scripted routes win when allowed.** Offline trace editing gets within 3-7% of speedrun world records where live play is 4-12 times slower, and the PokeAgent speedrun winner used LLM-written scripts. A realtime benchmark must rule these out to measure in-loop ability.
4. **What is still missing on the environment side**: human baselines under the same clock and interface, and short, human-easy tasks with pixels and low-level actions. Good bases exist and are open: MiniWoB++ (natively wall-clock with time-decayed reward), ViZDoom async mode, Atari and small arcade games behind a wall-clock wrapper, GameWorld-RT, and the Realtime-Bench harness with its wall, token and paused clocks.
5. **Four clock designs are in use**: wall clock, token clock, latency injection, and paused as the control. Token and injected clocks are reproducible and hardware independent, which matters for training.
6. **The recurring scaffold is a fast reactive loop plus a slow asynchronous thinker** (HLA, DPT-Agent, AgileThinker, Latent Bridge, the Thinking Machines background model). At human tick rates the fast loop is always a hand-written executor or a second model.
7. **Step 3 is open.** No paper was found that post-trains a reasoning LLM against a live game clock and reports better realtime scores. The nearest pieces are imitation-trained game models (Lumine), deadline-aware RL on static tasks (Timely-RL), prompt-level teaching (TORSI), and RL on timing rewards for speech models (Kyutai).
8. **No interaction or full-duplex model has been evaluated as a game player**, and none has an action output channel. Robotics has mature methods for acting while inference runs (action chunking, real-time chunking, delay-conditioned training) that have not been ported to LLM game agents.

## Caveats

- Every play-mode and clock label rests on a primary source that was opened and read (repo code or the paper's full text), cited in the Basis column of each table. Items with nothing readable are listed under "Not reviewable" at the end of [environments/README.md](environments/README.md#not-reviewable).
- Numbers were extracted from arXiv HTML pages by a summarising fetch tool and should be re-checked against the papers before being quoted.
- Model names in 2026 papers are reproduced as printed.
- Two October 2026 benchmarks have nearly the same name: Realtime-Bench (arXiv 2610.22155, UT Austin and others) and RealtimeBench (arXiv 2610.20665, Peking University and Samsung).
