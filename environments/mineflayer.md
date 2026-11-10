# Mineflayer

Mineflayer is a Minecraft bot API whose bot physics run on a 50 ms wall-clock interval against a server that runs in real time.

| | |
|---|---|
| Year | 2015- |
| Links | [repo](https://github.com/PrismarineJS/mineflayer) |
| Demo | [prismarine-viewer](https://prismarinejs.github.io/prismarine-viewer/): static WebGL world snapshots per Minecraft version, with a draggable camera. No bot activity shown. Human-playable: no. |
| Play mode | realtime-live at env level; LLM agents on it mostly scripted |
| Clock | bot physics on a 50 ms wall-clock interval (20 TPS) |
| Observation | structured state |
| Action | high-level API |
| Players | 1+ |
| Horizon | any |
| Human reference | n/a |
| Open source | MIT |
| Convertible to realtime-live | restrict action space |
| Basis | code: `lib/plugins/physics.js:14` `PHYSICS_INTERVAL_MS = 50`, `:549` `setInterval(doPhysics, ...)` |

## Details

- **Mineflayer**: the server runs in real time, but LLM agents on it mostly emit programs (scripted).

## Demo

- [project-page] [prismarine-viewer demo](https://prismarinejs.github.io/prismarine-viewer/) — Loaded the page (a 600x600 iframe of prismarine-viewer/standalone/) and dragged to rotate the camera. It shows static WebGL renders of Minecraft worlds, one per game version (1.21.4 down to 1.8.8), with terrain and a wooden structure; the camera responds to dragging. Play-mode evidence: world snapshots only, no Mineflayer bot or player, no clock, not playable.

Visited 10 November 2026 in a headless browser.

Related: [Voyager](voyager.md); [Odyssey](odyssey.md); [MINDcraft](mindcraft.md); [Orak](orak.md); [Parallelized Planning-Acting](../solutions/parallelized-planning-acting.md)
