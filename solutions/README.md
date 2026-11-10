# Solutions for realtime LLM agents

Research date: 10 November 2026. Part 2 of the review; see [README.md](../README.md) for scope and [environments](../environments/README.md) for Part 1.

This folder has one file per work. This index holds the conventions, the four summary tables, a list of all solution files by category, the cross-cutting notes, the per-category "What the team could reuse" lists and the gaps.

**Conventions.** Evaluation play mode is labelled realtime-live (RL), paused-live (PL), scripted (S), or "static" where there is no environment clock at all (QA, math, tool benchmarks). Every evaluation-mode label rests on an opened primary source, given in each table's Basis column ("code: <file>" or "paper: <section>" with a short quoted phrase); where a paper is silent, the label follows from what it does say and the entry says so. Numbers were extracted from arXiv HTML by a summarising fetch tool; re-check before quoting. Model names from 2026 papers are reproduced as printed. In the per-work files, play modes are spelled out, and each file links to the [environment](../environments/README.md) files it was evaluated on.

Contents: [Solution files](#solution-files-by-category) | [1. Scaffolds](#1-agent-scaffolds-on-existing-llms) | [2. Realtime architectures](#2-realtime-model-architectures) | [3. RL and decision models](#3-rl-and-decision-models) | [4. Post-training](#4-post-training-methods) | [5. Gaps](#5-gaps-what-nobody-appears-to-have-done)

**Demos.** Every solution file whose work has a public demo now has a Demo row in its field table (after Links) and a `## Demo` section after the details, recorded from headless-browser visits on 10 November 2026. Each bullet says what was done, what the demo shows and what it shows about play mode, and whether it was seen in a recording or run live. Where a demo conflicts with a file's play-mode label or Basis, the Demo section has a "Note:" bullet and the label is unchanged. No solution demo is a game a human can play ([Moshi](moshi.md) lets a human talk to the live model). Demos showing a model acting against a running clock, all seen in recordings: LLM scaffolds [DPT-Agent](dpt-agent.md), [HLA](hla.md), [FPX](fpx.md) and [Lumine](lumine.md), plus [AgileThinker](agile-thinker.md) (replays under RealtimeGym's token clock); streaming models [Moshi](moshi.md) and [VideoLLM-online](videollm-online.md); RL agents [OpenAI Five](openai-five.md), [AlphaStar](alphastar.md) and [GT Sophy](gt-sophy.md); robot policies [pi0](pi0.md), [Real-Time Chunking](real-time-chunking.md), [Hi Robot](hi-robot.md), [Fast-in-Slow (FiS-VLA)](fis-vla.md) and [Real-Time EXPO-FT](real-time-expo-ft.md).

## Solution files by category

### Agent scaffolds

- [AgileThinker](agile-thinker.md)
- [TORSI](torsi.md)
- [DPT-Agent](dpt-agent.md)
- [HLA](hla.md)
- [RRARA](rrara.md)
- [Latent Bridge](latent-bridge.md)
- [SwarmBrain](swarmbrain.md)
- [HIMA](hima.md) (also post-training)
- [Parallelized Planning-Acting](parallelized-planning-acting.md)
- [FPX (Win Fast or Lose Slow)](fpx.md)
- [Speculative Actions](speculative-actions.md)
- [Async I/O + Speculative Tool Calling / Async-SFT](async-sft.md) (also post-training)
- [Asynchronous Reasoning](asynchronous-reasoning.md)
- [Are LRMs Interruptible? (interruptibility diagnostic)](are-lrms-interruptible.md)
- [Never Stop Thinking](never-stop-thinking.md)
- [Second Thought](second-thought.md)
- [AsyncLM](asynclm.md)
- [LiveMind](livemind.md)
- [SwiftSage](swiftsage.md)
- [Talker-Reasoner](talker-reasoner.md)
- [Cradle](cradle.md)
- [Voyager](voyager.md)
- [PORTAL](portal.md)
- [CodeClash](codeclash.md)
- [AgentTime](agenttime.md)
- [Hi Robot](hi-robot.md)
- [Figure Helix](figure-helix.md)
- [FiS-VLA](fis-vla.md)

### Realtime model architectures

- [TML-Interaction-Small (Thinking Machines Lab interaction models)](tml-interaction-small.md)
- [Moshi](moshi.md)
- [PersonaPlex](personaplex.md)
- [MiniCPM-o 4.5](minicpm-o-4-5.md)
- [Duplex models / MiniCPM-Duplex](duplex-models.md)
- [SyncLLM](syncllm.md)
- [OmniFlatten](omniflatten.md)
- [dGSLM](dgslm.md)
- [gpt-realtime-2 (Realtime API)](gpt-realtime-2.md)
- [Gemini Live (2.5, 3.1 Flash Live)](gemini-live.md)
- [Qwen3-Omni / Qwen3.5-Omni](qwen3-omni.md)
- [Realtime-Venus](realtime-venus.md)
- [VideoLLM-online](videollm-online.md)
- [Dispider](dispider.md)
- [StreamingThinker](streamingthinker.md) (also post-training)
- [Flash-VStream](flash-vstream.md)
- [StreamBridge](streambridge.md)
- [LiveCC](livecc.md)
- [StreamingVLM](streamingvlm.md)
- [OmniMMI / M4](omnimmi-m4.md)
- [Proact-VL](proact-vl.md)
- [STITCH](stitch.md) (also post-training)
- [SHANKS](shanks.md)
- [Mini-Omni-Reasoner](mini-omni-reasoner.md) (also post-training)
- [FLAIR](flair.md) (also post-training)

### RL and decision models

- [DQN / Atari line](dqn-atari.md)
- [OpenAI Five](openai-five.md)
- [AlphaStar](alphastar.md)
- [FTW](ftw.md)
- [GT Sophy](gt-sophy.md)
- [Phillip / slippi-ai](phillip-slippi-ai.md)
- [VPT](vpt.md)
- [STEVE-1](steve-1.md)
- [GROOT](groot.md)
- [ROCKET](rocket.md)
- [JARVIS-VLA](jarvis-vla.md)
- [DreamerV3 / Dreamer 4](dreamer.md)
- [SIMA](sima.md)
- [SIMA 2](sima-2.md) (also post-training)
- [Lumine](lumine.md) (also post-training)
- [Game-TARS](game-tars.md) (also post-training)
- [NitroGen](nitrogen.md)
- [Open-P2P](open-p2p.md)
- [CombatVLA](combatvla.md) (also post-training)
- [pi0](pi0.md)
- [ACT (action chunking)](act.md)
- [Gemini Robotics](gemini-robotics.md)
- [Real-Time Chunking](real-time-chunking.md)
- [SmolVLA async](smolvla-async.md)
- [VLASH](vlash.md)
- [A2C2](a2c2.md)
- [D2E](d2e.md)

### Post-training methods

- [UI-TARS-2](ui-tars-2.md)
- [Odysseus](odysseus.md)
- [Orak fine-tuning](orak-fine-tuning.md)
- [Think in Games](think-in-games.md)
- [Timely-RL](timely-rl.md)
- [AnytimeReasoner](anytimereasoner.md)
- [Elastic Reasoning](elastic-reasoning.md)
- [BudgetThinker](budgetthinker.md)
- [L1](l1.md)
- [AdaptThink](adaptthink.md)
- [Thinkless](thinkless.md)
- [Interleaved Reasoning](interleaved-reasoning.md)
- [Dualformer](dualformer.md)
- [Distilling System 2 into 1](distilling-system-2-into-1.md)
- [Kyutai interactivity alignment](kyutai-interactivity-alignment.md)
- [Training-time RTC](training-time-rtc.md)
- [Real-Time EXPO-FT](real-time-expo-ft.md)
- [Think at 5 Hz, Act at 20 Hz](think-at-5hz-act-at-20hz.md) (also a robotics dual system, scaffolds notes)

---

## 1. Agent scaffolds on existing LLMs

### Summary

| Work | Year | Idea | Evaluated on | Eval mode | Headline result | Link | Basis |
|---|---|---|---|---|---|---|---|
| [AgileThinker](agile-thinker.md) | 2025 | Planning thread streams reasoning; reactive thread reads its partial trace and acts before each deadline | RealtimeGym (Freeway, Snake, Overcooked) | RL, token clock | 0.90 to 0.58 as pressure rises, against 0.92 to 0.05 for planning alone | [arXiv 2511.04898](https://arxiv.org/abs/2511.04898) | paper §2: "the environment steps forward at a fixed rate, even when the agent has not finished thinking"; §6 wall-clock run |
| [TORSI](torsi.md) | 2026 | Slow teacher writes guidance offline; fast student plays live alone | RealtimeBench (6 arcade games) | RL, wall clock | Fast student 13.51 to 24.19 | [arXiv 2610.20665](https://arxiv.org/abs/2610.20665) | paper §3: "While a response is pending, the game keeps running with the previous control still active"; §4 the student acts "without teacher calls" |
| [DPT-Agent](dpt-agent.md) | 2025 | FSM (rewritten by the LLM) acts every tick; asynchronous reflection and theory of mind | Overcooked at 4 Hz | RL (part S) | 46.6 against ReAct 15.5 | [arXiv 2502.11882](https://arxiv.org/abs/2502.11882) | code: `llm_agent_run_dpt_exp1.py` (`env.step` loop paced by `asyncio.sleep(0.25)`); paper: "each timestep corresponds to 0.25 seconds in the real world" |
| [HLA](hla.md) | 2023 | Slow LLM + fast LLM + scripted executor | Overcooked with humans, about 3 Hz | RL (paper; no code) | Macro latency 1.07 s against 4.16 s slow-only | [arXiv 2312.15224](https://arxiv.org/abs/2312.15224) | paper §1: Overcooked where "players collaborate at a rate of approximately 3Hz"; executor acts while the LLMs run; no pause described |
| [RRARA](rrara.md) | 2025-26 | Rule reflex acts at once; asynchronous LLM reflector corrects | HAZARD with injected latency | RL (INJECT) | Value rate 0.44 against best plain LLM 0.25 | [arXiv 2506.07223](https://arxiv.org/abs/2506.07223) | paper §3: "After each decision, we advance the simulator by frames" (frames = latency x 30 FPS) |
| [Latent Bridge](latent-bridge.md) | 2026 | Frozen fast VLM at 15 Hz + frozen slow VLM at 1 Hz, linked by a trained latent channel | 7 Atari games | PL (synchronous tick loop; slow model every 15 ticks) | Wins on 2 of 7 games against a text bridge | [arXiv 2606.24470](https://arxiv.org/abs/2606.24470) | code: `src/eval/benchmark.py:110-186` (`fast.predict_action` -> `env.step` -> inline `slow.emit`), `src/env/atari_wrapper.py` 4 frames per tick |
| [SwarmBrain](swarmbrain.md) | 2024 | LLM strategy + reflex state machine | StarCraft II vs built-in AI | RL | 76% against Hard | [arXiv 2401.17749](https://arxiv.org/abs/2401.17749) | code: `swarmbrain_launch.py:2666-2671` `run_game(..., realtime=True)`; LLM via `run_in_executor` (`swarmbrain.py:79`) |
| [HIMA](hima.md) | 2025 | Small fine-tuned agents propose long build sequences; planner called about 11 times a game | StarCraft II | PL by default (`--realtime` off); RL with the flag | 100% to 16% across AI levels 4-10 | [arXiv 2508.06042](https://arxiv.org/abs/2508.06042) | code: `main.py:23` `--realtime` default False, `main.py:70` `run_game(realtime=args.realtime)`; paper does not say which mode produced the win rates |
| [Parallelized Planning-Acting](parallelized-planning-acting.md) | 2025 | Planning and acting threads; single-slot buffer where a new plan interrupts the running action | Minecraft, unpaused server | RL (skills are scripted) | 3 agents halve diamond-armor time | [arXiv 2503.03505](https://arxiv.org/abs/2503.03505) | paper §3.2: "The game server operates continuously without pausing during interactions with LLMs" |
| [FPX (Win Fast or Lose Slow)](fpx.md) | 2025 | Mixed-precision quantisation as a latency knob | Street Fighter, HFTBench | RL | 3B at 195 ms beats 7B; 14B best for trading | [arXiv 2505.19481](https://arxiv.org/abs/2505.19481) | code: `StreetFighter/GameEngine/Engine/game.py` (continuous `env.step`, action 0 when none pending); `HFTBench/Environment/TradingEnv.py` (measured delay worsens fill price) |
| [Speculative Actions](speculative-actions.md) | 2025 | Fast model guesses the slow actor's next step; pre-execute and commit on match | chess, tau-bench, HotpotQA, OS tuning | PL / static | 19.5% time saved in chess | [arXiv 2510.04371](https://arxiv.org/abs/2510.04371) | paper §1: "Turn-based gameplay (e.g., chess)"; implemented on TextArena |
| [Async I/O + Speculative Tool Calling](async-sft.md) | 2026 | Event-driven loop decoupled from streaming speech and tool returns | tool benchmarks with simulated streaming input | static, simulated streaming clock | About 2x lower latency for fine-tuned 3B models | [arXiv 2605.13360](https://arxiv.org/abs/2605.13360) | paper §5: "We evaluate our method by simulating streaming updates from speech-to-text" |
| [Asynchronous Reasoning](asynchronous-reasoning.md) | 2025 | Training-free concurrent think/read/write in one model via position manipulation | math, commonsense, safety QA | static | First non-thinking token within 5 s | [arXiv 2512.10931](https://arxiv.org/abs/2512.10931) | paper §4: MATH-500, MMLU-Pro, GPQA, AIME-2025, ZebraLogic; delay measured as TTS silence time |
| [Are LRMs Interruptible?](are-lrms-interruptible.md) | 2025 | Diagnostic: interrupts and context updates mid-reasoning | math and code QA | static | Up to 60% accuracy drop | [arXiv 2510.11713](https://arxiv.org/abs/2510.11713) | paper §3: "we primarily use relative cut points" in the reasoning trace; GSM-8K, Math-500, AIME, LiveCodeBench |
| [Never Stop Thinking](never-stop-thinking.md) | 2026 | Interrupt-and-resume orchestrator so a text LLM thinks while listening and speaking | ReactiveBench (voice scenarios) | static (scripted interrupts, simulated speech rate) | Latency -19% | [arXiv 2609.17416](https://arxiv.org/abs/2609.17416) | paper §3: "interrupts are realized at the transcript level by truncating the agent's prior turn"; App. A simulated speech at 3.5 words/s |
| [Second Thought](second-thought.md) | 2026 | Fork reasoning branches during the act/observe wait | agent benchmarks | PL (agentic benchmarks) | Fewer turns in 9 of 9 pairs | [arXiv 2608.13667](https://arxiv.org/abs/2608.13667) | paper §1: SWE-Bench Pro, Terminal-Bench 2.1, tau-bench; §5 paired wall-clock replay |
| [AsyncLM](asynclm.md) | 2024 | Keep generating while tools run; interrupt tokens on return | BFCL | static | 1.6-5.4x lower latency | [arXiv 2412.07017](https://arxiv.org/abs/2412.07017) | paper §6: BFCL tasks; task completion latency |
| [LiveMind](livemind.md) | 2024 | Infer on a partial prompt while input streams | MMLU | static | Latency -84% | [arXiv 2406.14319](https://arxiv.org/abs/2406.14319) | paper §4.1 "Streaming input simulation" |
| [SwiftSage](swiftsage.md) | 2023 | Small cloned fast model + GPT-4 planner, heuristic switch | ScienceWorld | PL | (not extracted) | [arXiv 2305.17390](https://arxiv.org/abs/2305.17390) | paper §2: ScienceWorld text environment, one action per step |
| [Talker-Reasoner](talker-reasoner.md) | 2024 | Fast talker + slow reasoner with shared memory | sleep-coaching example | none | no quantitative evaluation | [arXiv 2410.08328](https://arxiv.org/abs/2410.08328) | paper §4: case study with "Qualitative Results" only |
| [Cradle](cradle.md) | 2024 | Six-module GPT-4o pipeline writing code skills | RDR2, Stardew and others | PL in every environment | about 62 s per decision | [arXiv 2403.03186](https://arxiv.org/abs/2403.03186) | code: `cradle/provider/execute/skill_execute.py` (unpause -> skill -> pause); paper §4 "we must pause those game environments" |
| [Voyager](voyager.md) | 2023-25 | LLM writes code, behaviour trees or bots | Minecraft, 3D games, code arenas | S (Voyager also pauses the server during LLM calls) | out of scope | [Voyager](https://arxiv.org/abs/2305.16291) | code: Voyager `voyager/env/bridge.py:113-124` |
| [PORTAL](portal.md) | 2023-25 | LLM writes code, behaviour trees or bots | Minecraft, 3D games, code arenas | S (Voyager also pauses the server during LLM calls) | out of scope | [arXiv 2503.13356](https://arxiv.org/abs/2503.13356) | PORTAL paper §2 "Rather than relying on LLM inference during gameplay" |
| [CodeClash](codeclash.md) | 2023-25 | LLM writes code, behaviour trees or bots | Minecraft, 3D games, code arenas | S (Voyager also pauses the server during LLM calls) | out of scope | [arXiv 2511.00839](https://arxiv.org/abs/2511.00839) | CodeClash paper §2 "LMs do not play the games directly" |

### Supporting evidence that more reasoning hurts under a clock

[Realtime-Bench](../environments/realtime-bench.md) (Claude Opus 5 at high effort: 70% paused, 14% wall clock), [LOLPlay](../environments/lolplay.md) (higher effort never helps), [ROAR](../environments/roar.md) (ReAct scaffolds help turn-based play only), [Orak's unpaused StarCraft II](../environments/orak.md) (scores to 0), [OSWorld-Human](../environments/osworld-human.md) (planning and reflection calls dominate latency), [AgentTime](agenttime.md) ([arXiv 2610.09944](https://arxiv.org/abs/2610.09944): agents land within 5% of a requested working duration in 63%, 39% and 4% of runs for three frontier agents).

### What the team could reuse
- Baselines: reactive-only, planning-only, [AgileThinker](agile-thinker.md), FSM safety net ([DPT](dpt-agent.md)), offline guidance ([TORSI](torsi.md)).
- Harness pieces: token clock, latency injection, default action on timeout, per-level latency reporting, single-slot interrupt buffer.
- The [interruptibility](are-lrms-interruptible.md) protocol and datasets as a static pre-test for mid-thought steering.

---

## 2. Realtime model architectures

Models trained to take input and produce output concurrently. Every evaluation below is conversational or perception-only. None of these models has been evaluated as a player on a verifiable realtime game or control task, and none has an action output channel.

### Summary

| Model | Year | Channels (in / out) | Tick | How thinking coexists with output | Open / fine-tunable | Link | Eval mode | Basis |
|---|---|---|---|---|---|---|---|---|
| [TML-Interaction-Small](tml-interaction-small.md) | 2026 | text, audio, video / text, audio | 200 ms micro-turns | Separate asynchronous background model reasons and calls tools | No weights or public API as of the May 2026 post | [blog](https://thinkingmachines.ai/blog/interaction-models/) | RL (speech); no game or control evaluation | docs: blog (saved) "continuous input and output streams split into micro-turns" of 200 ms; benchmarks self-reported |
| [Moshi](moshi.md) | 2024 | user audio / own audio + text | 80 ms (12.5 Hz), 17 streams | "Inner monologue" text stream, which is the transcript of its own speech | Open weights and code | [arXiv 2410.00037](https://arxiv.org/abs/2410.00037) | RL (speech) operation; reported evaluation static | paper: abstract "theoretical latency of 160ms, 200ms in practice"; §5.6 continuations of 10 s Fisher prompts |
| [PersonaPlex](personaplex.md) | 2026 | as Moshi + role and voice prompts | 80 ms | as Moshi | Weights released under the NVIDIA Open Model License (gated; HF API metadata and repo README) | [arXiv 2602.06053](https://arxiv.org/abs/2602.06053) | RL (speech) | paper §2: "user input audio is streamed in and the model's corresponding generated audio is captured and evaluated" |
| [MiniCPM-o 4.5](minicpm-o-4-5.md) | 2026 | video, audio, text / text, speech | 1 s windows | Listen/speak control token per window; no reasoning stream | Open, Apache-2.0 per model card | [arXiv 2604.27393](https://arxiv.org/abs/2604.27393) | offline replay (LiveSports-3K-CC); static elsewhere | paper §6.1 LiveSports-3K-CC "an audio-free full-duplex benchmark"; model card "decides at a frequency of 1Hz to speak or not" |
| [Duplex models / MiniCPM-Duplex](duplex-models.md) | 2024 | text / text | time slices | Reads a slice, writes a slice or stays idle | Fine-tuned from MiniCPM | [arXiv 2406.15718](https://arxiv.org/abs/2406.15718) | static (benchmarks) + RL (speech) user study | paper §4.4 "the user's speech is processed every 2 seconds"; §4.5 user study |
| [SyncLLM](syncllm.md) | 2024 | two speech streams | 160-240 ms chunks | Predicts the user's next chunk to hide latency | Llama-3-8B fine-tune | [arXiv 2409.15594](https://arxiv.org/abs/2409.15594) | static (continuation) + RL (speech, simulated one-chunk latency) | paper §5.4 "We simulate LLM-user interaction using LLM-LLM interaction with one-chunk latency" |
| [OmniFlatten](omniflatten.md) | 2024 | speech + text | flattened streams | Staged post-training of a small GPT, no architecture change | research | [arXiv 2410.17799](https://arxiv.org/abs/2410.17799) | offline replay | paper §4: "a predefined user speech input while setting a 1.5-second threshold" |
| [dGSLM](dgslm.md) | 2022 | two audio channels | units | none (textless) | research | [arXiv 2203.16502](https://arxiv.org/abs/2203.16502) | static | paper §4.3.2: 90-second continuations of 30-second prompts |
| [gpt-realtime-2 (Realtime API)](gpt-realtime-2.md) | 2026 | text, audio, images / text, audio | harness turn detection | Reasoning-effort levels; higher effort raises latency | API only, no fine-tuning | [docs](https://developers.openai.com/api/docs/models/gpt-realtime-2) | RL (speech) service; no game evaluation by the vendor | docs: model page, VAD guide (`server_vad` / `semantic_vad`), prompting guide (reasoning effort); fine-tuning "Not supported" |
| [Gemini Live (2.5, 3.1 Flash Live)](gemini-live.md) | 2025-26 | audio, video frames, text / audio, text | session streaming | `thinkingLevel`, default minimal | API only | [docs](https://ai.google.dev/gemini-api/docs/live-guide) | RL (speech) service | docs: Live API overview and capabilities guide (saved); video at most 1 frame per second |
| [Qwen3-Omni / Qwen3.5-Omni](qwen3-omni.md) | 2025-26 | audio, video, text / text, speech | streaming output | Thinker-Talker; thinking precedes output | Qwen3-Omni Apache-2.0 | [arXiv 2509.17765](https://arxiv.org/abs/2509.17765) | static | paper (Qwen3-Omni) §1: "Across 36 audio and audio-visual benchmarks"; "theoretical end-to-end first-packet latency of 234 ms" |
| [Realtime-Venus](realtime-venus.md) | 2026 | audio, video / speech | full duplex | Front-end model delegates to a background harness | not checked | [arXiv 2609.13814](https://arxiv.org/abs/2609.13814) | RL (speech, Full-Duplex-Bench) + static | paper §6 evaluation tables |
| [VideoLLM-online](videollm-online.md) | 2024 | video frames / text | per frame | Decides per frame to stay silent or speak | Open | [arXiv 2406.11816](https://arxiv.org/abs/2406.11816) | offline replay | paper §4: Ego4D "timestamp-narration" streaming set |
| [Dispider](dispider.md) | 2025 | video / text | per clip | Separate perception, decision and asynchronous reaction modules | research | [arXiv 2501.03218](https://arxiv.org/abs/2501.03218) | offline replay | paper §1: evaluated on StreamingBench and offline long-video benchmarks |
| [StreamingThinker](streamingthinker.md) | 2025 | streaming text / text | per sentence | Reasons while the prompt streams; parallel KV caches | Open, Qwen3 fine-tune | [arXiv 2510.17238](https://arxiv.org/abs/2510.17238) | static (simulated streaming input) | paper §4.1 latency definition with simulated input speed |

### What the team could reuse
- Baselines for the "interaction/realtime models" column: [gpt-realtime-2](gpt-realtime-2.md) and [Gemini Live](gemini-live.md) through their APIs, [Moshi](moshi.md)/[PersonaPlex](personaplex.md) and [MiniCPM-o 4.5](minicpm-o-4-5.md) locally. Game pixels must be pushed as frames, and actions must be parsed from text or speech.
- Serialisation ideas for post-training a text model: micro-turns, time slices, a listen/act control token per window, a parallel inner-monologue stream.

---

## 3. RL and decision models

### Summary

| System | Year | Domain | Action rate and reaction handling | Eval mode | Link | Basis |
|---|---|---|---|---|---|---|
| [DQN / Atari line](dqn-atari.md) | 2015- | Atari | frameskip 4 (15 Hz); inference time free | PL | [ALE docs](https://ale.farama.org/environments/) | paper: Nature 2015 Methods "the agent sees and selects actions on every kth frame"; human tester "not allowed to pause" |
| [OpenAI Five](openai-five.md) | 2019 | Dota 2 | acts every 4th frame (7.5 Hz); 217 ms average reaction | RL vs humans | [arXiv 1912.06680](https://arxiv.org/abs/1912.06680) | paper §2: "OpenAI Five only acts on every 4th frame"; "react to a game event in 217ms on average" |
| [AlphaStar](alphastar.md) | 2019 | StarCraft II | camera interface and limits on action frequency agreed with a professional player | RL on Battle.net | [blog](https://deepmind.google/blog/alphastar-grandmaster-level-in-starcraft-ii-using-multi-agent-reinforcement-learning/) | docs: DeepMind blog (saved) "viewing the world through a camera, and stronger limits on the frequency of its actions" |
| [FTW](ftw.md) | 2018-19 | Quake III CTF | reacts in 258 ms against 559 ms for humans; no win-rate loss up to 375 ms added delay | RL vs humans | [arXiv 1807.01281](https://arxiv.org/abs/1807.01281) | paper: "respond to newly appeared opponents in 258ms, compared with 559ms for humans"; "up to 375ms did not effect the win probability" |
| [GT Sophy](gt-sophy.md) | 2022 | Gran Turismo | 10 Hz control, game runs only in real time | RL on PS4 | [paper page](https://ai.sony/publications/Outracing-champion-Gran-Turismo-drivers-with-deep-reinforcement-learning) | paper: "GT Sophy interacted with the game at 10 Hz"; "Although GT ran only in real time" |
| [Phillip / slippi-ai](phillip-slippi-ai.md) | 2017- | Melee | 12-15 frame imposed delay + predictive model | RL in netplay | [arXiv 1810.07286](https://arxiv.org/abs/1810.07286) | paper (1810.07286) §1: "we add fixed delay between the time an agent chooses an action" and when it is applied; "12 frames to be the lowest" human-plausible delay |
| [VPT](vpt.md) | 2022-25 | Minecraft | 20 Hz native interface; synchronous simulator | PL | [arXiv 2206.11795](https://arxiv.org/abs/2206.11795) | paper (VPT) App. C: client and server "run in the same thread ... slower or faster than real time"; code: MineRL `_multiagent.py` synchronous token |
| [STEVE-1](steve-1.md) | 2022-25 | Minecraft | 20 Hz native interface; synchronous simulator | PL |  | paper (VPT) App. C: client and server "run in the same thread ... slower or faster than real time"; code: MineRL `_multiagent.py` synchronous token |
| [GROOT](groot.md) | 2022-25 | Minecraft | 20 Hz native interface; synchronous simulator | PL |  | paper (VPT) App. C: client and server "run in the same thread ... slower or faster than real time"; code: MineRL `_multiagent.py` synchronous token |
| [ROCKET](rocket.md) | 2022-25 | Minecraft | 20 Hz native interface; synchronous simulator | PL |  | paper (VPT) App. C: client and server "run in the same thread ... slower or faster than real time"; code: MineRL `_multiagent.py` synchronous token |
| [JARVIS-VLA](jarvis-vla.md) | 2022-25 | Minecraft | 20 Hz native interface; synchronous simulator | PL |  | paper (VPT) App. C: client and server "run in the same thread ... slower or faster than real time"; code: MineRL `_multiagent.py` synchronous token |
| [DreamerV3 / Dreamer 4](dreamer.md) | 2023-25 | Minecraft and others | simulator-stepped | PL (agent evaluation) | [arXiv 2509.24527](https://arxiv.org/abs/2509.24527) | paper (DreamerV3 v1) App.: MineRL, "36000 steps, corresponding to 30 minutes at the control frequency of 20Hz"; Dreamer 4 §4.1 follows the VPT protocol |
| [SIMA](sima.md) | 2024 | commercial 3D games | 8-action chunks; trained on time-offset action labels | RL | [arXiv 2404.10179](https://arxiv.org/abs/2404.10179) | paper §2: environments "do not stop and wait while the agent computes its next action" |
| [SIMA 2](sima-2.md) | 2025 | commercial 3D games | fine-tuned Gemini Flash-Lite emitting text action chunks, optional reasoning | RL (follows SIMA 1 setup; not restated) | [arXiv 2512.04797](https://arxiv.org/abs/2512.04797) | paper §3.2 "Periodically, the agent receives the latest frame"; same evaluation setup as SIMA 1, which "run in real-time, asynchronously to the agent" |
| [Lumine](lumine.md) | 2025 | Genshin Impact | 5 Hz perception, 30 Hz action chunks, 114 ms to first action | RL (missions) + PL (141-task benchmark, all agents) | [arXiv 2511.08892](https://arxiv.org/abs/2511.08892) | paper App.: "All the experiments are run in a real-time setting"; §5: "we pause the game during inference following the setup in Cradle" |
| [Game-TARS](game-tars.md) | 2025 | Minecraft, web games, ViZDoom | sparse thinking | PL | [arXiv 2510.23691](https://arxiv.org/abs/2510.23691) | paper §5 footnote: web games "used time-pause to ensure causal interaction"; MCU and ViZDoom are synchronous simulators |
| [NitroGen](nitrogen.md) | 2026 | 1,000+ games, gamepad | 16-action chunks from one frame; no language | PL (clock frozen) | [arXiv 2601.02427](https://arxiv.org/abs/2601.02427) | paper App. B.1 "freezes the game while the model predicts the next action"; code `nitrogen/game_env.py` `async_mode` pause/unpause per step |
| [Open-P2P](open-p2p.md) | 2026 | 3D PC games | 20 Hz on a consumer GPU | RL | [arXiv 2601.04575](https://arxiv.org/abs/2601.04575) | code: repo README (Recap "executes inputs in real time"; < 50 ms end-to-end requirement); paper §3 "the model must operate in real time (20 Hz)" |
| [CombatVLA](combatvla.md) | 2025 | Black Myth: Wukong | 1.85 s per step | PL | [arXiv 2503.09527](https://arxiv.org/abs/2503.09527) | paper §4: "the agent pauses the game during model inference and resumes the game when executing actions" |
| [pi0](pi0.md) | 2024 | robots | 50 Hz chunks, 73-86 ms inference, re-infer every 0.5 s | RL (real robot) | [arXiv 2410.24164](https://arxiv.org/abs/2410.24164) | paper App. D: inference every 0.5 s (50 Hz robots) or 0.8 s (20 Hz); real robots |
| [Gemini Robotics](gemini-robotics.md) | 2025 | robots | cloud backbone under 160 ms; local decoder gives 50 Hz effective | RL | [arXiv 2503.20020](https://arxiv.org/abs/2503.20020) | paper §3.1: backbone "under 160ms"; end-to-end "approximately 250ms"; "effective control frequency is 50Hz" |
| [Real-Time Chunking](real-time-chunking.md) | 2025 | robots, Kinetix | freeze committed prefix, inpaint the rest | RL (robot) + injected delay (sim) | [arXiv 2506.07339](https://arxiv.org/abs/2506.07339) | paper §5: Kinetix benchmark with simulated inference delay plus 6 real bimanual tasks |
| [SmolVLA async](smolvla-async.md) | 2025 | robots | action queue refilled asynchronously | RL | [arXiv 2506.01844](https://arxiv.org/abs/2506.01844) | paper §4.6: "the async mode decouples action execution and policy inference"; 9.7 s vs 13.75 s per task |
| [VLASH](vlash.md) | 2025 | robots | condition on predicted state at execution time | RL | [arXiv 2512.01031](https://arxiv.org/abs/2512.01031) | paper §V-A1 "simulated delays ranging from 0 to 4 steps"; §V-B real robots |
| [A2C2](a2c2.md) | 2025 | Kinetix, LIBERO | small per-tick correction head on stale chunks | injected delay (sim) | [arXiv 2509.23224](https://arxiv.org/abs/2509.23224) | paper §2: delay = "number of control steps between receiving an observation and obtaining the corresponding action chunk" |

### Landmark realtime systems

[OpenAI Five](openai-five.md), [AlphaStar](alphastar.md), [FTW](ftw.md) and [Phillip](phillip-slippi-ai.md) have their own files. The common pattern: these policies are fast enough that reaction delay is an imposed fairness constraint, the opposite of the LLM situation.

### How robotics handles inference latency
Real robots cannot pause the world, so this literature has the mature methods:
- **Action chunking** ([ACT](act.md), [pi0](pi0.md)): predict many actions per inference and execute open-loop.
- **Asynchronous queue** ([SmolVLA](smolvla-async.md)): refill the queue when it runs low; about 30% faster task completion with a small success drop.
- **[Real-Time Chunking](real-time-chunking.md)**: start the next inference early; freeze the actions that will execute during the delay and inpaint the rest. No degradation with 200 ms of added delay on real robots; works above 300 ms.
- **[Training-time RTC](training-time-rtc.md)** ([arXiv 2512.05964](https://arxiv.org/abs/2512.05964)): simulate the delay in training by giving the committed prefix as clean input.
- **[VLASH](vlash.md)**: condition on the predicted future state. **[A2C2](a2c2.md)**: a small head corrects the stale chunk every tick.
- **Time-offset labels** ([SIMA](sima.md)): train on the action that should execute one latency interval later.

For an autoregressive LLM agent, prefix commitment is simple: put the already-committed actions in the prompt and generate a continuation.

### Human reference numbers used as constraints
[OpenAI Five](openai-five.md) 217 ms average reaction; [FTW](ftw.md) humans 559 ms to respond to a new opponent (agents 258 ms); [FightingICE](../environments/fightingice.md) 15 frames (250 ms) of observation delay; Melee 12 frames as the lowest human-plausible delay (Firoiu et al.; see [Phillip / slippi-ai](phillip-slippi-ai.md)); conversational turn gap about 230 ms ([Moshi](moshi.md) paper). For general human simple visual reaction time, Woods et al. 2015 (Front. Hum. Neurosci. 9:131) report means of 231 ms, 213 ms after hardware correction (n = 1,469).

---

## 4. Post-training methods

### Summary

| Work | Year | What is trained | Signal | Evaluated on | Eval mode | Link | Basis |
|---|---|---|---|---|---|---|---|
| [Lumine](lumine.md) | 2025 | Qwen2-VL-7B; hybrid think-or-act | imitation (1,731 h play, 15 h annotated reasoning) | Genshin Impact | RL (missions) + PL (141-task benchmark) | [arXiv 2511.08892](https://arxiv.org/abs/2511.08892) | paper App.: "All the experiments are run in a real-time setting"; §5 "we pause the game during inference following the setup in Cradle" |
| [SIMA 2](sima-2.md) | 2025 | Gemini Flash-Lite | SFT then RL from verifiable rewards | 3D games | RL (follows SIMA 1 setup) | [arXiv 2512.04797](https://arxiv.org/abs/2512.04797) | paper §3.2 and SIMA 1 §3.4.1 (see RL table) |
| [Game-TARS](game-tars.md) | 2025 | VLM; sparse thinking | imitation, thoughts kept only where a reflex model fails | Minecraft, web games, ViZDoom | PL | [arXiv 2510.23691](https://arxiv.org/abs/2510.23691) | paper §5 footnote "used time-pause to ensure causal interaction" |
| [UI-TARS-2](ui-tars-2.md) | 2025 | VLM | multi-turn RL in a sandbox | 15 browser games | PL | [arXiv 2509.02544](https://arxiv.org/abs/2509.02544) | paper §2.2: clients "receive synchronous observations"; timing APIs "allow time acceleration and pause" |
| [CombatVLA](combatvla.md) | 2025 | 3B VLA; action first, explanation truncated at inference | SFT | Black Myth: Wukong | PL | [arXiv 2503.09527](https://arxiv.org/abs/2503.09527) | paper §4: "the agent pauses the game during model inference" |
| [Odysseus](odysseus.md) | 2026 | VLM | PPO with a turn-level critic over 100+ turns | Super Mario Land | PL | [arXiv 2605.00347](https://arxiv.org/abs/2605.00347) | paper §3.3: "the chosen discrete action is repeatedly applied for a fixed number of consecutive frames" (15 for jumps, otherwise 5) |
| [Orak fine-tuning](orak-fine-tuning.md) | 2025-26 | Llama-3.2-1B/3B | SFT on LLM trajectories | 12 games | PL | [arXiv 2506.03610](https://arxiv.org/abs/2506.03610) | paper §5.4 and App.: "During LLM inference, we pause the Super Mario game environment" |
| [Think in Games](think-in-games.md) | 2025 | Qwen 14B/32B | SFT + GRPO on replay labels | Honor of Kings macro prediction | offline, not gameplay | [arXiv 2508.21365](https://arxiv.org/abs/2508.21365) | paper §3.1: "label the main player's action as the ground truth for each game state" (offline prediction) |
| [HIMA agents](hima.md) | 2025 | Qwen-2 1.5B + LoRA | imitation of pro replays | StarCraft II | PL by default | [arXiv 2508.06042](https://arxiv.org/abs/2508.06042) | code: `main.py:23` `--realtime` default False |
| [Timely-RL](timely-rl.md) | 2026 | 8B LLM with timer tool | SFT + GRPO; zero reward if over the wall-clock budget | math, GPQA, Jericho text games | static with deadline | [arXiv 2601.16486](https://arxiv.org/abs/2601.16486) | paper §4.1: Jericho with assigned interaction delays; §5.2.2 over-budget answers count as incorrect |
| [AnytimeReasoner](anytimereasoner.md) | 2025 | reasoning LLM | RL with thinking truncated at sampled budgets | math | static | [arXiv 2505.13438](https://arxiv.org/abs/2505.13438) | paper §3: five math benchmarks at 32 token budgets |
| [Elastic Reasoning](elastic-reasoning.md) | 2025 | reasoning LLM | GRPO with budget-constrained rollouts | math, code | static | [arXiv 2505.05315](https://arxiv.org/abs/2505.05315) | paper §4: math and code benchmarks |
| [BudgetThinker](budgetthinker.md) | 2025 | reasoning LLM | periodic remaining-budget tokens; SFT + RL | (not extracted) | static | [arXiv 2508.17196](https://arxiv.org/abs/2508.17196) | paper §3.1 Evaluation Details |
| [L1](l1.md) | 2025 | reasoning LLM | RL reward minus length-target deviation | math | static | [arXiv 2503.04697](https://arxiv.org/abs/2503.04697) | paper §4 experimental setup (math) |
| [AdaptThink](adaptthink.md) | 2025 | reasoning LLM | RL to choose think or no-think | math | static | [AdaptThink](https://arxiv.org/abs/2505.13417) | papers: AdaptThink §4 |
| [Thinkless](thinkless.md) | 2025 | reasoning LLM | RL to choose think or no-think | math | static | [Thinkless](https://arxiv.org/abs/2505.13379) | Thinkless §4.1 (math) |
| [Interleaved Reasoning](interleaved-reasoning.md) | 2025 | LLM | RL rewarding correct intermediate answers | QA | static | [arXiv 2505.19640](https://arxiv.org/abs/2505.19640) | paper §1: five datasets; TTFT on fixed questions |
| [Dualformer](dualformer.md) | 2024 | transformer / LLM | train on randomly dropped reasoning traces; distil | mazes, QA | static | [Dualformer](https://arxiv.org/abs/2410.09918) | papers: Dualformer §4.1 maze/Sokoban as one-shot generation |
| [Distilling System 2 into 1](distilling-system-2-into-1.md) | 2024 | transformer / LLM | train on randomly dropped reasoning traces; distil | mazes, QA | static |  | Distilling §4 |
| [StreamingThinker](streamingthinker.md) | 2025 | Qwen3 | streaming CoT data, masks, parallel caches | QA | static | [arXiv 2510.17238](https://arxiv.org/abs/2510.17238) | paper §4.1 simulated input speed |
| [Async-SFT](async-sft.md) | 2026 | 3B LLMs | clock-simulated streaming input data | tool benchmarks | static, simulated streaming clock | [arXiv 2605.13360](https://arxiv.org/abs/2605.13360) | paper (2605.13360) §4: token clock used to generate SFT data; §5 simulated streaming speech |
| [Kyutai interactivity alignment](kyutai-interactivity-alignment.md) | 2026 | Moshi, PersonaPlex text stream | GRPO with rule-based timing rewards | Full-Duplex-Bench v1, v2 | RL (speech) | [arXiv 2606.11167](https://arxiv.org/abs/2606.11167) | paper §1: GRPO on conversation segments; evaluated on Full-Duplex-Bench v1 (pre-recorded) and v2 (real-time) |
| [STITCH](stitch.md) | 2025-26 | speech LLMs | interleaved or latent reasoning | spoken QA | RL (speech) | [STITCH](https://arxiv.org/abs/2507.15375) | papers: STITCH §4 |
| [Mini-Omni-Reasoner](mini-omni-reasoner.md) | 2025-26 | speech LLMs | interleaved or latent reasoning | spoken QA | RL (speech) | [arXiv 2508.15827](https://arxiv.org/abs/2508.15827) | Mini-Omni-Reasoner §4.4 (Spoken-MQA) |
| [FLAIR](flair.md) | 2025-26 | speech LLMs | interleaved or latent reasoning | spoken QA | RL (speech) | [arXiv 2603.17837](https://arxiv.org/abs/2603.17837) | FLAIR §4 (speech benchmarks, Full-Duplex-Bench) |
| [Training-time RTC](training-time-rtc.md) | 2025 | flow VLA | delay simulated in training | robots | RL | [arXiv 2512.05964](https://arxiv.org/abs/2512.05964) | paper §3: inference delay in controller timesteps; §4 Kinetix and real robots |
| [Real-Time EXPO-FT](real-time-expo-ft.md) | 2026 | VLA + small edit policy | online RL | real robots at 30 Hz | RL | [arXiv 2609.18207](https://arxiv.org/abs/2609.18207) | paper §3: delay of d timesteps; real-world dynamic tasks |
| [Think at 5 Hz, Act at 20 Hz](think-at-5hz-act-at-20hz.md) | 2026 | action expert on frozen VLM | randomised cache staleness | CARLA | PL (CARLA synchronous mode) | [arXiv 2607.15621](https://arxiv.org/abs/2607.15621) | paper §4.4: "in CARLA's synchronous mode the vehicle still receives fresh control at every tick" |

**No paper was found that post-trains a reasoning LLM or VLM against a live game clock and reports better realtime-live game scores.** The nearest pieces are in the files for [Lumine](lumine.md), [Game-TARS](game-tars.md), [CombatVLA](combatvla.md), [Timely-RL](timely-rl.md), [AnytimeReasoner](anytimereasoner.md), [Kyutai interactivity alignment](kyutai-interactivity-alignment.md), [Async-SFT](async-sft.md), [Odysseus](odysseus.md), [Orak fine-tuning](orak-fine-tuning.md) and [Think in Games](think-in-games.md).

### What the team could reuse
- Reward shaping: [Timely-RL](timely-rl.md)'s deadline reward; [AnytimeReasoner](anytimereasoner.md)'s random truncation; [Kyutai](kyutai-interactivity-alignment.md)'s rule-based timing rewards with a KL anchor.
- Data recipes: [sparse thinking](game-tars.md); [action-first with truncated explanation](combatvla.md); trace dropout ([Dualformer](dualformer.md)); clock-simulated streaming data ([Async-SFT](async-sft.md)); time-offset or delay-conditioned labels ([SIMA](sima.md), [training-time RTC](training-time-rtc.md)); [randomised staleness](think-at-5hz-act-at-20hz.md).
- Optimisers: GRPO variants; [Odysseus](odysseus.md) PPO for long episodes.
- Environment for rollouts: a token clock makes realtime-live rollouts reproducible and hardware independent.

---

## 5. Gaps: what nobody appears to have done

Based on the searches run; absence of evidence is not proof.

1. **Post-training against a live clock.** No RL or fine-tuning of a reasoning LLM or VLM with reward computed in a realtime-live game. The 2026 realtime benchmarks stop at evaluation or prompt-level adaptation ([TORSI](torsi.md)). [RealtimeGym](../environments/realtime-gym.md)'s authors list it as future work.
2. **Interaction models on games.** No full-duplex or interaction model ([TML-Interaction-Small](tml-interaction-small.md), [Moshi](moshi.md), [PersonaPlex](personaplex.md), [MiniCPM-o](minicpm-o-4-5.md)) has been evaluated as a player on a verifiable realtime game. [Realtime-Bench](../environments/realtime-bench.md) includes realtime API models and finds them weak, but not trained interaction models.
3. **An action stream in a duplex model.** All duplex output channels are text and audio. Multi-stream prediction has not been extended to keyboard, mouse or gamepad actions.
4. **Concurrent free-form reasoning and acting in one model.** [Moshi](moshi.md)'s inner monologue is its own transcript; [TML](tml-interaction-small.md) and [Dispider](dispider.md) push reasoning to a background model; [Lumine](lumine.md), [Game-TARS](game-tars.md) and [SIMA 2](sima-2.md) think then act. Concurrent think-and-respond exists for QA only ([Asynchronous Reasoning](asynchronous-reasoning.md)).
5. **Mid-thought steering in decision tasks.** [Interruptibility](are-lrms-interruptible.md) is diagnosed on static math and code; nobody has trained for it or tested it in an environment. [AgileThinker](agile-thinker.md) avoids the problem with a second model.
6. **Deciding to open more channels.** Nothing found on a model spawning extra perception or reasoning streams on demand.
7. **Multi-channel output under a clock.** Acting while speaking plus thinking is studied in speech models only, never combined with game control.
8. **Human baselines under the same clock.** Only [LOLPlay](../environments/lolplay.md) (two players), [GameWorld](../environments/gameworld.md) (paused mode) and a few others have human numbers; [Realtime-Bench](../environments/realtime-bench.md), [RealtimeBench](../environments/realtimebench.md), [ROAR](../environments/roar.md), [RealtimeGym](../environments/realtime-gym.md) and [OmniGameArena](../environments/omnigamearena.md) have none.
9. **Like-for-like comparison of the three baseline families** (fast action models, low-reasoning frontier LLMs, interaction models) on one realtime-live environment with one clock. [Realtime-Bench](../environments/realtime-bench.md) and [OmniGameArena](../environments/omnigamearena.md) come closest.
10. **Reaction-time-versus-score curves for LLM agents**, analogous to [FTW](ftw.md)'s added-delay study or [RTC](real-time-chunking.md)'s delay sweep. [RealtimeBench](../environments/realtimebench.md)'s 1x/1.5x/2x and [ROAR](../environments/roar.md)'s two tick rates are the only partial instances.
11. **Robotics delay methods ported to LLM agents.** Prefix commitment, training-time delay conditioning, future-state conditioning and per-tick correction heads have not been applied to text-action LLMs in games.
12. **Weight-level distillation of slow reasoning into fast reaction for a realtime game.** [TORSI](torsi.md) does it in prompts; [HIMA](hima.md) clones human replays.
13. **Scaffold comparison.** No head-to-head of two-thread, FSM code-as-policy, speculative and offline-guidance scaffolds on one benchmark and clock. Realtime scaffolds at human tick rates all rely on a hand-written executor; the LLM never issues the low-level action.
14. **Short, human-easy, pixel-plus-low-level-action tasks under a real clock.** Existing realtime benchmarks use text state with macro actions ([RealtimeGym](../environments/realtime-gym.md), [RealtimeBench](../environments/realtimebench.md)), 1 FPS GUI control ([Realtime-Bench](../environments/realtime-bench.md)), or long commercial games ([LOLPlay](../environments/lolplay.md), [VideoGameBench](../environments/videogamebench.md)).
