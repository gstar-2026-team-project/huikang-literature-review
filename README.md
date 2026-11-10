# Literature review: LLMs that sense, think and act in realtime

Research date: 10 November 2026.

## Scope

This review supports a project to (1) build or collect realtime environments, (2) show that current models do badly on them while humans do fine, and (3) post-train models to improve. It covers:

- **[environments.md](environments.md)**: game environments and benchmarks from RL-era platforms to 2026 LLM/VLM benchmarks, plus near neighbours (trading, negotiation, computer use, full-duplex speech, streaming video, robotics). It has a comparison table, a section per environment grouped by play mode, and a shortlist for first environments.
- **[solutions.md](solutions.md)**: agent scaffolds, realtime model architectures, RL and decision models, and post-training methods, each with a summary table and notes, then a list of gaps.

Out of scope: code execution as the way of solving a task, image and sound generation, pre-training or new architectures from scratch.

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

- Every play-mode and clock label rests on a primary source that was opened and read (repo code or the paper's full text), cited in the Basis column of each table. Items with nothing readable are listed under "Not reviewable" at the end of environments.md.
- Numbers were extracted from arXiv HTML pages by a summarising fetch tool and should be re-checked against the papers before being quoted.
- Model names in 2026 papers are reproduced as printed.
- Two October 2026 benchmarks have nearly the same name: Realtime-Bench (arXiv 2610.22155, UT Austin and others) and RealtimeBench (arXiv 2610.20665, Peking University and Samsung).
