---
layout: post
title: "Reading LoopArena's Cost Column"
date: 2026-09-01
categories: [reflection]
tags: [agents, evaluation, cost, orchestration]
---

[LoopArena](https://arxiv.org/abs/2608.28281) (arXiv 2608.28281 — Yi Wang et al., DreamX/Alibaba, BUPT, UNSW, Data61 CSIRO; posted 28 August, sitting at 80 upvotes on [HF daily papers](https://huggingface.co/papers/2608.28281)) inverts the usual coding-agent setup. It freezes the Worker — same coding agent, same tools, same 27 repository tasks (11 from SCBench, 16 from BeyondSWE) — and evaluates the model *directing* it. The Controller reads a structured summary each round and says what happens next, or says stop. Five Controllers, three settings: Type I is a single control decision with no execution, Type II runs the loop over a task slice, Type III runs the full task from its original state. The main results table is short enough to just print, so here it is:

```
                          Type I      Type II            Type III
Method                    Contract%   SSR%   $/run       SSR%   $/run
No control                    —      39.51    1.04      18.52    2.01
Fixed control                 —      46.91    1.08      18.52    5.58
Qwen3.7-Plus                72.22    48.15    4.30      23.46    6.89
DeepSeek-V4-Flash-0731      77.78    45.68    2.10      19.75   10.24
GLM 5.2                     74.44    37.04    1.63      16.05    4.86
GPT-5.5                     87.78    51.85    5.00      24.69   18.84
Claude Opus 4.8             76.67    48.15    5.87      20.99   16.82
```

**Two of the five Controllers are worse than no Controller.** GLM 5.2 lands at 16.05% full-task Strict Success Rate against the unguided baseline's 18.52%, and bills $4.86/run against $2.01. On the slice it is 37.04% versus 39.51% unguided. DeepSeek-V4-Flash clears the baseline by 1.23 points while costing 5.1×. A supervisory layer with negative expected value is not a failure mode most orchestration diagrams have a box for. And **the dumbest possible Controller wins the short horizon and evaporates on the long one**: "fixed control" merely restates the task objective at every control point, which is worth +7.4 points on Type II (39.51 → 46.91) — enough to beat DeepSeek and crush GLM — and then scores 18.52% on Type III, identical to no control to the digit, at 2.8× the cost. Any benchmark that only measures bounded slices will rank goal-restatement as a real technique.

**Cost per success reorders the leaderboard.** These tasks carry executable evaluators, so failure is detectable and retry is genuinely on the table. Divide $/run by SSR: unguided execution needs 5.40 attempts and $10.85 per completed task. Qwen3.7-Plus needs 4.26 attempts, $29.37. GPT-5.5 — the SSR winner — needs 4.05 attempts and **$76.31**. Claude Opus 4.8 is $80.13. The best Controller buys 6.17 points of absolute success rate at roughly 7× the cost per delivered task, which means "spend nothing on control and run it five times" dominates every Controller on this benchmark on price, and the gap is not close. A related ordering problem sits one column to the left: DeepSeek is 2nd on per-decision Contract Accuracy (77.78%) and 4th on full-task SSR, while Qwen is *last* on Contract Accuracy (72.22%) and 2nd on SSR. Type I is not junk — the best deterministic shortcut the authors could build (uniform choice, action-only, candidate length, lexical overlap) reaches 31.11% against 72–88% for real models, at a 0% invalid-response rate. It measures something real. It just is not the thing that gets a repository into a passing state.

The result worth stealing is the compression one, with a caveat attached. Type II reproduces Type III's Controller ordering at ρ = 0.9747 for 64.4% less inference spend — no strictly-ordered pair reverses, one pair ties. That is the benchmark-compression trick applied to agent loops, and it is the practical gift here: rank controllers on slices, and only pay for full runs at the end. The caveat is n = 5. Ten pairs, nine strict, one tie; ρ = 0.9747 on five models is one odd new entrant away from 0.7. Which leads back to the arithmetic. Routing is usually framed as picking the model that *answers*. LoopArena prices the other routing decision — picking the model that decides what happens next — and the honest read of its own table is that across 27 repository tasks, that decision was worth less than its price, and sometimes less than zero. If a control layer is going to earn $16.83/run over baseline, the benchmark that proves it has to be full-horizon, and the metric has to be cost per completed task rather than success rate.
