# Parallelized Planning-Acting

Parallelized Planning-Acting runs planning and acting threads with a single-slot buffer where a new plan interrupts the running action, on an unpaused Minecraft server.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2503.03505](https://arxiv.org/abs/2503.03505) |
| Demo | [Official demo videos in the repo README](https://github.com/zju-vipa/Odyssey/tree/master/Multi-Agent#demo) ([ender_dragon.mp4](https://raw.githubusercontent.com/zju-vipa/Odyssey/master/Multi-Agent/demo/ender_dragon.mp4), [wither.mp4](https://raw.githubusercontent.com/zju-vipa/Odyssey/master/Multi-Agent/demo/wither.mp4)): spectator-mode recordings of a large team of LLM agents beating the Ender Dragon and the Wither on a running server, with a boss-health counter and in-game chat. Recordings, some sped up; not human-playable. |
| Category | scaffold |
| Method | Planning and acting threads; single-slot buffer where a new plan interrupts the running action |
| Evaluated on | Minecraft, unpaused server |
| Evaluation play mode | realtime-live (skills are scripted) |
| Results | 3 agents halve diamond-armor time |
| Basis | paper §3.2: "The game server operates continuously without pausing during interactions with LLMs" |

## Details

- Minecraft convertibility (from the environments review): the server already runs at 20 TPS and at least one harness runs unpaused (Parallelized Planning-Acting, [arXiv 2503.03505](https://arxiv.org/abs/2503.03505)).

## Demo

- [video] [Odyssey Multi-Agent README demo](https://github.com/zju-vipa/Odyssey/tree/master/Multi-Agent#demo) — Opened the README (code repo zju-vipa/Odyssey, Multi-Agent folder, linked from the arXiv v1 HTML; no homepage set) and loaded both linked MP4s in a video element, seeking to 5, 30, 60 and 90% and screenshotting each. README: "All demonstration videos were captured using the spectator mode within Minecraft. To comply with GitHub's file size restrictions, some videos have been accelerated." "Agents defeating the Ender Dragon" (ender_dragon.mp4, 57.8 s, 1920x1080): about 15 diamond-armored agents in the End; chat shows "<SystemInfo> All End Crystals have been destroyed." and "<SystemInfo> Boss Health: 25". "Agents defeating the Wither" (wither.mp4, 36.4 s): named agents (Chris, Eric, Steve, William, Frank and others) fight the Wither in the Nether; the boss-health readout falls from 300 to 153, and an agent posts a plan in chat: "<Henry> The wither's health is dropping! Melee fighters, prepare to attack once it's below 150 health. Ranged attackers, focus on the wither until then. Healers, keep an eye on our health bars!" Play-mode evidence (recording): the boss keeps moving and attacking while agents chat and act, consistent with an unpaused server, but no wall clock or latency overlay is shown and some videos are sped up.
- Note: the videos show boss fights with about 15 agents, not the 3-agent diamond-armor task in the Results row.

Visited 10 November 2026 in a headless browser.

## What the team could reuse

- Harness pieces: single-slot interrupt buffer (from the scaffolds reuse list).

Related: [Voyager](../environments/voyager.md); [MINDcraft](../environments/mindcraft.md); [Mineflayer](../environments/mineflayer.md)
