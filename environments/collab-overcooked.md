# Collab-Overcooked

Collab-Overcooked is a step-based two-LLM Overcooked benchmark with atomic actions and chat.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2502.20073](https://arxiv.org/abs/2502.20073) |
| Demo | [EMNLP 2025 poster talk on Underline](https://underline.io/lecture/130001-collab-overcooked-benchmarking-and-evaluating-large-language-models-as-collaborative-agents): official 7-minute narrated slide video with static benchmark diagrams; no gameplay footage, replay viewer or hosted playable page. The [repo](https://github.com/YusaeMeow/Collab-Overcooked) has a local-only browser mode for a human to play with an agent teammate. |
| Play mode | paused-live |
| Clock | STEP |
| Observation | text |
| Action | atomic + chat |
| Players | 2 LLMs |
| Horizon | under 100 steps |
| Human reference | humans 90-100% with 10 s/step limit |
| Open source | open |
| Convertible to realtime-live | harness change |
| Basis | code: `src/main.py` (`team.joint_action` then `env.step` per timestep) |

## Details

- Collab-Overcooked ([arXiv 2502.20073](https://arxiv.org/abs/2502.20073)): step-based; humans under a 10 s per-step limit reach 90-100%, GPT-4o 4% at level 6. LLMs had no wall-clock limit.
- Convertibility (Overcooked family): easy. DPT-Agent already runs overcooked-ai at 4 Hz wall clock. A scripted partner makes it effectively single player.

## Demo

- [official video] [EMNLP 2025 poster presentation on Underline](https://underline.io/lecture/130001-collab-overcooked-benchmarking-and-evaluating-large-language-models-as-collaborative-agents): I played the video (duration 435 s, 640 px wide) and seeked to 20 s, 90 s and 180 s. It is a narrated slide talk with an automatic transcript. The frames show title slides such as "Contribution" and "How to Enforce Collaboration", with a static diagram of the "Task: Baked Potato Slices" kitchen, Alice and Bob's chat requests and their executed actions. The narration describes "resource isolation", "asymmetric task knowledge" and "30 tasks across 6 levels". Play-mode evidence: none. There is no gameplay footage, step counter or clock, only static figures from the paper.
- [local playable, not hosted] [GitHub repo README](https://github.com/YusaeMeow/Collab-Overcooked): the README documents `python src/human_play.py --order boiled_egg`, which serves a page at http://127.0.0.1:8080 where a human controls one chef with WASD/Space while "a deterministic recipe baseline" or a model server controls the other ("there is no chat channel between the human and the agent"). The repo has no homepage field and no GitHub Pages site (yusaemeow.github.io/Collab-Overcooked returns 404), so I could not open a hosted copy. The arXiv abstract comments list no demo.

Visited 10 November 2026 in a headless browser.

Related: [Overcooked-AI](overcooked-ai.md); [DPT-Agent Overcooked](dpt-agent-overcooked.md); [Robotouille](robotouille.md); [TimeArena](timearena.md)
