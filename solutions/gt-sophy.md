# GT Sophy

GT Sophy is a Gran Turismo racing agent with 10 Hz control in a game that runs only in real time.

![GT Sophy cars racing human drivers on the final lap at Dragon Trail Seaside](../assets/gifs/sol-gt-sophy.gif)

*Recording from the official broadcast of Race Together 2021 Race 1: GT Sophy cars (Sophy Violette, Verte, Noire) duel on the final lap at real-time speed, with a camera cut partway through. Source: [Gran Turismo Sophy Race Together 2021 #1, Polyphony Digital / Sony AI](https://www.youtube.com/watch?v=4Gfm317R7l4).*

| | |
|---|---|
| Year | 2022 |
| Links | [paper page](https://ai.sony/publications/Outracing-champion-Gran-Turismo-drivers-with-deep-reinforcement-learning) |
| Demo | [GT Sophy Race Together](https://www.gran-turismo.com/us/gran-turismo-sophy/race-together/) ([site](https://www.gran-turismo.com/us/gran-turismo-sophy/)): recorded broadcasts of live 2021 races against top human drivers, with GT Sport physics running in real time; the site itself gives no latency figure (10 Hz control per the paper). Nothing playable; human-playable: no. |
| Category | RL and decision model |
| Method | 10 Hz control, game runs only in real time |
| Evaluated on | Gran Turismo |
| Evaluation play mode | realtime-live on PS4 |
| Basis | paper: "GT Sophy interacted with the game at 10 Hz"; "Although GT ran only in real time" |

## Demo

- [project-page] [Gran Turismo Sophy site](https://www.gran-turismo.com/us/gran-turismo-sophy/) — Loaded the landing, Race Together and Technology pages and opened the Race Day #1 broadcast "[English] Gran Turismo Sophy RACE TOGETHER 2021 #1" (1:36:14), seeking to 120 s and 600 s. Race Days were 2 Jul 2021 and 21 Oct 2021, with three races (Dragon Trail Seaside N500, Lago Maggiore Gr.3, Sarthe Gr.X); YouTube IDs 4Gfm317R7l4, RbkvlcwP1FM, _RCvq_63nD8, dxmIAy9ShZg, nZbA_CDoWrk, oGbe4Zx-jDA, vIShQ2yD5K4; the Technology page describes DART on more than 1,000 cloud PS4 consoles. Play-mode evidence (recording): broadcasts of live races where GT Sport physics runs in real time beside human drivers; the site gives no reaction-time figure (the Nature paper and Sony AI write-ups, via search, give a 10 Hz control cap, about 23-30 ms inference latency, and superhuman results with 100-250 ms added delay). Nothing playable on the site.

Visited 10 November 2026 in a headless browser.

Related: [Gran Turismo Sophy interface](../environments/gran-turismo-sophy.md)
