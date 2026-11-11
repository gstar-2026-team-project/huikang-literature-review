# Literature review: LLMs that sense, think and act in realtime

Research date: 10 November 2026.

This is a literature review for a GStar Bootcamp 2026 team project. The project's goal is large language models (LLMs) that can sense, think and act in realtime: models that keep taking in input, reasoning and acting while the world around them keeps moving, instead of having it wait for them. The project plan has three steps:

1. **Environments**: build or collect realtime environments, such as games whose clock keeps running while the model thinks.
2. **Benchmark**: test current models on those environments, to show that they do badly where humans do fine.
3. **Post-training**: train models to do better on them.

The review collects published environments, benchmarks and methods that bear on each step. It is written for the project team and for anyone new to the topic.

**How to use it.** Read this page first. [Play modes and clocks](#play-modes-and-clocks) defines the labels used everywhere in the review, [Most relevant recent research](#most-relevant-recent-research) lists the work closest to steps 2 and 3, and [Key takeaways](#key-takeaways) summarises what the literature shows. For more, go to the two indexes below; each links to one file per work with details, sources and, where one exists, a demo.

## Scope

The review has two parts:

- **[environments/](environments/README.md)**: game environments and benchmarks, from platforms built for reinforcement learning (RL) to 2026 benchmarks for LLMs and vision-language models (VLMs), plus near neighbours (trading, negotiation, computer use, full-duplex speech, streaming video, robotics). It has one file per environment; the [index](environments/README.md) has the comparison tables, the environments grouped by play mode, and a shortlist of candidates for the project's first environments.
- **[solutions/](solutions/README.md)**: agent scaffolds (code wrapped around an existing model), realtime model architectures, reinforcement-learning and decision models, and post-training methods. It has one file per work; the [index](solutions/README.md) has a summary table per category, notes on what the project could reuse, and a list of gaps in the literature.

Out of scope: code execution as the way of solving a task, image and sound generation, pre-training or new architectures from scratch.

## Play modes and clocks

Every environment and evaluation in the review is classified by how the agent actually plays:

- **Realtime-live**: the model chooses actions itself during play and the environment clock keeps running while it thinks (wall clock, or a token or compute budget that advances the game). Slow thinking costs the agent. This is the mode the project targets.
- **Paused-live**: the model chooses each action itself but the environment waits for it (one turn per frame, emulator paused during inference, scored in frames or steps).
- **Scripted**: the model writes a program, policy, macro or offline action trace that then plays; the model is not in the loop during play.

Many benchmarks have more than one mode; each is recorded separately.

The clocks used to make an environment realtime-live:

- **Wall clock**: the environment advances in real elapsed time while the model runs.
- **Token clock**: each block of tokens the model generates advances the environment by a fixed amount of game time.
- **Latency injection** (also "inference time charged to the game clock"): the environment waits during the model call, then the measured latency is applied to the game before the action lands.
- **Paused**: the environment waits for every action; used as the control.

## Most relevant recent research

The works closest to steps 2 and 3 of the project, newest first within each group. Each name links to its file, which gives the source for its play-mode label and the full details. Note that Realtime-Bench and RealtimeBench are two different benchmarks (see [Caveats](#caveats)).

**Benchmarks that run a clock while the model thinks** (step 2: show that current models do badly)

| Work | Date | What it tests | Clock | Headline result |
|---|---|---|---|---|
| [LOLPlay](environments/lolplay.md) | Nov 2026 | 36 League of Legends tasks from 1080p screenshots, mouse and keyboard | wall clock | best task success 25% (GPT-6 Astra); higher reasoning effort never helped; two experienced human players completed all 36 |
| [Realtime-Bench](environments/realtime-bench.md) | Oct 2026 | 30 web and 20 game tasks (Pong, timed chess, Gomoku, highway) through a computer-use interface | wall, token and paused clocks on the same tasks | Claude Opus 5 at high effort: 70% success paused, 30% on the token clock, 14% on the wall clock; best wall-clock success of any model 44% |
| [RealtimeBench](environments/realtimebench.md) (with [TORSI](solutions/torsi.md)) | Oct 2026 | six arcade games (Mario, Snake, Tetris, runner, shooter, Flappy-style) from text state | paused, live, 1.5x and 2x | average score out of 100: GPT-6.1-sol about 44 paused (averaged by this review from the paper's per-game table), 1.5 live; model ranking flips between paused and live; no code released yet |
| [ROAR](environments/roar.md) | Oct 2026 | Unity arena shooter with pixels, depth, text and audio | 250 ms and 40 ms wall-clock ticks, plus turn-based | score from 0 to 1: Gemini-3.1 Pro 0.87 turn-based, 0.34 at 40 ms, level with a rule-based bot |
| [OmniGameArena](environments/omnigamearena.md) | Jun 2026 | 12 Unreal Engine 5 games | paused, and inference time charged to the game clock | GPT-5.5 on the SharedFloor game: 0.368 paused, 0.048 with latency charged |
| [GameWorld-RT](environments/gameworld.md) | Apr 2026 | 34 browser games with state-verified scoring and human baselines | paused (main) and wall clock (RT) | humans 55-77% success; the realtime (RT) mode was run on two Qwen3-VL models only |
| [Real-Time Reasoning Gym](environments/realtime-gym.md) | Nov 2025 | Freeway, Snake, Overcooked at three cognitive loads | one environment step per N generated tokens | score from 0 to 1: a planning agent falls from 0.92 to 0.05 as time pressure rises; [AgileThinker](solutions/agile-thinker.md) falls from 0.90 to 0.58 |

**Related benchmarks with designs to avoid or copy**

- [SpeedrunBench](environments/speedrunbench.md) (Oct 2026): scores frames to goal against human world records. Offline, the model edits an input trace (scripted) and gets within 3-7% of the record; online, the game waits for each action (paused-live) and runs take 4-12 times as long as the record. Its demo lets a human race a recorded model run.
- [PokeAgent speedrun track](environments/pokeagent-speedrun.md) (2025-26): the game runs while the agent reasons, but the winner used LLM-written scripted sub-policies, not live play.
- [Orak](environments/orak.md) (2025): pauses every game during inference; in its StarCraft II ablation without the pause, all models drop from paused scores of 75-100 to 0.
- [OpenAI Universe](environments/openai-universe.md) (2016): the original realtime platform with pixel input and keyboard output, abandoned in favour of synchronous emulators; its design is still a useful checklist.

**Methods for thinking while acting** (step 3: train models to do better)

- [AgileThinker](solutions/agile-thinker.md) (ICLR 2026): a planning model streams its reasoning while a reactive model reads the partial trace and acts before each deadline. The clearest published design that pairs a fast and a slow model in an LLM game agent.
- [TORSI](solutions/torsi.md) (Oct 2026): a slow teacher model writes guidance offline and a fast student model plays live on its own; this lifts the fast student's average RealtimeBench score from 13.5 to 24.2 (out of 100).
- [Thinking Machines interaction models](solutions/tml-interaction-small.md) (2026): a full-duplex model (one that takes input and produces output at the same time) working in 200 ms micro-turns, with an asynchronous background model; strong on speech timing benchmarks but never evaluated as a game player.
- [Lumine](solutions/lumine.md) (2025): a Genshin Impact agent trained by imitation, with perception at 5 Hz and action chunks at 30 Hz, that plays its long missions in realtime.
- [Timely-RL](solutions/timely-rl.md) (2026) and [Kyutai interactivity alignment](solutions/kyutai-interactivity-alignment.md) (2026): reinforcement learning with a deadline or timing reward, on static tasks and on speech respectively. These are the nearest existing post-training recipes; nobody has yet trained against a live game clock.
- [Real-Time Chunking](solutions/real-time-chunking.md) (2025): a robotics method for acting while the next chunk of actions is computed, not yet ported to LLM game agents.

## Key takeaways

1. **Step 2 (showing that current models do badly) is partly published already.** Between November 2025 and November 2026 a cluster of benchmarks appeared that run the same tasks paused and under a clock: Real-Time Reasoning Gym, GameWorld-RT, OmniGameArena, Realtime-Bench, RealtimeBench, ROAR and LOLPlay. The pattern is consistent: frontier reasoning models lose most of their score when the clock runs (for example 70% paused to 14% wall clock for one model in Realtime-Bench, and about 44 to 1.5 out of 100 in RealtimeBench); more reasoning effort helps when paused and hurts or does nothing live; and fast small models or realtime-API models respond quickly but are too weak.
2. **Pausing is the norm and is often stated only in an appendix.** [Orak](environments/orak.md), [Cradle](environments/cradle.md), [V-MAGE](environments/v-mage.md), [NitroGen](environments/nitrogen.md), [CombatVLA](environments/combatvla.md), [Game-TARS](environments/game-tars.md) (web games), [GameWorld](environments/gameworld.md) (main mode), [OmniGameArena](environments/omnigamearena.md) (main mode) and [VideoGameBench-Lite](environments/videogamebench.md) all pause the game during inference. Several "human-level" game results hold only under pause.
3. **Scripted routes win when allowed.** Offline trace editing gets within 3-7% of speedrun world records where live play takes 4-12 times as long, and the PokeAgent speedrun winner used LLM-written scripts. A realtime benchmark must rule these out to measure what the model can do while in the loop.
4. **What is still missing on the environment side**: human baselines under the same clock and interface, and short tasks that are easy for humans and use pixel input and low-level actions (keys, mouse, buttons). Good open starting points exist: [MiniWoB++](environments/miniwob-plusplus.md) (natively wall-clock, with a reward that decays over time), [ViZDoom](environments/vizdoom.md) in async mode, Atari and small arcade games behind a wall-clock wrapper, GameWorld-RT, and the Realtime-Bench harness with its wall, token and paused clocks.
5. **Four clock designs are in use**: wall clock, token clock, latency injection, and paused as the control (see [Play modes and clocks](#play-modes-and-clocks)). Token clocks and latency injection are reproducible and hardware independent, which matters for training.
6. **The recurring scaffold is a fast reactive loop plus a slow asynchronous thinker** ([HLA](solutions/hla.md), [DPT-Agent](solutions/dpt-agent.md), AgileThinker, [Latent Bridge](solutions/latent-bridge.md), the Thinking Machines background model). When the game runs at human reaction speeds, the fast loop is always a hand-written executor or a second model.
7. **Step 3 (post-training models to do better) is open.** No paper was found that post-trains a reasoning LLM against a live game clock and reports better realtime scores. The nearest pieces are game models trained by imitation (Lumine), deadline-aware reinforcement learning on static tasks (Timely-RL), teaching through the prompt (TORSI), and reinforcement learning on timing rewards for speech models (Kyutai).
8. **No interaction or full-duplex model has been evaluated as a game player**, and none has an output channel for actions. Robotics has mature methods for acting while inference runs (action chunking, real-time chunking, delay-conditioned training) that have not been ported to LLM game agents.

## Caveats

- Every play-mode and clock label rests on a primary source that was opened and read (repo code or the paper's full text), cited in the Basis column of each table. Items with nothing readable are listed under "Not reviewable" at the end of [environments/README.md](environments/README.md#not-reviewable).
- Numbers were extracted from arXiv HTML pages by a summarising fetch tool and should be re-checked against the papers before being quoted.
- Model names in 2026 papers are reproduced as printed.
- Two October 2026 benchmarks have nearly the same name: Realtime-Bench (arXiv 2610.22155, UT Austin and others) and RealtimeBench (arXiv 2610.20665, Peking University and Samsung).
