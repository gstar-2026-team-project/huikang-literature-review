# Voyager

Voyager is a Minecraft code agent that writes Mineflayer JavaScript skills, with the server paused during LLM calls.

| | |
|---|---|
| Year | 2023-25 |
| Links | [arXiv 2305.16291](https://arxiv.org/abs/2305.16291), [repo](https://github.com/MineDojo/Voyager) |
| Demo | [project page](https://voyager.minedojo.org/): a gallery of 9 short edited, recorded Minecraft clips (mine amethyst, build nether portal, etc.) plus static figures. There is no live or replay viewer, and the code pauses the server while GPT-4 is queried, so the game waits for the model. Human-playable: no. |
| Play mode | scripted (Voyager, Odyssey: server paused during LLM calls) / realtime-live (MINDcraft) |
| Clock | server 20 TPS |
| Observation | structured state |
| Action | JS skills / commands |
| Players | 1+ |
| Horizon | long |
| Human reference | none |
| Open source | open |
| Convertible to realtime-live | restrict to low-level controls |
| Basis | code: Voyager `voyager/env/bridge.py:113-124` (unpause -> run skill -> pause) |

## Details

- Minecraft code agents: Voyager, Odyssey, MINDcraft.
- Voyager ([arXiv 2305.16291](https://arxiv.org/abs/2305.16291); [repo](https://github.com/MineDojo/Voyager)) and Odyssey write Mineflayer JavaScript skills. Voyager pauses the server during LLM calls, confirmed in code: `voyager/env/bridge.py` calls `unpause()` before executing a skill and `pause()` after it, and `installation/fabric_mods_install.md` lists the Multi Server Pause mod as "used to pause the server when waiting for GPT-4 to reply". So Voyager is scripted with a paused world between skills.
- Convertibility: the server already runs at 20 TPS and at least one harness runs unpaused (Parallelized Planning-Acting, [arXiv 2503.03505](https://arxiv.org/abs/2503.03505)). To make latency bite, restrict actions to low-level controls and score survival time or kills in a short arena. The high-level API otherwise hides all sensorimotor difficulty.

## Demo

- [project-page] [Voyager project page](https://voyager.minedojo.org/) — Loaded the page, scrolled it and played each of the 9 gallery videos (muted, frames at 10%, 50% and 90%). The gallery holds 9 short looping, edited MP4 clips of 14-34 s each (Mine Amethyst as diamond.mp4, Gather Cactus, Build Base, Enderman, House, Gold, Build Nether Portal, Pig, Fish) with caption overlays, followed by static figures (exploration curve, skill library, tech tree, map coverage, zero-shot table, ablation); there is no playable game, live model or replay viewer, and some external resources fail to load. Play-mode evidence (recordings): no tick counter, timestamps or latency readout; progress is reported in "prompting iterations" (63 items within 160 iterations), and the clips show no sign of GPT-4 thinking time, so they appear condensed. The linked code (voyager/env/bridge.py pause()/unpause() posting to the mineflayer server's /pause endpoint, which sends '/pause' in chat) unpauses during skill execution and pauses afterward, so the world is frozen while GPT-4 is queried.

Visited 10 November 2026 in a headless browser.

Related: [Voyager](../solutions/voyager.md) (the agent); [Odyssey](odyssey.md); [MINDcraft](mindcraft.md); [Mineflayer](mineflayer.md); [Parallelized Planning-Acting](../solutions/parallelized-planning-acting.md)
