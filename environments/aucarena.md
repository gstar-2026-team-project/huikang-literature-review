# AucArena

AucArena is a round-based auction in which bidders act per auction round.

| | |
|---|---|
| Year | 2023 |
| Links | [arXiv 2310.05746](https://arxiv.org/abs/2310.05746) |
| Demo | [project page](https://auction-arena.github.io) with static figures, plus [HF Space](https://huggingface.co/spaces/jiangjiechen/Auction-Arena-Demo), a Gradio auction where LLM and human bidders play with live API calls (bring your own key). It is turn-based and waits for every bidder with no timeout. The Space currently shows a runtime error (launch timed out). Human-playable: designed to be, but not reachable now. |
| Play mode | paused-live, round-based auction |
| Clock | rounds |
| Basis | paper §3: bidders act per auction round |

## Details

- All the turn-based arenas convert trivially by adding a wall-clock deadline per message, as the UPenn paper does.

## Demo

- [project-page] [AucArena project page](https://auction-arena.github.io) — Loaded and scrolled the Wowchemy page and dumped its media, links and network requests. It has the abstract, a prose summary, static result figures (error.png, correlation.png, adaptive.png, heatmap.png, human.png and others) and links to GitHub, the HF Space and arXiv 2310.05746; no video, iframe, canvas or replay viewer. Play-mode evidence: no gameplay on the page itself; it links the 'live auction arena' Space where people can "pit your strategic auctioning skills against AI".
- [dead-or-unreachable] [Auction-Arena-Demo HF Space](https://huggingface.co/spaces/jiangjiechen/Auction-Arena-Demo) — Opened the Space and waited 15 s; it shows "Runtime error: Launch timed out, workload was not healthy after 30 min" (Gradio 3.47.1, last commit 2023-10-10), so nothing could be played. From its source (app.py, src/human_bidder.py, auction_workflow.py) it is a Gradio app where the user brings their own OpenAI or Anthropic key, sets up LLM bidders (GPT-3.5/4, claude-instant-1.2, claude-2.0 and others) or human bidders, and presses 'Start Bidding' to stream chat and bidding logs with budget, profit, token and belief-error monitors. Play-mode evidence (code read, not run): run_auction() is a turn-based generator that asks every bidder per round, HumanBidder blocks with `while self.semaphore <= 0: time.sleep(1)` with no timeout, and LLM bidders are queried synchronously, so the game waits for every bidder and there is no environment clock.

Visited 10 November 2026 in a headless browser.

Related: [Real-Time Deadlines (UPenn negotiation)](real-time-deadlines-negotiation.md)
