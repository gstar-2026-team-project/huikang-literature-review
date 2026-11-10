# OmniGameArena

OmniGameArena is a set of 12 new Unreal Engine 5 games played paused (PDQ) or with model inference time charged to the game clock (LCRT).

| | |
|---|---|
| Year | 2026 |
| Authors / org | Lin, Qian, Liu, Huang et al. (HKU, LIGHTSPEED, CUHK, Tsinghua) |
| Links | [arXiv 2606.09826](https://arxiv.org/abs/2606.09826), code [mxlin043/OmniGameArena](https://github.com/mxlin043/OmniGameArena) |
| Demo | [project page](https://mxlin043.github.io/OmniGameArena/): a leaderboard plus recorded gameplay videos per model and game, with a toggle between latency-free and latency-charged mode. In the latency-free clips the UE5 countdown clock is frozen while the model thinks; in the latency-charged clips it keeps running beside a 'Thinking...' panel. Human-playable: no (the UE5 environment is available to download from HF/ModelScope). |
| Play mode | paused-live (PDQ) + realtime-live (LCRT) |
| Clock | paused / INJECT |
| Observation | RGB + timestamp |
| Action | chunked keyboard-mouse |
| Players | 1, PvP, co-op |
| Horizon | short |
| Human reference | none |
| Open source | repo open (LICENSE file) |
| Convertible to realtime-live | has LCRT |
| Basis | code: README "LFM pauses the game during inference; LCM charges model inference time to the game clock", `omni_game_arena/clock.py` `decision_latency`; paper: PDQ "freezes the environment", LCRT "idles for the server-reported inference time" |

## Details

- OmniGameArena (Jun 2026).
- Lin, Qian, Liu, Huang et al. (HKU, LIGHTSPEED, CUHK, Tsinghua). [arXiv 2606.09826](https://arxiv.org/abs/2606.09826); code [mxlin043/OmniGameArena](https://github.com/mxlin043/OmniGameArena) (read). The repo calls the two clocks LFM ("pauses the game during inference") and LCM ("charges model inference time to the game clock", `--clock lcm`, implemented in `omni_game_arena/clock.py`).
- Tasks: 12 new Unreal Engine 5 games: 7 solo (ObstacleRun3D, ObstacleRun2D, LastStand, MonsterShoot, SceneEscape, CueChase, SoloCraft), 3 PvP, 2 co-op.
- Play modes: PDQ (paused, main tables); LCRT (the simulator idles for the server-reported inference time before the action applies, an INJECT clock). LCRT was run for four models only.
- Observation: RGB frame + timestamp. Action: chunked keyboard-mouse. No human reference.
- Results: GPT-5.5 leads 4 of 7 solo games paused; under LCRT its SharedFloor score goes 0.368 to 0.048 and MonsterShoot drops by about 0.41, at about 16 s of model time per call. It includes two action models (NitroGen, Open-P2P) alongside frontier VLMs.

## Demo

- [project-page] [OmniGameArena project page](https://mxlin043.github.io/OmniGameArena/) — Loaded the page, switched the "Gameplay recordings" gallery between "Latency-free mode" and "Latency-charged mode" and the Solo/PvP/Coop tabs, and seeked two recorded MP4s (lfm_or2d_gpt55.mp4, 13.3 s; lcm_last_gpt55.mp4, 50.4 s). Each clip shows the UE5 game with a countdown clock beside a per-step Reason/Action log; the page also has cards for the 12 games, a cold-start leaderboard (12 agents plus Random and Human expert) and Improvement Dynamics Curve charts. Latency-charged clips exist only for LastStand, MonsterShoot and SoloCraft under Solo (GPT-5.5, GPT-5.4, Opus 4.6, Sonnet 4.6). Play-mode evidence (recordings): in lcm_last_gpt55 the clock reads 02:48 at 0:05 with "Step 0 Thinking..." and 02:06 at 0:30 with "Step 2 Thinking...", so the clock runs during inference; in lfm_or2d_gpt55 the clock stays at 02:48 at 0:05 and 0:10 while several steps pile up, matching the page text "The game is paused while the model thinks." Nothing runs live and nothing is playable.

Visited 10 November 2026 in a headless browser.

## Fit

realtime via injection; verifiable; 7 solo games; human-easy unmeasured; short.

Related: [NitroGen](../solutions/nitrogen.md); [Open-P2P](../solutions/open-p2p.md)
