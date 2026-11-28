---
layout: post
title: "Vernier, Stage by Stage"
date: 2026-11-28
categories: [reflection]
tags: [evaluation, leaderboards, statistics, forecasting, process]
---

A leaderboard shows an order, but it rarely says how small a gap its own data could detect. A new paper, [*Resolution Analysis of Time-Series Forecasting Leaderboards* (arXiv 2611.31619)](https://huggingface.co/papers/2611.31619), ships a tool, [Vernier](https://github.com/therealram18/vernier), that computes exactly that number from the per-dataset score files boards already publish. What's worth following is what each stage of the pipeline does to a ranking. **Stage 1** picks the unit of evidence: each *dataset* is one independent cluster, not each series or forecast window, so a board showing thousands of numbers drawn from 28 datasets has roughly 28 independent observations. Everything downstream rests on that choice. **Stage 2** estimates the variance of every pairwise score difference with cluster-robust (CR2) standard errors and Satterthwaite degrees of freedom, both small-sample corrections; in simulation at 28 datasets the false-alarm rate came out at 5.2% against a nominal 5%. **Stage 3** converts that into a minimum detectable effect: resolution = (t₀.₉₇₅,ν + t₀.₈₀,ν) × SE, the gap a 5%-level test would catch with 80% power.

**Stage 4** lays the resolution next to the gaps the board actually displays, and this is where the headline order comes apart:

| Board | Resolution ÷ median neighbor gap | Top-10 neighbor pairs separated |
|---|---|---|
| GIFT-Eval | 7.5 | 1 of 9 |
| fev-bench | 3.6 | 0 of 9 |
| Chronos Bench II | 19 | 0 of 9 |
| TIME | 11 | 0 of 9 |
| BOOM | 0.63 | 9 of 9 |

Only BOOM, with 2,554 series, resolves its own top ten. On GIFT-Eval the resolution is about 6.8 ranks while neighbors sit 0.91 apart, so the top ten is roughly two distinguishable tiers drawn as ten rungs. **Stage 5** re-checks with tests that lean on fewer assumptions (a wild cluster bootstrap and exact sign-flip tests, Holm-corrected across all pairs) and reports a **leading tier**: every entry the data cannot separate from the leader.

The last two stages are the ones I'd steal. **Stage 6**, `vernier replay`, walks the board's git history update by update. Across 226 updates on four boards, mean-rank scoring rules, which grade each entry against whoever else is in the pool, reversed 43 top-ten pairs in 31 updates *where neither entry had been rerun*; GIFT-Eval alone accounts for 20. A geometric-mean rule, which doesn't depend on the pool, reversed none. In the authors' phrase, "below the resolution, a displayed order also records who else submitted." **Stage 7** lists what the board never recorded. Nobody logs how much history each model was fed, and cutting it to 512 steps raised error 15.3% for TimesFM-2.5 and Toto, 6.2% for Moirai-2.0, and a non-significant 2.7% for Chronos-Bolt, with error up in 64 of 70 configurations. A one-rank gap can simply be a settings gap.

Every stage ports to pairwise-vote arenas, and the hardest one to port is the first. On [arena.ai's board](https://arena.ai/leaderboard) this week the Agent Index reads Fable 5.2 at 1449, Opus 5.5 at 1342 and Gemini 4 Neon at 1331. The 107-point gap at the top is almost certainly real. Whether the 11 points below it are depends on what counts as a cluster: if votes clump by prompt template, by voter, or by post-launch traffic bursts, the effective sample shrinks and the resolution widens. Bradley-Terry ratings are also fit across the whole pool, so an arena carries Stage 6's exposure too: a newcomer with lopsided matchups can move the ratings of models it never played. Per-model intervals weren't visible on the page, so that 11-point call is a hypothesis, not a measurement. Vernier's report format is ready to copy, though: name the cluster unit, print the resolution in rating points beside the median neighbor gap, make the leading tier the headline, and replay the history to count reversals between pairs that were never rerun. A count near zero means the board resolves what it shows. A count like GIFT-Eval's 20 means the ranks are partly a record of who else turned up. And for anyone choosing a model off such a board, the practical upshot is to pick within the leading tier on cost or latency, not on rank.
