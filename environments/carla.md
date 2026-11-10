# CARLA

CARLA is a driving simulator whose default mode is asynchronous and whose synchronous mode waits for the client.

| | |
|---|---|
| Year | 2017 |
| Links | [docs](https://carla.readthedocs.io/en/latest/adv_synchrony_timestep/) |
| Demo | [carla.org homepage video](https://carla.org/) ([YouTube YLh07d-YPSI](https://www.youtube.com/watch?v=YLh07d-YPSI)): official release video, "CARLA 0.9.16 Release" (2:42), showing the simulator, its maps and sensor views (camera, segmentation, LIDAR). A recording of the simulator, not of an LLM or model playing; no replay viewer or browser-playable build. |
| Play mode | realtime-live (default async) + paused-live (sync) |
| Clock | server as fast as possible / client tick |
| Observation | cameras, LIDAR |
| Action | steer/throttle |
| Players | 1 |
| Horizon | long |
| Human reference | easy |
| Open source | open, heavy |
| Convertible to realtime-live | n/a |
| Basis | docs `Docs/core_synchrony.md`: "By default, CARLA runs in asynchronous mode. The server runs the simulation as fast as possible, without waiting for the client" |

## Details

- **CARLA**: default mode is asynchronous ("as fast as possible", not locked to wall clock); synchronous mode waits for the client.

## Demo

- [official-video] [carla.org homepage, "Video" section](https://carla.org/) embedding [YouTube YLh07d-YPSI](https://www.youtube.com/watch?v=YLh07d-YPSI) — Opened the homepage (repo homepage field `http://carla.org`), clicked play on the embedded player and seeked to about 1:03 of 2:42 (player readout "1:03 / 2:42"; duration 161.3 s). Title "CARLA 0.9.16 Release" by "CARLA Simulator". At 1:03 it shows a multi-view layout: a semantic-segmentation camera view, an RGB chase-camera view of a car and a large LIDAR point-cloud view. Play-mode evidence: a pre-recorded promotional video of the simulator and its sensors; it does not show an agent or LLM driving against a clock and says nothing about async versus sync stepping. Not human-playable in the browser (CARLA needs a local Unreal Engine install). The homepage has no other video, iframe or canvas besides a GitHub star button.

Visited 10 November 2026 in a headless browser.

Related: [Bench2Drive](bench2drive.md); [Think at 5 Hz, Act at 20 Hz](../solutions/think-at-5hz-act-at-20hz.md)
