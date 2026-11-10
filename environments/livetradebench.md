# LiveTradeBench

LiveTradeBench is a live-data trading benchmark with one decision per trading day.

| | |
|---|---|
| Year | 2025 |
| Links | [arXiv 2511.03628](https://arxiv.org/abs/2511.03628) |
| Demo | [trade-bench.live](https://trade-bench.live) (repo homepage): live leaderboard site (Stock, Polymarket, later BitMEX) charting each LLM agent's portfolio value and rankings, updated per trading cycle. Not a game view or replay; not human-playable. Site unreachable (connection timeout) on 10 Nov 2026; seen only via Wayback Machine snapshots, whose leaderboard data was not archived. |
| Play mode | paused-live (live data, daily) |
| Clock | one decision per trading day |
| Does model latency matter? | No |
| Basis | paper §4: "For each trading day ... we fix the portfolio position" |

## Details

- The live arenas are slow-cadence, noisy and unrepeatable; they are a poor fit for first environments.

## Demo

- [live-leaderboard] [trade-bench.live](https://trade-bench.live) — Found as the homepage of the repo [ulab-uiuc/live-trade-bench](https://github.com/ulab-uiuc/live-trade-bench) (description "Live evaluation of trading agents"; the arXiv page lists no project link). On 10 November 2026 the live site did not load (connection to 13.58.96.53 timed out in both the browser and curl). I opened Wayback Machine snapshots instead. The 9 November 2025 snapshot shows "Live Trading Benchmark", "Real-time leaderboard for LLM-powered portfolio management", and Stock and Polymarket tables (RANK, MODEL, RETURN, #TRADES) with "Next update (ET): 11/17/2025 09:30:00" (stock) and "Next update (ET): 11/14/2025 19:32:54" (Polymarket). The 4 April 2026 snapshot adds a BitMEX tab, a Chart/Rankings toggle with "30 Days"/"ALL", and News and Social Media pages. The page loads its data from a backend (`/api/models/`, `/api/models/history`, `/api/schedule/next-price-update`, `/api/news/stock`); the archive returned 404 for `/api/models/`, so the tables and the portfolio-value chart were empty. Play-mode evidence: scheduled per-cycle updates (stock at market open, 09:30 ET) are consistent with one decision per trading day; there is no replay viewer, game view or human play.

Visited 10 November 2026 in a headless browser.

Related: [Alpha Arena (Nof1)](alpha-arena.md); [Agent Market Arena](agent-market-arena.md)
