# Literature review: LLMs that sense, think and act in realtime

Research date: 10 November 2026.

This is a literature review for a GStar Bootcamp 2026 team project. The project's goal is large language models (LLMs) that can sense, think and act in realtime: models that keep taking in input, reasoning and acting while the world around them keeps moving, instead of having it wait for them. The project plan has three aspects, worked on together rather than in sequence:

- **Environments**: build or collect realtime environments, such as games whose clock keeps running while the model thinks.
- **Benchmarking**: test current models on those environments, to show that they do badly where humans do fine.
- **Post-training**: train models to do better on them.

The review collects published environments, benchmarks and methods that bear on each aspect. It is written for the project team and for anyone new to the topic.

**How to use it.** Read this page first. [Play modes and clocks](#play-modes-and-clocks) defines the labels used everywhere in the review, [Most relevant recent research](#most-relevant-recent-research) lists the work closest to benchmarking and post-training, and [Key takeaways](#key-takeaways) summarises what the literature shows. For more, go to the two indexes below; each links to one file per work with details, sources and, where one exists, a demo.

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

The works closest to the project's benchmarking and post-training, newest first within each group. Each name links to its file, which gives the source for its play-mode label and the full details. Note that Realtime-Bench and RealtimeBench are two different benchmarks (see [Caveats](#caveats)).

**Realtime benchmarks and environments**: the task itself runs in realtime, so the game keeps moving on its own clock (closest to benchmarking: showing that current models do badly)

| Work | Date | What it tests | Clock | Headline result | Visual |
|---|---|---|---|---|---|
| [LOLPlay](environments/lolplay.md) | Nov 2026 | 36 League of Legends tasks from 1080p screenshots, mouse and keyboard | wall clock | best task success 25% (GPT-6 Astra); higher reasoning effort never helped; two experienced human players completed all 36 | <img src="assets/gifs/lolplay.gif" alt="GPT-6 Astra playing League of Legends in LOLPlay"> |
| [Realtime-Bench](environments/realtime-bench.md) | Oct 2026 | 30 web and 20 game tasks (Pong, timed chess, Gomoku, highway) through a computer-use interface | wall, token and paused clocks on the same tasks | Claude Opus 5 at high effort: 70% success paused, 30% on the token clock, 14% on the wall clock; best wall-clock success of any model 44% | <img src="assets/gifs/realtime-bench.gif" alt="GPT-6-Astra playing Timed Chess in Realtime-Bench"> |
| [RealtimeBench](environments/realtimebench.md) (with [TORSI](solutions/torsi.md)) | Oct 2026 | six arcade games (Mario, Snake, Tetris, runner, shooter, Flappy-style) from text state | paused, live, 1.5x and 2x | average score out of 100: GPT-6.1-sol about 44 paused (averaged by this review from the paper's per-game table), 1.5 live; model ranking flips between paused and live; no code released yet | <img src="assets/gifs/realtimebench.png" alt="Figure 1 of The World Won't Wait"> |
| [ROAR](environments/roar.md) | Oct 2026 | Unity arena shooter with pixels, depth, text and audio | 250 ms and 40 ms wall-clock ticks, plus turn-based | score from 0 to 1: Gemini-3.1 Pro 0.87 turn-based, 0.34 at 40 ms, level with a rule-based bot | <img src="assets/gifs/roar.gif" alt="Gemini-3.1 Pro in ROAR real-time mode"> |
| [OmniGameArena](environments/omnigamearena.md) | Jun 2026 | 12 Unreal Engine 5 games | paused, and inference time charged to the game clock | GPT-5.5 on the SharedFloor game: 0.368 paused, 0.048 with latency charged | <img src="assets/gifs/omnigamearena.gif" alt="GPT-5.5 playing LastStand in OmniGameArena"> |
| [GameWorld-RT](environments/gameworld.md) | Apr 2026 | 34 browser games with state-verified scoring and human baselines | paused (main) and wall clock (RT) | humans 55-77% success; the realtime (RT) mode was run on two Qwen3-VL models only | <img src="assets/gifs/gameworld.gif" alt="Qwen3.5-122B-A10B playing NS-Shaft in GameWorld"> |
| [Real-Time Reasoning Gym](environments/realtime-gym.md) | Nov 2025 | Freeway, Snake, Overcooked at three cognitive loads | one environment step per N generated tokens | score from 0 to 1: a planning agent falls from 0.92 to 0.05 as time pressure rises; [AgileThinker](solutions/agile-thinker.md) falls from 0.90 to 0.58 | <img src="assets/gifs/realtime-gym.gif" alt="Three agents playing Freeway in RealtimeGym"> |
| [PokeAgent speedrun track](environments/pokeagent-speedrun.md) | 2025-26 | Pokemon Emerald to the first gym (15 milestones), ranked by wall-clock time | wall clock | winner 40:13, but it used LLM-written scripted sub-policies rather than live play; best pure-LLM harness 1:29:17; top human speedrunner 18 min | <img src="assets/gifs/pokeagent-speedrun.gif" alt="Winning PokeAgent agent in a Pokemon Emerald battle"> |
| [OpenAI Universe](environments/openai-universe.md) | 2016 | Atari, Flash and browser games in a remote desktop: the agent sees pixels and sends keyboard and mouse events | wall clock over VNC, 60 fps | no LLM results (built for reinforcement-learning agents); archived in 2018 in favour of synchronous emulators, but still the closest precedent for this interface | <img src="assets/gifs/openai-universe.gif" alt="Universe agent driving a racing Flash game"> |


**Related benchmarks with designs to avoid or copy**

| Work | Notes | Visual |
|---|---|---|
| [SpeedrunBench](environments/speedrunbench.md) (Oct 2026) | scores frames to goal against human world records. Offline, the model edits an input trace (scripted) and gets within 3-7% of the record; online, the game waits for each action (paused-live) and runs take 4-12 times as long as the record. Its demo lets a human race a recorded model run. | <img src="assets/gifs/speedrunbench.gif" alt="speedrunbench"> |
| [Orak](environments/orak.md) (2025) | pauses every game during inference; in its StarCraft II ablation without the pause, all models drop from paused scores of 75-100 to 0. | <img src="assets/gifs/orak.gif" alt="orak"> |

**Methods for thinking while acting** (closest to post-training: training models to do better)

| Work | Date | Idea | Evaluated on | Eval mode | Headline result | Visual |
|---|---|---|---|---|---|---|
| [AgileThinker](solutions/agile-thinker.md) | ICLR 2026 | a planning model streams its reasoning while a reactive model reads the partial trace and acts before each deadline; the clearest published design that pairs a fast and a slow model in an LLM game agent | [Real-Time Reasoning Gym](environments/realtime-gym.md) (Freeway, Snake, Overcooked) | realtime-live, token clock | score from 0 to 1 falls from 0.90 to 0.58 as time pressure rises, against 0.92 to 0.05 for the planning model alone | <img src="assets/gifs/agile-thinker.gif" alt="AgileThinker playing Snake in the RealtimeGym demo"> |
| [TORSI](solutions/torsi.md) | Oct 2026 | a slow teacher model writes guidance offline; a fast student model plays live on its own | [RealtimeBench](environments/realtimebench.md) (6 arcade games) | realtime-live, wall clock | the fast student's average score rises from 13.5 to 24.2 (out of 100); no code yet | <img src="assets/gifs/torsi.png" alt="TORSI method diagram"> |
| [Thinking Machines interaction models](solutions/tml-interaction-small.md) | 2026 | a full-duplex model (input and output at the same time) working in 200 ms micro-turns, with an asynchronous background model that reasons and calls tools | speech timing benchmarks only; never evaluated as a game player | realtime-live (speech) | self-reported: TimeSpeak 64.7, CueSpeak 81.7; no public weights or API | <img src="assets/gifs/tml-interaction-small.gif" alt="Thinking Machines time-awareness demo"> |
| [Lumine](solutions/lumine.md) | 2025 | a Genshin Impact agent trained by imitation (1,731 h of human play); perception at 5 Hz, action chunks at 30 Hz, thinks only when it chooses to | Genshin Impact | realtime-live for long missions; paused for its 141-task benchmark | Mondstadt Act I in 56 min, against 53 min for expert humans; 114 ms to first action without thinking, 234 ms with | <img src="assets/gifs/lumine.gif" alt="Lumine playing Genshin Impact"> |
| [Timely-RL](solutions/timely-rl.md) | 2026 | reinforcement learning (SFT, then GRPO) where the reward is zero if the answer misses a wall-clock deadline | math, GPQA, Jericho text games | static tasks with a deadline (no game clock) | on-time rate on AIME at 0.75x the time budget: 53.3%, against 30.0% for Qwen3-8B | <img src="assets/gifs/timely-rl.png" alt="Timely-RL training pipeline diagram"> |
| [Kyutai interactivity alignment](solutions/kyutai-interactivity-alignment.md) | 2026 | reinforcement learning (GRPO) with rule-based timing rewards for a full-duplex speech model | Full-Duplex-Bench v1 and v2 | realtime-live (speech) | Moshi's interruption latency falls from 1.377 s to 0.461 s | <img src="assets/gifs/kyutai-interactivity-alignment.png" alt="Kyutai timing-reward method diagram"> |
| [Real-Time Chunking](solutions/real-time-chunking.md) | 2025 | a robotics method: start computing the next chunk of actions early, keep the actions that will run during the delay, fill in the rest; not yet ported to LLM game agents | real robots and the Kinetix simulator | realtime-live (robots); injected delay (simulator) | no loss of performance with 200 ms of added delay on real robots | <img src="assets/gifs/real-time-chunking.gif" alt="Real-time chunking robot lighting a candle"> |

Timely-RL and Kyutai's work are the nearest existing post-training recipes; nobody has yet trained a model against a live game clock.

## Key takeaways

1. **Benchmarking current models under a clock is partly published already.** Between November 2025 and November 2026 a cluster of benchmarks appeared that run the same tasks paused and under a clock: Real-Time Reasoning Gym, GameWorld-RT, OmniGameArena, Realtime-Bench, RealtimeBench, ROAR and LOLPlay. The pattern is consistent: frontier reasoning models lose most of their score when the clock runs (for example 70% paused to 14% wall clock for one model in Realtime-Bench, and about 44 to 1.5 out of 100 in RealtimeBench); more reasoning effort helps when paused and hurts or does nothing live; and fast small models or realtime-API models respond quickly but are too weak.
2. **Pausing is the norm and is often stated only in an appendix.** [Orak](environments/orak.md), [Cradle](environments/cradle.md), [V-MAGE](environments/v-mage.md), [NitroGen](environments/nitrogen.md), [CombatVLA](environments/combatvla.md), [Game-TARS](environments/game-tars.md) (web games), [GameWorld](environments/gameworld.md) (main mode), [OmniGameArena](environments/omnigamearena.md) (main mode) and [VideoGameBench-Lite](environments/videogamebench.md) all pause the game during inference. Several "human-level" game results hold only under pause.
3. **Scripted routes win when allowed.** Offline trace editing gets within 3-7% of speedrun world records where live play takes 4-12 times as long, and the PokeAgent speedrun winner used LLM-written scripts. A realtime benchmark must rule these out to measure what the model can do while in the loop.
4. **What is still missing on the environment side**: human baselines under the same clock and interface, and short tasks that are easy for humans and use pixel input and low-level actions (keys, mouse, buttons). Good open starting points exist: [MiniWoB++](environments/miniwob-plusplus.md) (natively wall-clock, with a reward that decays over time), [ViZDoom](environments/vizdoom.md) in async mode, Atari and small arcade games behind a wall-clock wrapper, GameWorld-RT, and the Realtime-Bench harness with its wall, token and paused clocks.
5. **Four clock designs are in use**: wall clock, token clock, latency injection, and paused as the control (see [Play modes and clocks](#play-modes-and-clocks)). Token clocks and latency injection are reproducible and hardware independent, which matters for training.
6. **The recurring scaffold is a fast reactive loop plus a slow asynchronous thinker** ([HLA](solutions/hla.md), [DPT-Agent](solutions/dpt-agent.md), AgileThinker, [Latent Bridge](solutions/latent-bridge.md), the Thinking Machines background model). When the game runs at human reaction speeds, the fast loop is always a hand-written executor or a second model.
7. **Post-training for realtime play is open.** No paper was found that post-trains a reasoning LLM against a live game clock and reports better realtime scores. The nearest pieces are game models trained by imitation (Lumine), deadline-aware reinforcement learning on static tasks (Timely-RL), teaching through the prompt (TORSI), and reinforcement learning on timing rewards for speech models (Kyutai).
8. **No interaction or full-duplex model has been evaluated as a game player**, and none has an output channel for actions. Robotics has mature methods for acting while inference runs (action chunking, real-time chunking, delay-conditioned training) that have not been ported to LLM game agents.

## Media credits

The GIFs and figures on this page are short excerpts of each work's published material (recordings, replays or paper figures, not live runs), used with credit:

- **LOLPlay**: A recording of GPT-6 Astra (low effort) playing Lee Sin in League of Legends on LOLPlay Task002, with the wall clock running: its status goes from "waiting for model" to "executing action batch" (Q skillshot on a jungle camp, level up) to the next step while the in-game timer moves from 03:04 to 03:09. Rearranged from the left pane of the side-by-side video (status panel and timer enlarged and moved above the game view). Source: [Clip from the LOLPlay project page (answers111.github.io/LOL-Play-homepage), Zhaojian Yu et al.](https://answers111.github.io/LOL-Play-homepage/).
- **Realtime-Bench**: A recording of GPT-6-Astra (high effort) playing White in Realtime-Bench's Timed Chess in wall-clock mode, sped up 11x: its queen raids Black's pieces while its 2:00 clock runs down to 0:39 (this run scored reward 1.0). Source: [Trial recording from the Realtime-Bench Harbor trajectory browser (realtimeagents.org/harbor)](https://realtimeagents.org/harbor/).
- **RealtimeBench**: Paper figure: while the model is still thinking, the game keeps running and the late action causes a crash in Mario, Temple and Snake (an 824 ms delay against a 667 ms tick). Source: [Figure 1 from Pan, Li, Shen, Ding, Tang and Zhang, "The World Won't Wait" (arXiv 2610.20665)](https://arxiv.org/abs/2610.20665).
- **ROAR**: Recorded clip of Gemini-3.1 Pro in ROAR's real-time mode (40 ms tick): the game clock runs from 03:04 to 02:57 while the agent stands aiming and turret fire drops its health from 100 to 16. Source: [Clip from the ROAR GitHub README (github.com/tb6147877/ROAR), by Dawei Wang et al.](https://github.com/tb6147877/ROAR).
- **OmniGameArena**: A recording of GPT-5.5 playing LastStand in OmniGameArena's latency-charged mode: the countdown clock keeps running (01:44 to 01:32) while tiles flash red and drop away, and the clip ends on "GAME OVER" when the character falls. Source: [Clip from the OmniGameArena project page (mxlin043.github.io/OmniGameArena)](https://mxlin043.github.io/OmniGameArena/).
- **GameWorld**: A recording from the authors' archived live stream: Qwen3.5-122B-A10B plays NS-Shaft. Over 8 s the step counter goes from 063 to 066 while the LIVE countdown drops from 00:40 to 00:33 at wall-clock speed. The stream does not say whether this was the paused or the RT track. Source: [Clip from the GameWorld authors' official YouTube live stream (youtube.com/@gameworld-bench)](https://www.youtube.com/watch?v=vcOLE5vcKro).
- **Real-Time Reasoning Gym**: A recorded RealtimeGym Freeway replay (Hard load, Extreme time pressure on the token clock) with the Reactive, Planning and AgileThinker agents side by side, showing the step counter, each agent's score and its next action, captured from the authors' replay viewer (not live play). Source: [Frames captured from the RealtimeGym interactive demo (realtimegym.saltlab.stanford.edu), Wen et al., Stanford SALT](https://realtimegym.saltlab.stanford.edu/).
- **PokeAgent**: A recording of the winning team Heatz's agent in its first Pokemon Emerald battle: it picks FIGHT, then TACKLE, against a wild Zigzagoon. The video is edited from the 40:13 run, so no clock is visible. Source: [Footage: team Heatz (uploader Junik Bae), winning PokeAgent Challenge speedrun submission video, linked from the official leaderboard at pokeagent.github.io/leaderboard.html](https://youtu.be/A28OJRl3R8o).
- **OpenAI Universe**: A recording of a trained Universe RL agent driving a Formula-style racing Flash game, with the in-game race timer running in the top right. Cropped to one of three side-by-side games. Source: [Video: OpenAI, "Universe" launch post (5 Dec 2016), clip "Three trained agents playing several racing Flash games", via the Internet Archive.](https://web.archive.org/web/20161207112259/https://openai.com/blog/universe/).
- **SpeedrunBench**: A recording of GPT-5.6 Sol's SpeedrunBench run through SuperTux level 1-1 "Welcome to Antarctica" (finished in 0:33.047), with Tux running and jumping past enemies. Source: [Footage: SpeedrunBench (Fujinuma, Kamahori, Koike et al.; Patronus AI), speedrunbench.com play page; game: SuperTux.](https://speedrunbench.com/play).
- **Orak**: A screen recording of Claude Sonnet 4 calling Orak's MCP tools (load-obs, send-agent-module-response, dispatch-final-action) while Baba Is You waits behind a PAUSE overlay, then moves one step. Source: [Recording from the Orak leaderboard page, KRAFTON AI (Park et al., arXiv 2506.03610)](https://krafton-ai.github.io/orak-leaderboard/).
- **AgileThinker**: A replay of a recorded AgileThinker game of Snake from the RealtimeGym demo, with its Agent Reasoning panel open and updating each turn. The card was resized for capture. Source: [Wen, Ye, Zhang, Yang, Zhu (SALT Lab, Stanford): RealtimeGym interactive demo, realtimegym.saltlab.stanford.edu](https://realtimegym.saltlab.stanford.edu/).
- **TORSI**: Figure from the paper: the TORSI method diagram, with a fast model playing Mario and Flappy Bird live using frozen guidance that a slow model writes between runs. Source: [Figure 5 from Pan et al., "The World Won't Wait" (RealtimeBench / TORSI), arXiv 2610.20665, 2026.](https://arxiv.org/abs/2610.20665).
- **Thinking Machines interaction models**: Recording from the authors' Time-awareness demo: three people talk to the interaction model on a phone on the table, while an on-screen timer counts from 00:00 to 00:05. Source: [Video: Thinking Machines Lab, "Time-awareness" demo for Interaction Models (May 2026), YouTube @thinkymachines](https://www.youtube.com/watch?v=sqJNfze19jA).
- **Lumine**: Recording of Lumine playing Genshin Impact: its inner monologue appears as a subtitle (planning to shoot the Hilichurl watchtower with a bow character), and the keyboard-and-mouse overlay lights up as it fires and then runs toward the camp. Source: [Footage: ByteDance Seed, Lumine project (lumine-ai.org), Mondstadt main-story playthrough on YouTube.](https://www.youtube.com/watch?v=C5y_5tFlhi0).
- **Timely-RL**: A diagram from the paper: a timer adds up scaled inference time and tool execution time while the model works, and the episode either returns an answer or times out. Source: [Figure 1 from Ma et al., "Timely-RL" (arXiv 2601.16486)](https://arxiv.org/abs/2601.16486).
- **Kyutai interactivity alignment**: Figure from the paper: a conversation context goes into the full-duplex speech model, its sampled replies are scored with timing rewards (+1.6, -0.5, -1.1) and the scores feed back through GRPO. Source: [Figure 1 from Ohashi, Zeghidour, Defossez, Kharitonov (Kyutai), arXiv 2606.11167](https://arxiv.org/abs/2606.11167).
- **Real-Time Chunking**: Recording at 1x speed of a robot with real-time chunking (left) striking a match and lighting a candle on a pie, while the synchronous-inference robot (right) is still picking up the matchbox. Source: [Video: Physical Intelligence, "Real-Time Action Chunking with Large Models" (Black, Galliker, Levine), pi.website](https://www.pi.website/research/real_time_chunking).

## Caveats

- Every play-mode and clock label rests on a primary source that was opened and read (repo code or the paper's full text), cited in the Basis column of each table. Items with nothing readable are listed under "Not reviewable" at the end of [environments/README.md](environments/README.md#not-reviewable).
- Numbers were extracted from arXiv HTML pages by a summarising fetch tool and should be re-checked against the papers before being quoted.
- Model names in 2026 papers are reproduced as printed.
- Two October 2026 benchmarks have nearly the same name: Realtime-Bench (arXiv 2610.22155, UT Austin and others) and RealtimeBench (arXiv 2610.20665, Peking University and Samsung).
