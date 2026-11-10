# Game-TARS game suite

Game-TARS was evaluated on web games run with time-pause, plus Minecraft (MCU) and ViZDoom on synchronous simulators.

| | |
|---|---|
| Year | 2025 |
| Authors / org | ByteDance Seed |
| Links | [arXiv 2510.23691](https://arxiv.org/abs/2510.23691) |
| Demo | [Game-TARS page](https://seed-tars.com/game-tars): project page with pre-recorded montage videos of agent rollouts in Minecraft and unseen web/Windows games, with per-step Thought/Action text. The videos do not show whether the game kept running or was paused during inference. Human-playable: no. Live model: no. |
| Play mode | paused-live |
| Clock | Game-TARS web games time-paused; UI-TARS-2 synchronous browser sandbox |
| Observation | screenshots |
| Action | keyboard/mouse |
| Players | 1 |
| Horizon | short |
| Human reference | human-normalised |
| Open source | not released |
| Convertible to realtime-live | un-pause the sandbox |
| Basis | paper 2510.23691 §5 footnote: "used time-pause to ensure causal interaction" |

## Details

- Game-TARS (ByteDance Seed), [arXiv 2510.23691](https://arxiv.org/abs/2510.23691): web games were run with time-pause "to ensure causal interaction" because of inference latency. Game-TARS's Minecraft (MCU) and ViZDoom runs use synchronous simulators (MineStudio; ViZDoom default `PLAYER`), so the whole suite is paused-live.
- Convertibility: the ByteDance sandboxes are not released.
- Game-TARS reports ViZDoom results (figures only).

## Demo

- [video] [Game-TARS blog page](https://seed-tars.com/game-tars) — Loaded the ByteDance Seed post (Oct 24, 2025) and seeked its two recorded montages, game-tars-minecraft-2.mp4 (45.6 s) and game-tars-unseen.mp4 (40.4 s), to 5/30/60/90%; the network log shows only static mp4 files and analytics, no model calls. The Minecraft video has four panels (kill_entity:fox, kill_entity:creeper, craft_item, mine_block:terracotta) with action-log overlays such as "Action: move(dx='0.0', dy='-2.0')" and keyDown(...); the unseen-games grid (Racing, Temple Run, Plane in the Air, Jump Only, Vizdoom Battle-1/2, Chaze Horizon, Stardew Valley and other Windows games) shows per-tile Chinese "Thought:" text and "Action:" lines (keyPress, mouseMove). Caption: "GameTARS can follow human instructions, reason and play unseen games on web, OS, and simulators." Play-mode evidence (recording): agent runs, but nothing on screen (latency, tick counter, clock) shows whether the game kept running or was paused; the page copy claims "Human-Native Real-Time Interaction" and a "sparse ReAct" pattern. Links go to arXiv 2510.23691, the UI-TARS GitHub repo and UI-TARS-1.5-7B weights (not Game-TARS weights).

Visited 10 November 2026 in a headless browser.

Related: [Game-TARS](../solutions/game-tars.md) (the model); [UI-TARS-2 game suite](ui-tars-2.md); [ViZDoom](vizdoom.md); [MCU / MineStudio](mcu-minestudio.md)
