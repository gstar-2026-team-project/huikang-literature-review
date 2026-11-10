# STEVE-1

STEVE-1 is a Minecraft model listed with the VPT line on the 20 Hz native interface with a synchronous simulator.

| | |
|---|---|
| Year | 2022-25 |
| Category | RL and decision model |
| Method | 20 Hz native interface; synchronous simulator |
| Evaluated on | Minecraft |
| Evaluation play mode | paused-live |
| Demo | [project page](https://sites.google.com/view/steve-1): official project page with seven embedded YouTube videos of STEVE-1 playing Minecraft (four text-instruction sessions, one visual-instruction session, two prompt-chaining clips). Recordings only; not human-playable and no live model. |
| Basis | paper (VPT) App. C: client and server "run in the same thread ... slower or faster than real time"; code: MineRL `_multiagent.py` synchronous token |

## Demo

- [project page / video] [STEVE-1 project page](https://sites.google.com/view/steve-1) (homepage field of github.com/Shalev-Lifshitz/STEVE-1) — Opened in a headless browser, played and seeked each of the seven embedded YouTube clips and screenshotted frames. Sections: "Demo: Interactive Sessions with STEVE-1 Following Text Instructions" ("In these clips, we use text instructions in real-time to control STEVE-1 playing Minecraft"), with "STEVE-1: Interactive Text 1" to "4" (0:51, 1:37, 1:49, 0:48) showing first-person Minecraft footage beside the current prompt ("chop a tree", "place a torch", "dig a hole, get dirt, mine dirt", "place torches"); a visual-instructions session (1:15) with a "Visual Prompt" panel; and "Demo: STEVE-1 with Prompt Chaining" ("Half way through each clip, we switch to the second prompt"): "Prompt chaining 'build a tower'" and "Prompt Chaining 'make wooden planks'" (2:05 each). Play-mode evidence (recording): pre-recorded MP4s; no on-screen tick counter or clock, and nothing shows whether the simulator was paused while the policy computed each action.
- Note: the caption says the text instructions were given "in real-time", which describes the human switching prompts during a session; it does not show the environment kept running without waiting for the model, so it does not contradict the paused-live label, but it is not evidence for it either.

Visited 10 November 2026 in a headless browser.

Related: [VPT](vpt.md); [MineRL](../environments/minerl.md)
