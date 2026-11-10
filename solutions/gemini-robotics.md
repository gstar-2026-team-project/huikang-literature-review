# Gemini Robotics

Gemini Robotics uses a cloud backbone under 160 ms with a local decoder that gives a 50 Hz effective control rate.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2503.20020](https://arxiv.org/abs/2503.20020) |
| Demo | [launch blog](https://deepmind.google/blog/gemini-robotics-brings-ai-into-the-physical-world/) with four official YouTube videos (e.g. [Dynamic interactions](https://www.youtube.com/watch?v=HyQs2OAIf-I)), and the [Gemini Robotics model page](https://deepmind.google/models/gemini-robotics/) (now showing the later 2.x models): recorded videos of real robots (ALOHA 2 bi-arm) doing tasks in real time, labelled "Autonomous 1x". Not a game, not interactive, no live model calls. |
| Category | RL and decision model |
| Method | cloud backbone under 160 ms; local decoder gives 50 Hz effective |
| Evaluated on | robots |
| Evaluation play mode | realtime-live |
| Basis | paper §3.1: backbone "under 160ms"; end-to-end "approximately 250ms"; "effective control frequency is 50Hz" |

## Demo

- [official-video] [Launch blog "Gemini Robotics brings AI into the physical world"](https://deepmind.google/blog/gemini-robotics-brings-ai-into-the-physical-world/) (12 March 2025) — Opened the page and listed its media: four YouTube embeds titled "Gemini Robotics: Bringing AI to the physical world" (4MvGnmmP3c0), "Generality in action" (sY20x_tyWpQ), "Dynamic interactions" (HyQs2OAIf-I) and "Dexterous skills" (x-exzZ-CIUw), with captions such as "A demonstration of Gemini Robotics's world understanding." and "Gemini Robotics displays advanced levels of dexterity". The blog says that if "an object slips from its grasp, or someone moves an item around, Gemini Robotics quickly replans and carries on". Play-mode evidence (recording): these are edited recordings of real robot runs, not a live session.
- [official-video] [Gemini Robotics: Dynamic interactions](https://www.youtube.com/watch?v=HyQs2OAIf-I) (1:40) — Played the video and jumped to 0:15, 0:45 and 1:30. It shows a bi-arm robot putting fruit into containers while a person moves the containers and objects around. The on-screen labels read "Interactive" and "Autonomous 1x". Play-mode evidence (recording): the "Autonomous 1x" label says the footage is unassisted and not sped up, so the robot is reacting in real time to a moving scene. This matches realtime-live, but it is a recording, not a live model.
- [official-video] [Gemini Robotics model page](https://deepmind.google/models/gemini-robotics/) — Opened the page and played its first video, a 23.6 s autoplay hero clip (`gemini-robotics__page-cover__hero__20.webm`), up to 6.3 s. The page now covers the later "Gemini Robotics 2.5", "Gemini Robotics ER 2" and "Gemini Robotics On-Device 2" models, with short silent clips (`gemini-robotics-2__hands-on__whole-body.webm`, `__dexterity.webm`, `__multi-robot.webm`) and four YouTube embeds. "Try Gemini Robotics ER 2" opens AI Studio, which needs a sign-in, so I did not try it. That model is the later embodied-reasoning model, not the 2025 VLA in this file. The VLA itself is open only through a trusted-tester waitlist. Play-mode evidence: recordings only; no live control is open to the public.

Visited 10 November 2026 in a headless browser.
