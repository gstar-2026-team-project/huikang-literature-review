# pi0

pi0 is a robot policy that predicts 50 Hz action chunks with 73-86 ms inference and re-infers every 0.5 s.

| | |
|---|---|
| Year | 2024 |
| Links | [arXiv 2410.24164](https://arxiv.org/abs/2410.24164) |
| Demo | [pi0 blog](https://www.pi.website/blog/pi0): recorded videos of real robots acting autonomously ('uncut, from a single policy operating fully autonomously'; 1x/2x speed in the file names). The later RTC post says pi0 ran synchronously, pausing between chunks during inference. No interactive or live demo; human-playable: no. |
| Category | RL and decision model |
| Method | 50 Hz chunks, 73-86 ms inference, re-infer every 0.5 s |
| Evaluated on | robots |
| Evaluation play mode | realtime-live (real robot) |
| Basis | paper App. D: inference every 0.5 s (50 Hz robots) or 0.8 s (20 Hz); real robots |

## Details

- **Action chunking** (ACT, pi0): predict many actions per inference and execute open-loop.

## Demo

- [video] [pi0 blog post](https://physicalintelligence.company/blog/pi0) — Loaded the page (redirects to https://www.pi.website/blog/pi0), listed the media and seeked the first two videos to 1 s and 5 s; nothing is interactive and every clip is a pre-recorded MP4 from website.pi-asset.com. It has a 3:36 hero video (PhysicalIntelligence_2min_v2_out.mp4), 6 s clips of each robot (UR5e, Franka, bimanual Trossen and ARX, mobile Trossen and Fibocom) and task clips (laundry, box building, bussing, dryer unloading). Play-mode evidence (recording): file names give playback speed (lowres_processed1xspeed_build_box_3.mp4, processed2xspeed_apartment_laundry_10min.mp4, lowres_processed2xspeed_bussing_2.mp4) and a caption says "The video is uncut, from a single policy operating fully autonomously"; the real world never stops, though the later RTC post says pi0 ran synchronously, pausing between chunks while inference ran.

Visited 10 November 2026 in a headless browser.

Related: [ACT](act.md); [Real-Time Chunking](real-time-chunking.md)
