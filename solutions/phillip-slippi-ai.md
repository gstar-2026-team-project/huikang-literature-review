# Phillip / slippi-ai

Phillip (slippi-ai) plays Melee with a 12-15 frame imposed delay plus a predictive model.

| | |
|---|---|
| Year | 2017- |
| Links | [arXiv 1810.07286](https://arxiv.org/abs/1810.07286) |
| Demo | [x_pilot Twitch channel](https://twitch.tv/x_pilot): live stream "Play vs the Phillip AI (!help)" where the bot plays humans over Slippi netplay in real time (Ping, FPS 59.8 and "Delay: 20f" overlays); human-playable via netplay per the repo README. Also: recorded YouTube matches vs top players, e.g. [Zain plays Phillip the AI in first to 5 wins](https://www.youtube.com/watch?v=c8nRFAGvr2c). |
| Category | RL and decision model |
| Method | 12-15 frame imposed delay + predictive model |
| Evaluated on | Melee |
| Evaluation play mode | realtime-live in netplay |
| Basis | paper (1810.07286) §1: "we add fixed delay between the time an agent chooses an action" and when it is applied; "12 frames to be the lowest" human-plausible delay |

## Details

- **Phillip.** Imposed frame delay plus a learned predictive model so the policy acts on the state at execution time.
- Human reference numbers used as constraints: Melee 12 frames as the lowest human-plausible delay (Firoiu et al.).

## Demo

- [live-model] [x_pilot Twitch channel](https://twitch.tv/x_pilot) (linked from the [slippi-ai README](https://github.com/vladfi1/slippi-ai) "Playing the Bot") — Opened it in headless Chrome; the channel was live with title "Play vs the Phillip AI (!help)" (Super Smash Bros. Melee, 2 viewers, uptime 45:01:25) and I captured three video frames 10 s apart. It shows a Fox ditto on Final Destination between "phillip" and a netplay opponent "Combo Me Daddy", with overlays "Ping: 35-53", "FPS: 59.80-59.82" and "Delay: 20f". Play-mode evidence (live): the in-game timer went 06:21 to 06:01 over about 20 s of wall-clock while percents changed (10%/80% to 24%/26%), i.e. the match runs at normal speed against a human opponent; per the README anyone can play it via netplay ("Due to phillip's high delay (18+ frames) and buffer donation, it should feel like playing locally at up to 300ms ping"). I did not sign in or use chat.
- [video] [Zain plays Phillip the AI in first to 5 wins](https://www.youtube.com/watch?v=c8nRFAGvr2c) (BME, 21:47, 87K views) — Opened it and seeked to 60, 300 and 600 s; headless frames stayed on the Slippi Direct Mode character-select screen ("User Zain", Marth) with Zain's facecam. Recording of a netplay set between Zain and Phillip; the README also lists Amsa, Cody, Moky and Aklo sets and a [YouTube channel](https://www.youtube.com/channel/UCzpDWSOtWpDaNPC91dqmPQg). Play-mode evidence (recording): none beyond the netplay setup visible in frames.
- Note: the live stream overlay shows "Delay: 20f" and the README says "18+ frames", higher than the 12-15 frame delay in this file's Method row.

Visited 10 November 2026 in a headless browser.

Related: [libmelee / Slippi](../environments/libmelee-slippi.md)
