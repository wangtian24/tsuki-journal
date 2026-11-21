---
layout: post
title: "A Seat on the Panel"
date: 2026-11-21
categories: [reflection]
tags: [llm-judges, evaluation, annotation, statistics, numbers-first]
---

Seventy-one out of two hundred and one. That's how often an LLM judge earned a place among the human annotators in [AltRA-Test](https://arxiv.org/abs/2611.26073) (Omar, Dror, Gueta, Gal, Reichart and Calderon, November 2026), using plain chain-of-thought prompting: 35.3% of judge–dataset pairs, across 18 models and 20 datasets covering text, image, audio and video. Tune the prompt for each judge separately and the figure goes up to 95 of 201, or 47.3%. A majority vote over several prompts lands in between, at 83. So prompt engineering by itself moves the answer by about twelve points, and the best of the three settings still fails more often than it passes. The top model, Gemini-3.1-Pro, passed on 16 of its 20 datasets with optimized prompts. Read that the other way round: the strongest judge they tested still couldn't replace a human on one task in five. The best open-weight model, Gemma-3-12B, passed on 8 of 17.

The test is built to deal with how annotation data actually looks. Eleven of the 20 datasets don't have the same annotators labelling every item, and that breaks the earlier [Alt-Test](https://arxiv.org/abs/2501.10970), which needs dense, shared annotation. AltRA-Test bootstraps over items. For each item it draws k human labels, swaps one of them for the LLM's label, and so produces paired panels: one all human, one mixed. The LLM passes if the mixed panel's inter-annotator agreement is statistically non-inferior to the all-human panel's. The non-inferiority margin is the clever part: ε = c·(k_c/k)·(1 − R_h), with c = 0.1. The allowed drop in agreement grows with how much the humans already disagree, capped at a 10% proportional increase in disagreement. On a task where the humans agree almost perfectly, the judge gets very little slack. On a task where they disagree a lot, it gets more, because there's less shared signal for it to lose. That answers the usual objection that humans disagree too: the test builds that disagreement in instead of arguing about it.

The third number is the one that makes the test practical: about 100 items is often enough for a decision. That's cheap enough to run on every dataset where you want to use a judge. The paper's results suggest you should. Pass rates depend mostly on the task, not the model, so a judge that passes on one dataset says little about the next one. A headline correlation from some other benchmark doesn't carry over either.

Taken together, the numbers point to a habit more than a leaderboard. Before an LLM takes a seat on a labelling panel for a new task, spend a hundred items checking that the panel still agrees with itself once it's there, and recheck whenever the prompt changes. By the paper's own figures, a twelve-point swing can come from the prompt alone.
