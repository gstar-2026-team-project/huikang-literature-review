# Real-Time Deadlines (UPenn negotiation)

In the UPenn Real-Time Deadlines setting two agents negotiate a contract under a 240-360 s deadline, with each utterance costing time in proportion to its word count.

| | |
|---|---|
| Year | 2026 |
| Authors / org | Sehgal, Guntuku, Ungar |
| Links | [arXiv 2601.13206](https://arxiv.org/abs/2601.13206) |
| Demo | None found (searched: arXiv 2601.13206 abstract page (no project page or video listed); code repo github.com/sehgal-neil/llm-temporal-awareness (README is CLI replication instructions only, no homepage, no media); web search for the paper title plus demo/GitHub) |
| Play mode | realtime-live (weak: output-length clock) |
| Clock | each utterance costs word count at 150 words/min; reasoning free |
| Basis | paper §3: "each utterance incurs a delay proportional to word count, calibrated at 150 words per minute ... deducted from the remaining time budget" |

## Details

- Details for the UPenn paper (Sehgal, Guntuku, Ungar): two agents negotiate a contract under a 240-360 s deadline. Deal closure for GPT-5.1-chat-latest: 4% told the deadline once, 32% with remaining time shown each turn, 98-100% under a turn limit instead. The failure is tracking elapsed time, not negotiating. Pairwise, objective payoffs, cheap to replicate.
- Later, for pairwise work (from the shortlist): the UPenn deadline negotiation.

## Demo

- None found (searched: arXiv 2601.13206 abstract page (no project page or video listed); code repo github.com/sehgal-neil/llm-temporal-awareness (README is CLI replication instructions only, no homepage, no media); web search for the paper title plus demo/GitHub).

Searched 10 November 2026; no demo found.

Related: [GPTNT](gptnt.md); [NegotiationArena](negotiationarena.md); [AucArena](aucarena.md); [Deal or No Deal](deal-or-no-deal.md); [AmongAgents](amongagents.md)
