# Solutions for realtime LLM agents

Research date: 10 November 2026. Part 2 of the review; see [README.md](README.md) for scope and [environments.md](environments.md) for Part 1.

**Conventions.** Evaluation play mode is labelled realtime-live (RL), paused-live (PL), scripted (S), or "static" where there is no environment clock at all (QA, math, tool benchmarks). Every evaluation-mode label rests on an opened primary source, given in each table's Basis column ("code: <file>" or "paper: <section>" with a short quoted phrase); where a paper is silent, the label follows from what it does say and the entry says so. Numbers were extracted from arXiv HTML by a summarising fetch tool; re-check before quoting. Model names from 2026 papers are reproduced as printed.

Contents: [1. Scaffolds](#1-agent-scaffolds-on-existing-llms) | [2. Realtime architectures](#2-realtime-model-architectures) | [3. RL and decision models](#3-rl-and-decision-models) | [4. Post-training](#4-post-training-methods) | [5. Gaps](#5-gaps-what-nobody-appears-to-have-done)

---

## 1. Agent scaffolds on existing LLMs

### Summary

| Work | Year | Idea | Evaluated on | Eval mode | Headline result | Link | Basis |
|---|---|---|---|---|---|---|---|
| AgileThinker | 2025 | Planning thread streams reasoning; reactive thread reads its partial trace and acts before each deadline | RealtimeGym (Freeway, Snake, Overcooked) | RL, token clock | 0.90 to 0.58 as pressure rises, against 0.92 to 0.05 for planning alone | [arXiv 2511.04898](https://arxiv.org/abs/2511.04898) | paper §2: "the environment steps forward at a fixed rate, even when the agent has not finished thinking"; §6 wall-clock run |
| TORSI | 2026 | Slow teacher writes guidance offline; fast student plays live alone | RealtimeBench (6 arcade games) | RL, wall clock | Fast student 13.51 to 24.19 | [arXiv 2610.20665](https://arxiv.org/abs/2610.20665) | paper §3: "While a response is pending, the game keeps running with the previous control still active"; §4 the student acts "without teacher calls" |
| DPT-Agent | 2025 | FSM (rewritten by the LLM) acts every tick; asynchronous reflection and theory of mind | Overcooked at 4 Hz | RL (part S) | 46.6 against ReAct 15.5 | [arXiv 2502.11882](https://arxiv.org/abs/2502.11882) | code: `llm_agent_run_dpt_exp1.py` (`env.step` loop paced by `asyncio.sleep(0.25)`); paper: "each timestep corresponds to 0.25 seconds in the real world" |
| HLA | 2023 | Slow LLM + fast LLM + scripted executor | Overcooked with humans, about 3 Hz | RL (paper; no code) | Macro latency 1.07 s against 4.16 s slow-only | [arXiv 2312.15224](https://arxiv.org/abs/2312.15224) | paper §1: Overcooked where "players collaborate at a rate of approximately 3Hz"; executor acts while the LLMs run; no pause described |
| RRARA | 2025-26 | Rule reflex acts at once; asynchronous LLM reflector corrects | HAZARD with injected latency | RL (INJECT) | Value rate 0.44 against best plain LLM 0.25 | [arXiv 2506.07223](https://arxiv.org/abs/2506.07223) | paper §3: "After each decision, we advance the simulator by frames" (frames = latency x 30 FPS) |
| Latent Bridge | 2026 | Frozen fast VLM at 15 Hz + frozen slow VLM at 1 Hz, linked by a trained latent channel | 7 Atari games | PL (synchronous tick loop; slow model every 15 ticks) | Wins on 2 of 7 games against a text bridge | [arXiv 2606.24470](https://arxiv.org/abs/2606.24470) | code: `src/eval/benchmark.py:110-186` (`fast.predict_action` -> `env.step` -> inline `slow.emit`), `src/env/atari_wrapper.py` 4 frames per tick |
| SwarmBrain | 2024 | LLM strategy + reflex state machine | StarCraft II vs built-in AI | RL | 76% against Hard | [arXiv 2401.17749](https://arxiv.org/abs/2401.17749) | code: `swarmbrain_launch.py:2666-2671` `run_game(..., realtime=True)`; LLM via `run_in_executor` (`swarmbrain.py:79`) |
| HIMA | 2025 | Small fine-tuned agents propose long build sequences; planner called about 11 times a game | StarCraft II | PL by default (`--realtime` off); RL with the flag | 100% to 16% across AI levels 4-10 | [arXiv 2508.06042](https://arxiv.org/abs/2508.06042) | code: `main.py:23` `--realtime` default False, `main.py:70` `run_game(realtime=args.realtime)`; paper does not say which mode produced the win rates |
| Parallelized Planning-Acting | 2025 | Planning and acting threads; single-slot buffer where a new plan interrupts the running action | Minecraft, unpaused server | RL (skills are scripted) | 3 agents halve diamond-armor time | [arXiv 2503.03505](https://arxiv.org/abs/2503.03505) | paper §3.2: "The game server operates continuously without pausing during interactions with LLMs" |
| FPX (Win Fast or Lose Slow) | 2025 | Mixed-precision quantisation as a latency knob | Street Fighter, HFTBench | RL | 3B at 195 ms beats 7B; 14B best for trading | [arXiv 2505.19481](https://arxiv.org/abs/2505.19481) | code: `StreetFighter/GameEngine/Engine/game.py` (continuous `env.step`, action 0 when none pending); `HFTBench/Environment/TradingEnv.py` (measured delay worsens fill price) |
| Speculative Actions | 2025 | Fast model guesses the slow actor's next step; pre-execute and commit on match | chess, tau-bench, HotpotQA, OS tuning | PL / static | 19.5% time saved in chess | [arXiv 2510.04371](https://arxiv.org/abs/2510.04371) | paper §1: "Turn-based gameplay (e.g., chess)"; implemented on TextArena |
| Async I/O + Speculative Tool Calling | 2026 | Event-driven loop decoupled from streaming speech and tool returns | tool benchmarks with simulated streaming input | static, simulated streaming clock | About 2x lower latency for fine-tuned 3B models | [arXiv 2605.13360](https://arxiv.org/abs/2605.13360) | paper §5: "We evaluate our method by simulating streaming updates from speech-to-text" |
| Asynchronous Reasoning | 2025 | Training-free concurrent think/read/write in one model via position manipulation | math, commonsense, safety QA | static | First non-thinking token within 5 s | [arXiv 2512.10931](https://arxiv.org/abs/2512.10931) | paper §4: MATH-500, MMLU-Pro, GPQA, AIME-2025, ZebraLogic; delay measured as TTS silence time |
| Are LRMs Interruptible? | 2025 | Diagnostic: interrupts and context updates mid-reasoning | math and code QA | static | Up to 60% accuracy drop | [arXiv 2510.11713](https://arxiv.org/abs/2510.11713) | paper §3: "we primarily use relative cut points" in the reasoning trace; GSM-8K, Math-500, AIME, LiveCodeBench |
| Never Stop Thinking | 2026 | Interrupt-and-resume orchestrator so a text LLM thinks while listening and speaking | ReactiveBench (voice scenarios) | static (scripted interrupts, simulated speech rate) | Latency -19% | [arXiv 2609.17416](https://arxiv.org/abs/2609.17416) | paper §3: "interrupts are realized at the transcript level by truncating the agent's prior turn"; App. A simulated speech at 3.5 words/s |
| Second Thought | 2026 | Fork reasoning branches during the act/observe wait | agent benchmarks | PL (agentic benchmarks) | Fewer turns in 9 of 9 pairs | [arXiv 2608.13667](https://arxiv.org/abs/2608.13667) | paper §1: SWE-Bench Pro, Terminal-Bench 2.1, tau-bench; §5 paired wall-clock replay |
| AsyncLM | 2024 | Keep generating while tools run; interrupt tokens on return | BFCL | static | 1.6-5.4x lower latency | [arXiv 2412.07017](https://arxiv.org/abs/2412.07017) | paper §6: BFCL tasks; task completion latency |
| LiveMind | 2024 | Infer on a partial prompt while input streams | MMLU | static | Latency -84% | [arXiv 2406.14319](https://arxiv.org/abs/2406.14319) | paper §4.1 "Streaming input simulation" |
| SwiftSage | 2023 | Small cloned fast model + GPT-4 planner, heuristic switch | ScienceWorld | PL | (not extracted) | [arXiv 2305.17390](https://arxiv.org/abs/2305.17390) | paper §2: ScienceWorld text environment, one action per step |
| Talker-Reasoner | 2024 | Fast talker + slow reasoner with shared memory | sleep-coaching example | none | no quantitative evaluation | [arXiv 2410.08328](https://arxiv.org/abs/2410.08328) | paper §4: case study with "Qualitative Results" only |
| Cradle | 2024 | Six-module GPT-4o pipeline writing code skills | RDR2, Stardew and others | PL in every environment | about 62 s per decision | [arXiv 2403.03186](https://arxiv.org/abs/2403.03186) | code: `cradle/provider/execute/skill_execute.py` (unpause -> skill -> pause); paper §4 "we must pause those game environments" |
| Voyager, PORTAL, CodeClash | 2023-25 | LLM writes code, behaviour trees or bots | Minecraft, 3D games, code arenas | S (Voyager also pauses the server during LLM calls) | out of scope | [Voyager](https://arxiv.org/abs/2305.16291) | code: Voyager `voyager/env/bridge.py:113-124`; PORTAL paper §2 "Rather than relying on LLM inference during gameplay"; CodeClash paper §2 "LMs do not play the games directly" |

### Notes on the most relevant

**AgileThinker** (Wen, Ye, Zhang, Yang, Zhu; ICLR 2026; code in [RealtimeGym](https://github.com/SALT-NLP/RealtimeGym), MIT). The planning thread (DeepSeek-R1) is never interrupted and runs across environment steps. The reactive thread (DeepSeek-V3) starts in the last few thousand tokens of each step with the newest observation and the planner's partial trace. It needs visible reasoning traces, so closed models can only be approximated. At 8k tokens per step on hard load: Freeway 0.06 reactive / 0.10 planning / 0.51 AgileThinker. A wall-clock check used steps of about six minutes. Budget-forcing the reasoning model scored 0.01. No training; the authors list training urgency-aware agents as future work. Reuse: the baseline scaffold and the gym.

**TORSI** (Pan et al., Oct 2026; no code yet). A slow teacher (GPT-6.1-sol) works offline on saved states and student trajectories in paused or slowed games and writes textual skills and rules; guidance is adopted only if it improves validation scores. The fast student (Jev, 0.52 s latency) then plays live with no teacher calls. Test average 13.51 to 24.19, against prompt optimisers ACE 13.22, AHE 16.59, GEPA 14.52. Guidance transfers to other fast models. No weight updates. Reuse: the natural no-training baseline that post-training should beat.

**DPT-Agent** (Zhang et al., ACL 2025; [code](https://github.com/sjtu-marl/DPT-Agent), MIT). System 1 is an FSM over macro actions with A* for atomic moves; the LLM periodically rewrites the FSM logic and the FSM keeps acting when no new code arrives. System 2 runs asynchronously. Reasoning models score negative under plain ReAct in realtime (o3-mini-high: -43.0) and 55.2 with DPT. Human study with 68 participants. Reuse: an FSM safety net and an open 4 Hz harness.

**HLA** (Liu et al., AAMAS 2024). Slow Mind (GPT-3.5) for intent and chat, Fast Mind (quantised Llama-2-13B) for macro actions, scripted executor for atomic actions. Reports latency per level: 0.08 s atomic, 1.07 s macro.

**RRARA** (Zheng et al.; no code). A rule policy acts immediately; a fine-tuned GPT-3.5 reflector vetoes or corrects asynchronously; a pre-planner caches subgoal sequences. Its Time Conversion Mechanism (advance the simulator by ceil(latency x FPS) frames) is reusable on its own.

**Latent Bridge** (Li, Shi; [code](https://github.com/19PINE-AI/latent-bridge-games)). MiniCPM-o 4.5 acts each 67 ms tick; Qwen3-VL-8B-Thinking deliberates at about 1 Hz and its latest output is reused for about 15 ticks. Only a 33M-parameter MLP mapping slow-model residuals to 8 soft tokens is trained. Headline scores use an uncached path of about 157 ms per tick, and in the released benchmark the emulator waits for the fast model: `src/eval/benchmark.py` runs a synchronous tick loop (fast prediction, then `env.step` of 4 frames) and calls the slow model's `emit()` inline every 15 ticks, so the 15 Hz and 1 Hz rates are tick ratios, not wall-clock (paused-live). The paper's statement that "the fast loop never blocks" on the slow model holds only in tick terms. Scores are far below RL and human levels (MsPacman 628). Honest negative results on 5 of 7 games.

**Interruptibility diagnostic** (Wu et al., Berkeley, ICML 2026; [code](https://github.com/dynamic-lm/interrupt-lrm), Apache-2.0). Hard interrupts, "answer faster" requests, and context updates injected at a fraction of the reasoning trace. Failure modes: reasoning leaks into the answer after a hard interrupt, "panic" under speed-up requests, and "self-doubt" after updates (about 80% of update errors). Token-fraction timing on static tasks; no training tried. This is the only systematic study of a thought process steered mid-thought.

**Supporting evidence that more reasoning hurts under a clock.** Realtime-Bench (Claude Opus 5 at high effort: 70% paused, 14% wall clock), LOLPlay (higher effort never helps), ROAR (ReAct scaffolds help turn-based play only), Orak's unpaused StarCraft II (scores to 0), OSWorld-Human (planning and reflection calls dominate latency), AgentTime ([arXiv 2610.09944](https://arxiv.org/abs/2610.09944): agents land within 5% of a requested working duration in 63%, 39% and 4% of runs for three frontier agents).

**Robotics dual systems (brief).** Hi Robot ([arXiv 2502.19417](https://arxiv.org/abs/2502.19417)): the high-level VLM re-runs every second or immediately on a user interjection. Figure Helix: 7-9 Hz VLM, 200 Hz policy, linked by a latent (Figure's announcement page, saved; real-robot demonstrations, no quantitative evaluation). FiS-VLA ([arXiv 2506.01953](https://arxiv.org/abs/2506.01953)): 117.7 Hz. "Think at 5 Hz, Act at 20 Hz" ([arXiv 2607.15621](https://arxiv.org/abs/2607.15621)): a fast head reads a stale VLM cache and is trained with randomised staleness; CARLA route completion 37% to 94%.

### What the team could reuse
- Baselines: reactive-only, planning-only, AgileThinker, FSM safety net (DPT), offline guidance (TORSI).
- Harness pieces: token clock, latency injection, default action on timeout, per-level latency reporting, single-slot interrupt buffer.
- The interruptibility protocol and datasets as a static pre-test for mid-thought steering.

---

## 2. Realtime model architectures

Models trained to take input and produce output concurrently. Every evaluation below is conversational or perception-only. None of these models has been evaluated as a player on a verifiable realtime game or control task, and none has an action output channel.

### Summary

| Model | Year | Channels (in / out) | Tick | How thinking coexists with output | Open / fine-tunable | Link | Eval mode | Basis |
|---|---|---|---|---|---|---|---|---|
| TML-Interaction-Small | 2026 | text, audio, video / text, audio | 200 ms micro-turns | Separate asynchronous background model reasons and calls tools | No weights or public API as of the May 2026 post | [blog](https://thinkingmachines.ai/blog/interaction-models/) | RL (speech); no game or control evaluation | docs: blog (saved) "continuous input and output streams split into micro-turns" of 200 ms; benchmarks self-reported |
| Moshi | 2024 | user audio / own audio + text | 80 ms (12.5 Hz), 17 streams | "Inner monologue" text stream, which is the transcript of its own speech | Open weights and code | [arXiv 2410.00037](https://arxiv.org/abs/2410.00037) | RL (speech) operation; reported evaluation static | paper: abstract "theoretical latency of 160ms, 200ms in practice"; §5.6 continuations of 10 s Fisher prompts |
| PersonaPlex | 2026 | as Moshi + role and voice prompts | 80 ms | as Moshi | Weights released under the NVIDIA Open Model License (gated; HF API metadata and repo README) | [arXiv 2602.06053](https://arxiv.org/abs/2602.06053) | RL (speech) | paper §2: "user input audio is streamed in and the model's corresponding generated audio is captured and evaluated" |
| MiniCPM-o 4.5 | 2026 | video, audio, text / text, speech | 1 s windows | Listen/speak control token per window; no reasoning stream | Open, Apache-2.0 per model card | [arXiv 2604.27393](https://arxiv.org/abs/2604.27393) | offline replay (LiveSports-3K-CC); static elsewhere | paper §6.1 LiveSports-3K-CC "an audio-free full-duplex benchmark"; model card "decides at a frequency of 1Hz to speak or not" |
| Duplex models / MiniCPM-Duplex | 2024 | text / text | time slices | Reads a slice, writes a slice or stays idle | Fine-tuned from MiniCPM | [arXiv 2406.15718](https://arxiv.org/abs/2406.15718) | static (benchmarks) + RL (speech) user study | paper §4.4 "the user's speech is processed every 2 seconds"; §4.5 user study |
| SyncLLM | 2024 | two speech streams | 160-240 ms chunks | Predicts the user's next chunk to hide latency | Llama-3-8B fine-tune | [arXiv 2409.15594](https://arxiv.org/abs/2409.15594) | static (continuation) + RL (speech, simulated one-chunk latency) | paper §5.4 "We simulate LLM-user interaction using LLM-LLM interaction with one-chunk latency" |
| OmniFlatten | 2024 | speech + text | flattened streams | Staged post-training of a small GPT, no architecture change | research | [arXiv 2410.17799](https://arxiv.org/abs/2410.17799) | offline replay | paper §4: "a predefined user speech input while setting a 1.5-second threshold" |
| dGSLM | 2022 | two audio channels | units | none (textless) | research | [arXiv 2203.16502](https://arxiv.org/abs/2203.16502) | static | paper §4.3.2: 90-second continuations of 30-second prompts |
| gpt-realtime-2 (Realtime API) | 2026 | text, audio, images / text, audio | harness turn detection | Reasoning-effort levels; higher effort raises latency | API only, no fine-tuning | [docs](https://developers.openai.com/api/docs/models/gpt-realtime-2) | RL (speech) service; no game evaluation by the vendor | docs: model page, VAD guide (`server_vad` / `semantic_vad`), prompting guide (reasoning effort); fine-tuning "Not supported" |
| Gemini Live (2.5, 3.1 Flash Live) | 2025-26 | audio, video frames, text / audio, text | session streaming | `thinkingLevel`, default minimal | API only | [docs](https://ai.google.dev/gemini-api/docs/live-guide) | RL (speech) service | docs: Live API overview and capabilities guide (saved); video at most 1 frame per second |
| Qwen3-Omni / Qwen3.5-Omni | 2025-26 | audio, video, text / text, speech | streaming output | Thinker-Talker; thinking precedes output | Qwen3-Omni Apache-2.0 | [arXiv 2509.17765](https://arxiv.org/abs/2509.17765) | static | paper (Qwen3-Omni) §1: "Across 36 audio and audio-visual benchmarks"; "theoretical end-to-end first-packet latency of 234 ms" |
| Realtime-Venus | 2026 | audio, video / speech | full duplex | Front-end model delegates to a background harness | not checked | [arXiv 2609.13814](https://arxiv.org/abs/2609.13814) | RL (speech, Full-Duplex-Bench) + static | paper §6 evaluation tables |
| VideoLLM-online | 2024 | video frames / text | per frame | Decides per frame to stay silent or speak | Open | [arXiv 2406.11816](https://arxiv.org/abs/2406.11816) | offline replay | paper §4: Ego4D "timestamp-narration" streaming set |
| Dispider | 2025 | video / text | per clip | Separate perception, decision and asynchronous reaction modules | research | [arXiv 2501.03218](https://arxiv.org/abs/2501.03218) | offline replay | paper §1: evaluated on StreamingBench and offline long-video benchmarks |
| StreamingThinker | 2025 | streaming text / text | per sentence | Reasons while the prompt streams; parallel KV caches | Open, Qwen3 fine-tune | [arXiv 2510.17238](https://arxiv.org/abs/2510.17238) | static (simulated streaming input) | paper §4.1 latency definition with simulated input speed |

### Notes

**Thinking Machines Lab interaction models** (blog, 11 May 2026). TML-Interaction-Small is a 276B-parameter MoE with 12B active, encoder-free. Input and output are interleaved in 200 ms micro-turns in one sequence, so silence, overlap and elapsed time are in context. Long reasoning is pushed to a background model that shares the conversation and whose results are woven back in. Self-reported: Full-Duplex-Bench v1 turn-taking latency 0.40 s (GPT-realtime-2.0 minimal 1.18 s; Gemini-3.1-flash-live 0.57 s); v1.5 average 77.8 against 46.8. Timing benchmarks, against GPT-realtime-2.0 minimal: TimeSpeak 64.7 / 4.3, CueSpeak 81.7 / 2.9, RepCount-A 35.4 / 1.3, Charades start/stop 32.4 / 0 mIoU. No game or action experiment. Reuse: the micro-turn serialisation can be imitated in text post-training without a new architecture; the timing tasks are tiny, verifiable, human-easy realtime tasks.

**Moshi** (Kyutai). A 7B text LLM over Mimi codec tokens. Each 80 ms step predicts 8 codebooks of user audio, 8 of its own audio and one text stream. 160 ms theoretical latency, about 200 ms in practice. The only mature open full-duplex backbone with a parallel text stream. Follow-ups: Hibiki (simultaneous translation), Unmute (a cascade that makes any text LLM listen and speak), PersonaPlex (NVIDIA; role and voice conditioning).

**MiniCPM-o 4.5** (OpenBMB). 9B, Qwen3-8B backbone. Time-division multiplexing on a shared time axis; the paper ablated 1.0 s, 0.2 s and 0.1 s windows and chose 1.0 s because shorter windows hurt quality. First-token latency about 0.58 s on an RTX 4090. The best open candidate with vision, but worst-case reaction above one second is slower than a human. It is the fast model in Latent Bridge.

**Realtime APIs.** In the OpenAI Realtime API and Gemini Live, interactivity is largely in the harness (voice activity detection, turn detection), not learned full duplex. In Realtime-Bench, GPT-Realtime-2 scores 12-18% and Gemini 3.1 Flash Live 6-18% under wall clock: quick but not good enough. Proactive audio is configurable on Gemini 2.5 Flash Live, permanently on for the 3.8 Live models and not supported on 3.1 Flash Live Preview (Live API capabilities guide, saved).

**Streaming video LLMs** (VideoLLM-online, Flash-VStream, Dispider, StreamBridge, LiveCC, StreamingVLM, OmniMMI/M4, Proact-VL). The only "action" is when to speak. Evaluations replay recorded video and mostly score offline. Proact-VL ([arXiv 2603.03447](https://arxiv.org/abs/2603.03447)) is the closest to games: it comments on gameplay but does not play.

**Streaming and duplex text models.** Duplex models (time slices of text), StreamingThinker (think while reading, with separate position IDs and parallel KV caches), Asynchronous Reasoning (training-free concurrent thinking and writing). These are the nearest text-only mechanisms for new input landing mid-thought. All are evaluated on static QA or chat.

**Thinking while speaking** (STITCH [arXiv 2507.15375](https://arxiv.org/abs/2507.15375), SHANKS [arXiv 2510.06917](https://arxiv.org/abs/2510.06917), Mini-Omni-Reasoner [arXiv 2508.15827](https://arxiv.org/abs/2508.15827), FLAIR [arXiv 2603.17837](https://arxiv.org/abs/2603.17837)). Reasoning chunks are interleaved with spoken chunks, or generated while the user is still talking, so reasoning costs no extra latency. STITCH reports +15% on spoken math at the latency of a no-reasoning baseline. Speech only.

### What the team could reuse
- Baselines for the "interaction/realtime models" column: gpt-realtime-2 and Gemini Live through their APIs, Moshi/PersonaPlex and MiniCPM-o 4.5 locally. Game pixels must be pushed as frames, and actions must be parsed from text or speech.
- Serialisation ideas for post-training a text model: micro-turns, time slices, a listen/act control token per window, a parallel inner-monologue stream.

---

## 3. RL and decision models

### Summary

| System | Year | Domain | Action rate and reaction handling | Eval mode | Link | Basis |
|---|---|---|---|---|---|---|
| DQN / Atari line | 2015- | Atari | frameskip 4 (15 Hz); inference time free | PL | [ALE docs](https://ale.farama.org/environments/) | paper: Nature 2015 Methods "the agent sees and selects actions on every kth frame"; human tester "not allowed to pause" |
| OpenAI Five | 2019 | Dota 2 | acts every 4th frame (7.5 Hz); 217 ms average reaction | RL vs humans | [arXiv 1912.06680](https://arxiv.org/abs/1912.06680) | paper §2: "OpenAI Five only acts on every 4th frame"; "react to a game event in 217ms on average" |
| AlphaStar | 2019 | StarCraft II | camera interface and limits on action frequency agreed with a professional player | RL on Battle.net | [blog](https://deepmind.google/blog/alphastar-grandmaster-level-in-starcraft-ii-using-multi-agent-reinforcement-learning/) | docs: DeepMind blog (saved) "viewing the world through a camera, and stronger limits on the frequency of its actions" |
| FTW | 2018-19 | Quake III CTF | reacts in 258 ms against 559 ms for humans; no win-rate loss up to 375 ms added delay | RL vs humans | [arXiv 1807.01281](https://arxiv.org/abs/1807.01281) | paper: "respond to newly appeared opponents in 258ms, compared with 559ms for humans"; "up to 375ms did not effect the win probability" |
| GT Sophy | 2022 | Gran Turismo | 10 Hz control, game runs only in real time | RL on PS4 | [paper page](https://ai.sony/publications/Outracing-champion-Gran-Turismo-drivers-with-deep-reinforcement-learning) | paper: "GT Sophy interacted with the game at 10 Hz"; "Although GT ran only in real time" |
| Phillip / slippi-ai | 2017- | Melee | 12-15 frame imposed delay + predictive model | RL in netplay | [arXiv 1810.07286](https://arxiv.org/abs/1810.07286) | paper (1810.07286) §1: "we add fixed delay between the time an agent chooses an action" and when it is applied; "12 frames to be the lowest" human-plausible delay |
| VPT, STEVE-1, GROOT, ROCKET, JARVIS-VLA | 2022-25 | Minecraft | 20 Hz native interface; synchronous simulator | PL | [arXiv 2206.11795](https://arxiv.org/abs/2206.11795) | paper (VPT) App. C: client and server "run in the same thread ... slower or faster than real time"; code: MineRL `_multiagent.py` synchronous token |
| DreamerV3 / Dreamer 4 | 2023-25 | Minecraft and others | simulator-stepped | PL (agent evaluation) | [arXiv 2509.24527](https://arxiv.org/abs/2509.24527) | paper (DreamerV3 v1) App.: MineRL, "36000 steps, corresponding to 30 minutes at the control frequency of 20Hz"; Dreamer 4 §4.1 follows the VPT protocol |
| SIMA | 2024 | commercial 3D games | 8-action chunks; trained on time-offset action labels | RL | [arXiv 2404.10179](https://arxiv.org/abs/2404.10179) | paper §2: environments "do not stop and wait while the agent computes its next action" |
| SIMA 2 | 2025 | commercial 3D games | fine-tuned Gemini Flash-Lite emitting text action chunks, optional reasoning | RL (follows SIMA 1 setup; not restated) | [arXiv 2512.04797](https://arxiv.org/abs/2512.04797) | paper §3.2 "Periodically, the agent receives the latest frame"; same evaluation setup as SIMA 1, which "run in real-time, asynchronously to the agent" |
| Lumine | 2025 | Genshin Impact | 5 Hz perception, 30 Hz action chunks, 114 ms to first action | RL (missions) + PL (141-task benchmark, all agents) | [arXiv 2511.08892](https://arxiv.org/abs/2511.08892) | paper App.: "All the experiments are run in a real-time setting"; §5: "we pause the game during inference following the setup in Cradle" |
| Game-TARS | 2025 | Minecraft, web games, ViZDoom | sparse thinking | PL | [arXiv 2510.23691](https://arxiv.org/abs/2510.23691) | paper §5 footnote: web games "used time-pause to ensure causal interaction"; MCU and ViZDoom are synchronous simulators |
| NitroGen | 2026 | 1,000+ games, gamepad | 16-action chunks from one frame; no language | PL (clock frozen) | [arXiv 2601.02427](https://arxiv.org/abs/2601.02427) | paper App. B.1 "freezes the game while the model predicts the next action"; code `nitrogen/game_env.py` `async_mode` pause/unpause per step |
| Open-P2P | 2026 | 3D PC games | 20 Hz on a consumer GPU | RL | [arXiv 2601.04575](https://arxiv.org/abs/2601.04575) | code: repo README (Recap "executes inputs in real time"; < 50 ms end-to-end requirement); paper §3 "the model must operate in real time (20 Hz)" |
| CombatVLA | 2025 | Black Myth: Wukong | 1.85 s per step | PL | [arXiv 2503.09527](https://arxiv.org/abs/2503.09527) | paper §4: "the agent pauses the game during model inference and resumes the game when executing actions" |
| pi0 | 2024 | robots | 50 Hz chunks, 73-86 ms inference, re-infer every 0.5 s | RL (real robot) | [arXiv 2410.24164](https://arxiv.org/abs/2410.24164) | paper App. D: inference every 0.5 s (50 Hz robots) or 0.8 s (20 Hz); real robots |
| Gemini Robotics | 2025 | robots | cloud backbone under 160 ms; local decoder gives 50 Hz effective | RL | [arXiv 2503.20020](https://arxiv.org/abs/2503.20020) | paper §3.1: backbone "under 160ms"; end-to-end "approximately 250ms"; "effective control frequency is 50Hz" |
| Real-Time Chunking | 2025 | robots, Kinetix | freeze committed prefix, inpaint the rest | RL (robot) + injected delay (sim) | [arXiv 2506.07339](https://arxiv.org/abs/2506.07339) | paper §5: Kinetix benchmark with simulated inference delay plus 6 real bimanual tasks |
| SmolVLA async | 2025 | robots | action queue refilled asynchronously | RL | [arXiv 2506.01844](https://arxiv.org/abs/2506.01844) | paper §4.6: "the async mode decouples action execution and policy inference"; 9.7 s vs 13.75 s per task |
| VLASH | 2025 | robots | condition on predicted state at execution time | RL | [arXiv 2512.01031](https://arxiv.org/abs/2512.01031) | paper §V-A1 "simulated delays ranging from 0 to 4 steps"; §V-B real robots |
| A2C2 | 2025 | Kinetix, LIBERO | small per-tick correction head on stale chunks | injected delay (sim) | [arXiv 2509.23224](https://arxiv.org/abs/2509.23224) | paper §2: delay = "number of control steps between receiving an observation and obtaining the corresponding action chunk" |

### Landmark realtime systems
- **OpenAI Five.** Dota 2 at 30 fps; the agent acts on every fourth frame and reacts in 217 ms on average. The nominal reaction time was raised from 80 ms to 200 ms for the 2018 benchmark as a fairness constraint. State vector from the bot API, not pixels.
- **AlphaStar.** The DeepMind announcement says AlphaStar "now has the same kind of constraints that humans play under – including viewing the world through a camera, and stronger limits on the frequency of its actions", and that it "played on the official game server, Battle.net". The Nature paper's exact delay and action-rate numbers could not be read (paywalled), so none are given here.
- **FTW.** A post-hoc delay study: added response time up to 375 ms did not change win probability; at 448 ms the win rate fell to 85%. This is the template for a reaction-time-versus-score curve.
- **Phillip.** Imposed frame delay plus a learned predictive model so the policy acts on the state at execution time.

The common pattern: these policies are fast enough that reaction delay is an imposed fairness constraint, the opposite of the LLM situation.

### Game foundation and action models
- **SIMA** states its environments "do not stop and wait while the agent computes" and compensates by predicting actions "offset in time" during behavioural cloning. No Man's Sky: humans 60%, SIMA 34%. Not released.
- **SIMA 2** fine-tunes Gemini Flash-Lite, chosen over Pro "due to the latency constraints that come with embodied action". Untrained Gemini scores 3.2% (Flash-Lite) and 7.0% (Pro) in the same harness. Action fine-tuning costs general ability (AIME -25.5% after SFT). The paper (including appendices) gives no rate and does not mention pausing; the realtime-live label follows from its statement that "Periodically, the agent receives the latest frame" and from its reuse of the SIMA 1 setup, whose environments "run in real-time, asynchronously to the agent".
- **Lumine** is the most complete public description of an LLM that perceives, thinks sparsely and acts in real time: one frame per 200 ms, six 33 ms action chunks per step streamed as decoded, KV-cache reuse, quantisation, 25x latency reduction. The paper states its experiments run in a real-time setting. Mondstadt Act I in 56 minutes against 53 for expert humans. Its frontier-model baselines were run paused "following Cradle" because API calls can take 30 s. The paper does not state a weights or code release.
- **NitroGen** (about 500M parameters, vision to gamepad, 40,000 hours of video) and **Open-P2P** (150M-1.2B, 8,300 hours of labelled keyboard/mouse data, open code and checkpoints) are the ready "fast but will not think" baselines. OmniGameArena and Realtime-Bench already include decision models alongside frontier VLMs.
- **D2E** ([arXiv 2510.05684](https://arxiv.org/abs/2510.05684)) provides an open recorder with synchronised screen and input timestamps, useful for collecting human baselines.

### How robotics handles inference latency
Real robots cannot pause the world, so this literature has the mature methods:
- **Action chunking** (ACT, pi0): predict many actions per inference and execute open-loop.
- **Asynchronous queue** (SmolVLA): refill the queue when it runs low; about 30% faster task completion with a small success drop.
- **Real-Time Chunking**: start the next inference early; freeze the actions that will execute during the delay and inpaint the rest. No degradation with 200 ms of added delay on real robots; works above 300 ms.
- **Training-time RTC** ([arXiv 2512.05964](https://arxiv.org/abs/2512.05964)): simulate the delay in training by giving the committed prefix as clean input.
- **VLASH**: condition on the predicted future state. **A2C2**: a small head corrects the stale chunk every tick.
- **Time-offset labels** (SIMA): train on the action that should execute one latency interval later.

For an autoregressive LLM agent, prefix commitment is simple: put the already-committed actions in the prompt and generate a continuation.

### Human reference numbers used as constraints
OpenAI Five 217 ms average reaction; FTW humans 559 ms to respond to a new opponent (agents 258 ms); FightingICE 15 frames (250 ms) of observation delay; Melee 12 frames as the lowest human-plausible delay (Firoiu et al.); conversational turn gap about 230 ms (Moshi paper). For general human simple visual reaction time, Woods et al. 2015 (Front. Hum. Neurosci. 9:131) report means of 231 ms, 213 ms after hardware correction (n = 1,469).

---

## 4. Post-training methods

### Summary

| Work | Year | What is trained | Signal | Evaluated on | Eval mode | Link | Basis |
|---|---|---|---|---|---|---|---|
| Lumine | 2025 | Qwen2-VL-7B; hybrid think-or-act | imitation (1,731 h play, 15 h annotated reasoning) | Genshin Impact | RL (missions) + PL (141-task benchmark) | [arXiv 2511.08892](https://arxiv.org/abs/2511.08892) | paper App.: "All the experiments are run in a real-time setting"; §5 "we pause the game during inference following the setup in Cradle" |
| SIMA 2 | 2025 | Gemini Flash-Lite | SFT then RL from verifiable rewards | 3D games | RL (follows SIMA 1 setup) | [arXiv 2512.04797](https://arxiv.org/abs/2512.04797) | paper §3.2 and SIMA 1 §3.4.1 (see RL table) |
| Game-TARS | 2025 | VLM; sparse thinking | imitation, thoughts kept only where a reflex model fails | Minecraft, web games, ViZDoom | PL | [arXiv 2510.23691](https://arxiv.org/abs/2510.23691) | paper §5 footnote "used time-pause to ensure causal interaction" |
| UI-TARS-2 | 2025 | VLM | multi-turn RL in a sandbox | 15 browser games | PL | [arXiv 2509.02544](https://arxiv.org/abs/2509.02544) | paper §2.2: clients "receive synchronous observations"; timing APIs "allow time acceleration and pause" |
| CombatVLA | 2025 | 3B VLA; action first, explanation truncated at inference | SFT | Black Myth: Wukong | PL | [arXiv 2503.09527](https://arxiv.org/abs/2503.09527) | paper §4: "the agent pauses the game during model inference" |
| Odysseus | 2026 | VLM | PPO with a turn-level critic over 100+ turns | Super Mario Land | PL | [arXiv 2605.00347](https://arxiv.org/abs/2605.00347) | paper §3.3: "the chosen discrete action is repeatedly applied for a fixed number of consecutive frames" (15 for jumps, otherwise 5) |
| Orak fine-tuning | 2025-26 | Llama-3.2-1B/3B | SFT on LLM trajectories | 12 games | PL | [arXiv 2506.03610](https://arxiv.org/abs/2506.03610) | paper §5.4 and App.: "During LLM inference, we pause the Super Mario game environment" |
| Think in Games | 2025 | Qwen 14B/32B | SFT + GRPO on replay labels | Honor of Kings macro prediction | offline, not gameplay | [arXiv 2508.21365](https://arxiv.org/abs/2508.21365) | paper §3.1: "label the main player's action as the ground truth for each game state" (offline prediction) |
| HIMA agents | 2025 | Qwen-2 1.5B + LoRA | imitation of pro replays | StarCraft II | PL by default | [arXiv 2508.06042](https://arxiv.org/abs/2508.06042) | code: `main.py:23` `--realtime` default False |
| Timely-RL | 2026 | 8B LLM with timer tool | SFT + GRPO; zero reward if over the wall-clock budget | math, GPQA, Jericho text games | static with deadline | [arXiv 2601.16486](https://arxiv.org/abs/2601.16486) | paper §4.1: Jericho with assigned interaction delays; §5.2.2 over-budget answers count as incorrect |
| AnytimeReasoner | 2025 | reasoning LLM | RL with thinking truncated at sampled budgets | math | static | [arXiv 2505.13438](https://arxiv.org/abs/2505.13438) | paper §3: five math benchmarks at 32 token budgets |
| Elastic Reasoning | 2025 | reasoning LLM | GRPO with budget-constrained rollouts | math, code | static | [arXiv 2505.05315](https://arxiv.org/abs/2505.05315) | paper §4: math and code benchmarks |
| BudgetThinker | 2025 | reasoning LLM | periodic remaining-budget tokens; SFT + RL | (not extracted) | static | [arXiv 2508.17196](https://arxiv.org/abs/2508.17196) | paper §3.1 Evaluation Details |
| L1 | 2025 | reasoning LLM | RL reward minus length-target deviation | math | static | [arXiv 2503.04697](https://arxiv.org/abs/2503.04697) | paper §4 experimental setup (math) |
| AdaptThink / Thinkless | 2025 | reasoning LLM | RL to choose think or no-think | math | static | [AdaptThink](https://arxiv.org/abs/2505.13417), [Thinkless](https://arxiv.org/abs/2505.13379) | papers: AdaptThink §4, Thinkless §4.1 (math) |
| Interleaved Reasoning | 2025 | LLM | RL rewarding correct intermediate answers | QA | static | [arXiv 2505.19640](https://arxiv.org/abs/2505.19640) | paper §1: five datasets; TTFT on fixed questions |
| Dualformer; Distilling System 2 into 1 | 2024 | transformer / LLM | train on randomly dropped reasoning traces; distil | mazes, QA | static | [Dualformer](https://arxiv.org/abs/2410.09918) | papers: Dualformer §4.1 maze/Sokoban as one-shot generation; Distilling §4 |
| StreamingThinker | 2025 | Qwen3 | streaming CoT data, masks, parallel caches | QA | static | [arXiv 2510.17238](https://arxiv.org/abs/2510.17238) | paper §4.1 simulated input speed |
| Async-SFT | 2026 | 3B LLMs | clock-simulated streaming input data | tool benchmarks | static, simulated streaming clock | [arXiv 2605.13360](https://arxiv.org/abs/2605.13360) | paper (2605.13360) §4: token clock used to generate SFT data; §5 simulated streaming speech |
| Kyutai interactivity alignment | 2026 | Moshi, PersonaPlex text stream | GRPO with rule-based timing rewards | Full-Duplex-Bench v1, v2 | RL (speech) | [arXiv 2606.11167](https://arxiv.org/abs/2606.11167) | paper §1: GRPO on conversation segments; evaluated on Full-Duplex-Bench v1 (pre-recorded) and v2 (real-time) |
| STITCH, Mini-Omni-Reasoner, FLAIR | 2025-26 | speech LLMs | interleaved or latent reasoning | spoken QA | RL (speech) | [STITCH](https://arxiv.org/abs/2507.15375) | papers: STITCH §4, Mini-Omni-Reasoner §4.4 (Spoken-MQA), FLAIR §4 (speech benchmarks, Full-Duplex-Bench) |
| Training-time RTC | 2025 | flow VLA | delay simulated in training | robots | RL | [arXiv 2512.05964](https://arxiv.org/abs/2512.05964) | paper §3: inference delay in controller timesteps; §4 Kinetix and real robots |
| Real-Time EXPO-FT | 2026 | VLA + small edit policy | online RL | real robots at 30 Hz | RL | [arXiv 2609.18207](https://arxiv.org/abs/2609.18207) | paper §3: delay of d timesteps; real-world dynamic tasks |
| Think at 5 Hz, Act at 20 Hz | 2026 | action expert on frozen VLM | randomised cache staleness | CARLA | PL (CARLA synchronous mode) | [arXiv 2607.15621](https://arxiv.org/abs/2607.15621) | paper §4.4: "in CARLA's synchronous mode the vehicle still receives fresh control at every tick" |

### Notes

**No paper was found that post-trains a reasoning LLM or VLM against a live game clock and reports better realtime-live game scores.** The nearest pieces:

**Lumine** (ByteDance Seed). Three stages: 1,731 hours of human play, 200 hours instruction-labelled, 15 hours with annotated inner monologue. The model decides each step whether to think before acting and learns to think mainly at transitions. Thinking adds latency (234 ms to first action against 114 ms) and is sequential: think, then act. When to think is imitation-learned, not optimised against its time cost. In-domain ablation: 6.6% without thinking or history, 93.4% with both.

**Game-TARS sparse thinking.** Keep a thought only at timesteps where an action-only model mispredicts the human action, and only if the thought leads to the right action. 37 tokens per step against 68. A ready data-construction rule for "reason only when needed". Evaluated paused.

**CombatVLA.** Output is action, then a truncation token, then explanation; generation stops at the truncation token at inference. A simple way to train with reasoning supervision and skip it at run time.

**Timely-RL** (Ma et al.). Reward is zero if over time; if correct and on time, accuracy plus a bonus for using the budget. Generation time is rescaled during RL to imitate faster or slower hardware. TimelyLM-8B against Qwen3-8B: on-time rate at 0.75x budget on AIME 53.3% against 30.0%. The closest existing reward design, but the world does not change while the model thinks.

**AnytimeReasoner.** The model must give its best answer at randomly sampled truncation points, which yields dense rewards. This is the natural objective for "be interruptible at any time" and maps onto a realtime environment where the deadline is the next tick.

**Kyutai interactivity alignment** (Ohashi, Zeghidour, Defossez, Kharitonov). GRPO on the text stream only, with rule-based timing rewards computed from sampled continuations (pause handling, response delay, backchannel timing) and a KL anchor to the frozen model. Moshi interruption latency 1.377 s to 0.461 s; PersonaPlex turn-taking latency 0.219 s to 0.079 s. The closest published analogue of the team's step 3; the recipe transfers if the reward is a game score and the segment is a short episode.

**Async-SFT** (Hooper et al., Berkeley). A clock-based simulator generates fine-tuning data where input arrives mid-generation; 3B models get about 2x lower latency at similar accuracy. A direct template for data where stimulus lands mid-thought.

**Odysseus** (Princeton). PPO with a lightweight turn-level critic scales RL on a VLM to 100+ turn episodes; at least three times the progress of frontier models in Super Mario Land. A candidate optimiser if a time cost is added.

**Orak fine-tuning.** SFT of small Llama models on LLM trajectories lifts Street Fighter III from 12.0 to 40.0 paused. No fine-tuning aimed at the unpaused setting.

**Think in Games** does not play Honor of Kings live; it predicts macro actions for replay snapshots (66.67% to 86.84% with GRPO).

### What the team could reuse
- Reward shaping: Timely-RL's deadline reward; AnytimeReasoner's random truncation; Kyutai's rule-based timing rewards with a KL anchor.
- Data recipes: sparse thinking; action-first with truncated explanation; trace dropout (Dualformer); clock-simulated streaming data (Async-SFT); time-offset or delay-conditioned labels (SIMA, training-time RTC); randomised staleness.
- Optimisers: GRPO variants; Odysseus PPO for long episodes.
- Environment for rollouts: a token clock makes realtime-live rollouts reproducible and hardware independent.

---

## 5. Gaps: what nobody appears to have done

Based on the searches run; absence of evidence is not proof.

1. **Post-training against a live clock.** No RL or fine-tuning of a reasoning LLM or VLM with reward computed in a realtime-live game. The 2026 realtime benchmarks stop at evaluation or prompt-level adaptation (TORSI). RealtimeGym's authors list it as future work.
2. **Interaction models on games.** No full-duplex or interaction model (TML-Interaction-Small, Moshi, PersonaPlex, MiniCPM-o) has been evaluated as a player on a verifiable realtime game. Realtime-Bench includes realtime API models and finds them weak, but not trained interaction models.
3. **An action stream in a duplex model.** All duplex output channels are text and audio. Multi-stream prediction has not been extended to keyboard, mouse or gamepad actions.
4. **Concurrent free-form reasoning and acting in one model.** Moshi's inner monologue is its own transcript; TML and Dispider push reasoning to a background model; Lumine, Game-TARS and SIMA 2 think then act. Concurrent think-and-respond exists for QA only (Asynchronous Reasoning).
5. **Mid-thought steering in decision tasks.** Interruptibility is diagnosed on static math and code; nobody has trained for it or tested it in an environment. AgileThinker avoids the problem with a second model.
6. **Deciding to open more channels.** Nothing found on a model spawning extra perception or reasoning streams on demand.
7. **Multi-channel output under a clock.** Acting while speaking plus thinking is studied in speech models only, never combined with game control.
8. **Human baselines under the same clock.** Only LOLPlay (two players), GameWorld (paused mode) and a few others have human numbers; Realtime-Bench, RealtimeBench, ROAR, RealtimeGym and OmniGameArena have none.
9. **Like-for-like comparison of the three baseline families** (fast action models, low-reasoning frontier LLMs, interaction models) on one realtime-live environment with one clock. Realtime-Bench and OmniGameArena come closest.
10. **Reaction-time-versus-score curves for LLM agents**, analogous to FTW's added-delay study or RTC's delay sweep. RealtimeBench's 1x/1.5x/2x and ROAR's two tick rates are the only partial instances.
11. **Robotics delay methods ported to LLM agents.** Prefix commitment, training-time delay conditioning, future-state conditioning and per-tick correction heads have not been applied to text-action LLMs in games.
12. **Weight-level distillation of slow reasoning into fast reaction for a realtime game.** TORSI does it in prompts; HIMA clones human replays.
13. **Scaffold comparison.** No head-to-head of two-thread, FSM code-as-policy, speculative and offline-guidance scaffolds on one benchmark and clock. Realtime scaffolds at human tick rates all rely on a hand-written executor; the LLM never issues the low-level action.
14. **Short, human-easy, pixel-plus-low-level-action tasks under a real clock.** Existing realtime benchmarks use text state with macro actions (RealtimeGym, RealtimeBench), 1 FPS GUI control (Realtime-Bench), or long commercial games (LOLPlay, VideoGameBench).
