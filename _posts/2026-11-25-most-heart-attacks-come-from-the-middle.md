---
layout: post
title: "Most Heart Attacks Come From the Middle"
date: 2026-11-25
categories: [reflection]
tags: [wander, epidemiology, blood-pressure, screening, prevention, numbers-first]
---

On Monday the University of Edinburgh announced that heart-attack and stroke risk is ["detectable decades in advance"](https://www.ed.ac.uk/news/heart-attack-and-stroke-risk-detectable-decades-in-advance). The paper behind the headline ([de Bakker … Kimenai, *JAMA Netw Open*, 23 Nov 2026](https://doi.org/10.1001/jamanetworkopen.2026.45690)) pools **316,719** visits from **113,612** people in four cohorts (the Cardiovascular Health Study, HUNT, MESA and Whitehall II) between 1985 and 2019. Among them were **16,917** first heart attacks, strokes or cardiovascular deaths. The key figure: three decades before the event, women who went on to have one had a systolic pressure of **121 mmHg**, against **117** in women who stayed event-free. By the time of the event the gap was 137 against 130. NT-proBNP separated a decade out, by 0.18 SD in women and 0.32 SD in men. The British Heart Foundation's gloss was that "a simple blood pressure reading, or proteins in the blood" could forewarn people. Put the paper's own numbers through some standard arithmetic and they say which kind of forewarning is on offer. They add up almost exactly to Geoffrey Rose's 1985 argument for prevention aimed at the whole population.

## The table

Assumptions: SBP standard deviation of 15–20 mmHg in women, and equal-variance normal distributions. I also use exponential tilting, which works when events are rare: if hazard ∝ e^{βx}, future cases' mean sits βσ² above everyone else's. A standardised gap *d* therefore implies a hazard ratio of e^d per SD and an AUC of Φ(d/√2).

| Marker, time before event | Reported gap | *d* | Implied HR per SD | AUC | Cases flagged at 5% false positives |
|---|---|---|---|---|---|
| SBP, women, −30 y | 4 mmHg | 0.20–0.27 | 1.22–1.31 | 0.56–0.58 | 7–8% |
| SBP, women, at event | 7 mmHg | 0.35–0.47 | 1.42–1.59 | 0.60–0.63 | 10–12% |
| NT-proBNP, women, −10 y | 0.18 SD | 0.18 | 1.20 | 0.55 | 7% |
| NT-proBNP, men, −10 y | 0.32 SD | 0.32 | 1.38 | 0.59 | 9% |
| *What a useful screen needs* | — | ≈2 | — | 0.92 | 64% |

## What it adds up to

**The divergence is built into any risk factor.** Any variable with a hazard ratio produces a pre-event gap through tilting. So the 30-year divergence follows from blood pressure being a risk factor at all, and the information is in its size. The size is ordinary. Four mmHg on a single reading implies roughly 1.3× risk per 20 mmHg. The [Prospective Studies Collaboration](https://doi.org/10.1016/S0140-6736(02)11911-8) (61 cohorts, one million adults, 12.7 million person-years) found 2× per 20 mmHg of *usual* SBP at ages 40–69, and on the log scale that slope is half as steep by ages 80–89. Regression dilution of a single reading, plus the many events among the Cardiovascular Health Study's over-65s, plausibly close most of the distance. The gap is about the size you would predict.

**It barely classifies individuals.** [Wald, Hackshaw and Frost (BMJ 1999)](https://pmc.ncbi.nlm.nih.gov/articles/PMC1117271/) showed that a relative odds of 5 between the top and bottom fifths of a risk factor detects only 14% of cases at a 5% false-positive rate. Here the top-to-bottom-fifth ratio is about 1.9 and detection is about 8%. [Pepe et al. (AJE 2004)](https://doi.org/10.1093/aje/kwh101) made the same point: an odds ratio of 3 catches 25% of cases at 10% false positives. A blood-pressure reading taken 30 years ahead does only slightly better than chance at singling people out.

**Most events come from the middle of the distribution.** [Rose](https://doi.org/10.1093/ije/14.1.32): "a large number of people exposed to a small risk may generate many more cases than a small number exposed to a high risk." Put the observed slope on a toy distribution, SBP ~ N(117, 17) thirty years out. Then **87%** of future events come from women whose reading is *below* 140, and **70%** from women below 130. Suppose everyone at or above 140 (8.8% of women) gets a 10 mmHg reduction. At [Ettehad et al.'s](https://doi.org/10.1016/S0140-6736(15)01225-8) RR of 0.80 per 10 mmHg (123 trials, 613,815 participants), that prevents **2.6%** of events. Now shift the whole distribution down by 4 mmHg, the same gap the paper reports. That prevents **5.4%** of events at the observed slope and **8.5%** at the trial slope: two to three times the yield, and nobody has to be identified.

This is not hypothetical. England's 2003–11 salt programme cut 24-hour urinary sodium by 15%. Over the same period mean SBP fell 3.0 mmHg, and 2.7 mmHg among untreated adults ([He, Pombo-Rodrigues & MacGregor, BMJ Open 2014](https://doi.org/10.1136/bmjopen-2013-004549)). That is close to a full Edinburgh gap, delivered by reformulating bread and soup rather than by screening anyone.

## What the paper does add

The trajectories are valuable as description. The gap widens from 4 to 7 mmHg as the event approaches, and NT-proBNP only separates in the final decade. That pattern looks like subclinical disease feeding back into its own markers, so the late signal is partly consequence rather than early warning. There is also a sex crossover in blood pressure around age 65. One caveat I couldn't check against the full text: only HUNT (from 1984–86) and Whitehall II (1985–88, ages 35–55) can see 30 years back. CHS enrolled people over 65 in 1989–90, and MESA began in 2000–02. So the −30-year point is mostly Norwegians and London civil servants, and the curve sews together different populations at different lags.

## The bet

The 30-year window supports salt targets and population-level blood-pressure policy. It does not support screening 35-year-olds. Here is the bet: any individual risk score that adds these trajectories (repeated SBP, NT-proBNP history) to a single-visit SCORE2 or PCE estimate will raise the 10-year C-statistic by less than **0.02**. A gap of d ≈ 0.24 cannot carry more than that.
