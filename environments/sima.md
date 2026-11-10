# SIMA evaluation environments

SIMA's evaluation environments are commercial games that "do not stop and wait while the agent computes".

| | |
|---|---|
| Year | 2024 |
| Authors / org | DeepMind |
| Links | [arXiv 2404.10179](https://arxiv.org/abs/2404.10179) |
| Demo | [SIMA blog](https://deepmind.google/discover/blog/sima-generalist-ai-agent-for-3d-virtual-environments/): edited recorded gameplay clips from 9 partner games and research environments, with no latency or tick readout. No live model, replay viewer or playable demo; human-playable: no. |
| Play mode | realtime-live |
| Horizon | tasks of about 10 seconds |
| Open source | not released |

## Details

- **SIMA** evaluation environments (DeepMind, 2024), [arXiv 2404.10179](https://arxiv.org/abs/2404.10179): commercial games that "do not stop and wait while the agent computes"; tasks of about 10 seconds; not released. Covered in [SIMA](../solutions/sima.md) on the solutions side.

## Demo

- [video] [SIMA blog post](https://deepmind.google/discover/blog/sima-generalist-ai-agent-for-3d-virtual-environments/) — Scrolled the March 2024 post and played/seeked its 2 embedded videos: a grid of short recorded gameplay clips from the 9 partner games (Valheim, Goat Simulator 3, No Man's Sky, Teardown and others) and research environments (Playhouse, Construction Lab). The text says SIMA takes screen pixels and a language instruction, outputs keyboard and mouse actions, and is evaluated on about 600 basic skills of roughly 10 s each. Play-mode evidence (recording): edited footage with no tick counter, latency readout or live controls; the page does not show whether the game was paused during inference.

Visited 10 November 2026 in a headless browser.

Related: [SIMA](../solutions/sima.md); [SIMA 2](../solutions/sima-2.md); [Lumine evaluation settings](lumine.md)
