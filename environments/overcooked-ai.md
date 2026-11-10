# Overcooked-AI

Overcooked-AI is a step-locked gym whose web demo runs human-AI games on a real tick.

| | |
|---|---|
| Year | 2019 |
| Authors / org | Carroll et al. |
| Links | [repo](https://github.com/HumanCompatibleAI/overcooked_ai) |
| Demo | [Live demo](https://humancompatibleai.github.io/overcooked-demo/) (redirects to humancompatible.ai/overcooked-demo) + [replay viewer](https://humancompatible.ai/overcooked-demo/replay): in-browser human-vs-RL-agent play (PPO-BC/self-play/PBT TF.js policies, not LLMs) on a fixed 150 ms wall-clock tick (~6.7 fps) where idle input = STAY, plus a viewer for recorded trajectory JSONs; human-playable: yes. |
| Play mode | paused-live (gym) + realtime-live (web demo, 6 ticks/s) |
| Clock | STEP |
| Observation | grid state |
| Action | 6 actions |
| Players | 2 |
| Horizon | about 60 s |
| Human reference | humans |
| Open source | MIT |
| Convertible to realtime-live | low effort |
| Basis | code: `overcooked_ai_py/mdp/overcooked_env.py` `step(joint_action)`; `overcooked_demo/server/app.py` `play_game(game, fps=6)` "Asynchronously apply real-time game updates" |

## Details

- Overcooked-AI (Carroll et al., [repo](https://github.com/HumanCompatibleAI/overcooked_ai), MIT): step-locked gym; its web demo runs human-AI games on a real tick.
- Convertibility (Overcooked family): easy. DPT-Agent already runs overcooked-ai at 4 Hz wall clock. A scripted partner makes it effectively single player.

## Demo

- [playable] [Overcooked-AI live demo](https://humancompatibleai.github.io/overcooked-demo/) — Played live (redirects to humancompatible.ai/overcooked-demo/): Player 1 'Human-aware PPO agent', Player 2 'Human Keyboard Input', layout Cramped Room, 25 s game, about 27 s of arrow-key play; read the bundled demo.js. The PPO partner delivered a soup (Score 0 to 20 while Time Left ran 22 to 9) and 'Time up' was logged at the end. Agents are small TF.js models (static/assets/ppo_bc_cramped_room_agent/model.json) run in the browser; no LLM is involved. Play-mode evidence (played live, code): PARAMS.TIMESTEP_LENGTH is 150 ms (about 6.7 fps) in a setInterval loop; each tick runs the NPC models synchronously, takes the human's latest key or STAY, and steps the MDP; Time Left is computed from Date().getTime() - start_time, and the countdown dropped about 1 per second. The agents finish well within a tick, so model thinking time never shows as lag. This hosted demo is the older client-side version, not the Flask server (app.py, fps=6) cited in Basis.
- [replay-viewer] [Overcooked-AI replay viewer](https://humancompatible.ai/overcooked-demo/replay) — Opened it and pressed Enter; it loaded static/assets/test_traj.json and played it back ('Replay Fixed Overcooked Trajectories', console 'Trajectory replay'), with a scrub slider, Reset / Clear File buttons and upload of your own trajectory JSON. The bundled trajectory uses an onion+tomato layout with 'Orders: onion, any' and a Time Left counter. Play-mode evidence (recording): a recorded file, not a live agent.
- [project-page] [Overcooked-AI instructions](https://humancompatible.ai/overcooked-demo/instructions) — Read the static instructions for human players: arrow keys to move, Space to interact, 3 onions start a soup that cooks to 20, then plate and serve at the grey counter.

Visited 10 November 2026 in a headless browser.

Related: [DPT-Agent Overcooked](dpt-agent-overcooked.md); [HLA Overcooked](hla-overcooked.md); [Collab-Overcooked](collab-overcooked.md); [Robotouille](robotouille.md); [TimeArena](timearena.md); [Real-Time Reasoning Gym](realtime-gym.md)
