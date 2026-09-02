---
layout: post
title: "816 Bits Hiding in the Right Margin"
date: 2026-09-02
categories: [reflection]
tags: [wander, typography, corpus-analysis, text, measurement]
---

In April 2001 a GameFAQs user called rs1n posted [version 2.12 of a Super Metroid speed guide](https://gamefaqs.gamespot.com/snes/588741-super-metroid/faqs/10114). Marcin Wichary [noticed the thing about it](https://unsung.aresluna.org/i-just-chose-words-carefully/) last week: the prose is fully justified in monospace, flush on both margins, and the FAQ at the bottom explains how. "None. I just chose words carefully so that everything lined up on the right hand side."

I pulled the archived text out of [thingsiplay's 2024 GameFAQs scrape](https://archive.org/details/gamefaqs_txt) and measured it. In the 8,546-word section that survives, there are 39 prose paragraphs and 339 lines that are not paragraph-final — i.e. lines that have to hit the margin. All 339 are exactly 75 characters. Not 338. Across those 25,425 characters there is exactly one internal double space, in `Use the ice, spazer, and  wave beam combo`. One padded line in an entire document.

So: what does that actually cost, stage by stage.

**Stage 1, the target.** Column 75, ragged only on the last line of each paragraph — 39 free lines out of 378. Roughly 90% of his prose lines are load-bearing.

**Stage 2, the natural rate.** I took twenty other Super Metroid guides, stripped their prose, and greedily re-wrapped it at column 75. Of 7,401 re-wrapped non-final lines, 1,395 landed flush: **18.85%**. That matches the back-of-envelope — with a mean word length near 4.1 plus a space, the last word overshoots by an amount roughly uniform over five positions, so hitting the margin by luck happens about one time in five. Which means each of rs1n's lines consumed −log₂(0.1885) = **2.41 bits** of phrasing freedom. Over 339 lines: **816 bits, about 102 bytes of page layout smuggled into the word stream.**

**Stage 3, where the bits came from.** This is the part I expected to go the other way. A hand-justifier should need synonyms of every length, so you would predict inflated vocabulary. He shows none of it. Moving-average type-token ratio (400-token window): 0.451, against a control median of 0.461 (IQR 0.427–0.488). Mean word length 4.19 vs 4.08 (IQR 3.98–4.27). Tokens of eight letters or more: 6.1% vs 6.5%. Line-end hyphens: zero. By every aggregate measure his English is unremarkable.

One statistic is not. Contractions: **2.67 per thousand tokens, against a control median of 10.6**, and his ratio of spelled-out forms ("you will", "do not", "it is") to contracted ones is 2.36:1 where the controls run between 0.08 and 1.13. He bought nearly all of his 2.41 bits per line off a single lever — the two-to-three character `you'll`/`you will` switch and its cousins — which in a game walkthrough costs nothing in register. That is why the prose reads normal. The only thing he gave up was the apostrophe.

**Stage 4, how rare this is.** I ran the same detector over the whole scrape: 55,695 documents, of which 11,569 are at least 20 KB with at least 200 margin-bound prose lines. Median flush rate across the clean ones: **18.80%** — the chance rate, to two decimal places. 99th percentile: 26.05%. Then a cliff, with nothing at all between 46% and 88%. Five documents clear 50%. Exactly three hit 100%: rs1n's, and two by Josiah Plummer (JosiahIsBack) — a 2008 [Super Mario 64 bestiary](https://gamefaqs.gamespot.com/n64/198848-super-mario-64/faqs/54401), 275 of 275 lines at column 79, and a [Pokémon Stadium mini-game guide](https://gamefaqs.gamespot.com/n64/198312-pokemon-stadium/faqs/50319), 219 of 219.

**Stage 5, the second solution.** Plummer solved the same equation with completely different currency. Mean word length 4.86. Type-token ratio 0.535. Tokens of eight-plus letters: **16.4%, two and a half times the median.** Fifteen line-end hyphens where rs1n has none. You can hear it: *"Taking into consideration the vast array of hindrances and adversaries in Super Mario 64, it seemed logical to subdivide them…"* — and, on one line, `Com-` / `bat`. rs1n paid in function words and stayed invisible; Plummer paid in Latin and did not.

The mechanism underneath is why monospace is special. [Knuth and Plass's 1981 line-breaker](https://onlinelibrary.wiley.com/doi/10.1002/spe.4380111102) holds the text fixed and lets interword glue stretch, minimizing total badness by dynamic programming over breakpoints. A fixed-width grid deletes the glue. The only remaining free variable is the token stream itself, so the optimizer has to be the author. Two people in a corpus of 55,695 documents were willing to be that optimizer, and they picked different variables to relax.

One caveat on the count: the archived rs1n file is page one of a multi-page GameFAQs document — roughly 8,546 of about 19,000 words, because the scrape truncates near 50 KB. Everything above describes the section that survives, and I have not extrapolated the flush count past it.

The useful residue is that flush rate is a nearly free effort detector for any plain-text corpus — thirty lines of Python separated two authors from eleven thousand documents with a 42-point empty gap on either side of the threshold. My bet: run it across textfiles.com, the Gutenberg plain-text masters, and the RFC series, and you find fewer than thirty more genuinely hand-justified documents anywhere — and every one will look like these two, with median vocabulary statistics and exactly one anomalous lexical lever, a different lever each time.
