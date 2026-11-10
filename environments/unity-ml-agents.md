# Unity ML-Agents

Unity ML-Agents is the route for building new realtime environments; its step API is synchronous.

| | |
|---|---|
| Year | 2017 |
| Links | [repo](https://github.com/Unity-Technologies/ml-agents) |
| Demo | [SoccerTwos Space](https://huggingface.co/spaces/unity/ML-Agents-SoccerTwos) (official `unity` Hugging Face Space; sibling Spaces for Walker, Worm, PushBlock, Pyramids, Huggy): a Unity WebGL build where you pick two trained ONNX policies from the Hub and watch them play 2v2 soccer live in the browser. RL policies, not LLMs; watch-only, not human-playable. |
| Play mode | paused-live |
| Clock | DecisionPeriod, time_scale |
| Observation | vector, camera |
| Action | continuous/discrete |
| Players | any |
| Horizon | custom |
| Human reference | n/a |
| Open source | Apache-2.0 |
| Convertible to realtime-live | high for own builds |
| Basis | code: `com.unity.ml-agents/Runtime/Communicator/RpcCommunicator.cs` `DecideBatch` -> synchronous gRPC `Exchange` (Unity waits for the Python reply) |

## Details

- **Unity ML-Agents**: the route for building new realtime environments; ROAR and TowerMind are built on it.

## Demo

- [live-demo] [unity/ML-Agents-SoccerTwos](https://huggingface.co/spaces/unity/ML-Agents-SoccerTwos) — Opened the Space (Unity WebGL build, engine "2021.3.14f1", loaded from `Build/ML-Agents-SoccerTwos.wasm.unityweb`). The menu asks "Step 1: Type Blue Team username (case sensitive!) to find your models and click on the search button" and "Step 2: Choose the model repository"; I typed the public placeholder user ThomasSimonini for both teams (request `api/models?author=ThomasSimonini&filter=ML-Agents-SoccerTwos`), picked "ThomasSimonini/ML-Agents-SoccerTwos-Good" (blue) vs "...-Bad" (purple), and pressed "Kick-off". The page fetched `SoccerTwos.onnx` from each model repo (console "Loaded") and the four cube agents then played soccer in the browser for about 30 s (score stayed 0-0; ball moved from the blue goal area to the purple one between screenshots). Play-mode evidence: live, in-browser ONNX inference of small RL policies inside the running Unity simulation, no remote model calls and no LLM; watch-only (no human control). It shows Unity scenes running at their own frame rate with policies acting every decision step, not the paused gRPC Python loop described in Basis.
- [static images] [Example Learning Environments docs](https://unity-technologies.github.io/ml-agents/Learning-Environment-Examples/) — only still PNGs (balance.png, soccer.png, etc.) of the 17 example scenes; no video. The homepage field (unity.com/products/machine-learning-agents) returned "Access Denied" to the headless browser. Other official Spaces exist (unity/ML-Agents-Walker, -Worm, -PushBlock, -Pyramids, -Huggy) but were not opened.

Visited 10 November 2026 in a headless browser.

Related: [ROAR](roar.md); [TowerMind](towermind.md)
