# Voyager

Voyager is an LLM agent that writes Mineflayer JavaScript skills for Minecraft.

| | |
|---|---|
| Year | 2023-25 |
| Links | [Voyager](https://arxiv.org/abs/2305.16291) |
| Demo | [project page](https://voyager.minedojo.org/): a gallery of 9 short edited, recorded Minecraft clips (mine amethyst, build nether portal, etc.) plus static figures. There is no live or replay viewer, and the code pauses the server while GPT-4 is queried, so the game waits for the model. Human-playable: no. |
| Category | scaffold |
| Method | LLM writes code, behaviour trees or bots |
| Evaluated on | Minecraft, 3D games, code arenas |
| Evaluation play mode | scripted (Voyager also pauses the server during LLM calls) |
| Results | out of scope |
| Basis | code: Voyager `voyager/env/bridge.py:113-124` |

## Demo

- [project-page] [Voyager project page](https://voyager.minedojo.org/) — Loaded the page, scrolled it and played each of the 9 gallery videos (muted, frames at 10%, 50% and 90%). The gallery holds 9 short looping, edited MP4 clips of 14-34 s each (Mine Amethyst as diamond.mp4, Gather Cactus, Build Base, Enderman, House, Gold, Build Nether Portal, Pig, Fish) with caption overlays, followed by static figures (exploration curve, skill library, tech tree, map coverage, zero-shot table, ablation); there is no playable game, live model or replay viewer, and some external resources fail to load. Play-mode evidence (recordings): no tick counter, timestamps or latency readout; progress is reported in "prompting iterations" (63 items within 160 iterations), and the clips show no sign of GPT-4 thinking time, so they appear condensed. The linked code (voyager/env/bridge.py pause()/unpause() posting to the mineflayer server's /pause endpoint, which sends '/pause' in chat) unpauses during skill execution and pauses afterward, so the world is frozen while GPT-4 is queried.

Visited 10 November 2026 in a headless browser.

Related: [Voyager](../environments/voyager.md) (environment details); [PORTAL](portal.md); [CodeClash](codeclash.md)
