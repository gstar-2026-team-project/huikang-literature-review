# DQN / Atari line

The DQN / Atari line of RL agents acts with frameskip 4 (15 Hz) and gets inference time for free.

![DQN playing Atari Breakout](../assets/gifs/sol-dqn-atari.gif)

*Recording of DQN playing Atari Breakout late in training, clearing a tunnel at the left edge of the wall as the score climbs from 042 to 064; a 5-second excerpt from the official video, cropped to the playfield. Source: [Google DeepMind, "DQN Breakout" video](https://www.youtube.com/watch?v=TmPfTpjtdgg).*

| | |
|---|---|
| Year | Dec 2013 |
| Links | [ALE docs](https://ale.farama.org/environments/) |
| Demo | ["DQN Breakout" video](https://www.youtube.com/watch?v=TmPfTpjtdgg) (Google DeepMind, 1:12), embedded in the [Google Research blog post](https://research.google/blog/from-pixels-to-actions-human-level-control-through-deep-reinforcement-learning/): an official recording of DQN playing Breakout after 100, 200, 400 and 600 training episodes, ending with the tunnel strategy. A recording, not live or human-playable. |
| Category | RL and decision model |
| Method | frameskip 4 (15 Hz); inference time free |
| Evaluated on | Atari |
| Evaluation play mode | paused-live |
| Basis | paper: Nature 2015 Methods "the agent sees and selects actions on every kth frame"; human tester "not allowed to pause" |

## Demo

- [official video] ["DQN Breakout" on YouTube](https://www.youtube.com/watch?v=TmPfTpjtdgg), also embedded in the [Google Research blog post](https://research.google/blog/from-pixels-to-actions-human-level-control-through-deep-reinforcement-learning/) (25 February 2015, captioned "Video courtesy of Atari Inc. and Mnih et al.") — played the 1:12 video and seeked to 0:10, 0:31, 0:53 and 1:09. Description: "This video illustrates the improvement in the performance of DQN over training (i.e. after 100, 200, 400 and 600 episodes). After 600 episodes DQN finds and exploits the optimal strategy in this game, which is to make a tunnel around the side". Frames show Atari Breakout with the on-screen score at 003 near the start and 099 near the end. Play-mode evidence (recording): an edited screen capture of the emulator; it does not show the frameskip or the agent's inference timing, so it neither confirms nor contradicts the paused-live label.

Visited 10 November 2026 in a headless browser.

Related: [ALE / Atari](../environments/ale-atari.md)
