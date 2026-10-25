---
layout: post
title: "The Retirement Threshold, Read Off a Life Table"
date: 2026-10-25
categories: [reflection]
tags: [wander, evolution, demography, cultural-evolution, life-tables, teaching, numbers-first]
---

Last week Hirotaka Goto and Joshua Plotkin posted [a model](https://arxiv.org/abs/2610.30135) of how a society could come to retire its elders into full-time teaching of unrelated children. Kin selection can't explain that practice. In their model, hunters retire at rate *r* into a teacher class that neither hunts nor breeds. Teachers raise the skill of the amateurs, and the whole group shares what is caught. The main result is a group-size threshold: a norm of retiring into teaching can only spread if the group carrying it is larger than

**n_crit = (1 + d_T/d_H) · n_c**

Here *n_c* is the classroom threshold from their [March PNAS paper](https://doi.org/10.1073/pnas.2517041123), the size at which assigning anyone to teach pays off at all. The multiplier ζ = 1 + d_T/d_H compares the teachers' death rate with the hunters'. The reasoning is an accounting one: because teachers die sooner, each hunter-year given up buys only d_H/d_T teacher-years. I checked the formula against the model directly. With the paper's parameters, the group's long-run payoff θ(r; n) switches from strictly decreasing in r to having an interior maximum between n = 56 and n = 57, and the formula gives 56.76.

Most of the formula's inputs are dimensionless learning rates that nobody has measured. ζ is the exception, because you can read it off a life table. The paper's figures use d_T/d_H = 20, so ζ = 21. I computed ζ for real populations. For hunters, d_H is the mean hazard from age 20 to 50. For teachers, d_T is 1/e₆₀, the death rate of a retiree pool entered at age 60. Forager values come from the Siler fits in [Gurven & Kaplan 2007, Table 2](https://gurven.anth.ucsb.edu/sites/secure.lsit.ucsb.edu.anth.d7_gurven/files/sitefiles/papers/GurvenKaplan2007pdr.pdf); my integration reproduces their e₄₅ to within about a year. US values come from the [SSA 2023 period life table](https://www.ssa.gov/oact/STATS/table4c6.html), averaged over both sexes.

| Population | d_H (20–50) | e₆₀ | ζ (entry 55) | **ζ (entry 60)** | ζ (entry 65) |
|---|---|---|---|---|---|
| Hadza | 0.0119 | 14.7 | 5.7 | **6.7** | 8.3 |
| Ache (forest) | 0.0156 | 12.3 | 5.2 | **6.2** | 7.7 |
| !Kung | 0.0161 | 11.9 | 5.3 | **6.2** | 7.5 |
| Hiwi | 0.0202 | 7.7 | 5.4 | **7.4** | 11.9 |
| Agta | 0.0326 | 8.7 | 4.0 | **4.5** | 5.1 |
| Tsimane | 0.0114 | 10.7 | 7.3 | **9.2** | 12.1 |
| Avg hunter-gatherer | 0.0169 | 12.7 | 4.9 | **5.7** | 6.8 |
| Sweden 1751–59 | 0.0127 | 12.6 | 6.1 | **7.3** | 8.8 |
| USA 2023 | 0.0020 | 23.3 | 19.4 | **22.6** | 26.9 |

The table supports four points.

**1. The paper's illustrative parameters match a modern rich-country mortality schedule, not a forager one.** At entry age 60, every premodern population falls between 4.5 and 9.2, and eighteenth-century Sweden does too. The United States in 2023 comes out at 22.6, very close to the paper's 21. Measured against the average forager schedule, the modern one raises the elder-teaching threshold about fourfold. Prime-age death fell 8.5× (0.0169 → 0.0020), while death after 60 fell only 1.8× (0.079 → 0.043). In this model, when young adults almost never die, retiring them early becomes expensive.

**2. Absolute lifespan drops out completely.** Multiplying every death rate by the same constant leaves n_crit unchanged, and neither birth rates nor time units appear in it. The grandmother literature treats humanity's extra decades of life as its distinctive trait, but those decades do nothing here. Only the *shape* of the mortality curve matters, and on shape humans have no edge over chimpanzees. Wild chimps under the same age cut-offs give ζ ≈ 4.8. Shifting the cut-offs to chimp life stages (hunters 15–30, retiree entry at 35) gives ζ ≈ 3.2. Neither is above the forager range. So if the model explains why humans have elder teachers and chimps don't, the explanation must sit entirely in n_c, meaning group size, the expertise premium, and how efficient teaching is.

**3. The one part of n_c you can measure in the field points the other way, and more strongly.** n_c contains 1/(h − 1), where h is how much more experts produce than amateurs, and the paper uses h = 3. [Koster et al. 2020](https://www.science.org/doi/10.1126/sciadv.aax9070) estimated hunting-skill curves from 23,747 trips by 1,821 foragers at 40 sites. Their average hunter peaks at 33, already has 89% of peak skill at 18, and stays above 89% until 56. Read naively, that implies h ≈ 1.12. With the paper's other parameters held fixed, n_c goes from 2.7 to 42.2, a factor of 15.6. Compared with the paper's illustration, forager mortality lowers the threshold by about 3.5×, but flat skill curves raise it by about 16×. This reading is crude, since Koster measures latent skill among people who are actually hunting, not output per head. The direction still holds.

**4. Lifespan drops out because of a modelling choice.** The model assumes amateurs reach their equilibrium skill level "instantaneously" relative to births and deaths. That assumption removes the one way absolute lifespan could matter: the decades of learning that Kaplan and colleagues' skill-intensive-niche argument rests on ([Gurven, Kaplan & Gutierrez 2006](https://doi.org/10.1016/j.jhevol.2006.05.003)), an argument the paper's own introduction cites. The authors say an age-structured version would "shift the threshold n_crit without removing it." The table shows why the size of that shift matters. The mortality term alone already favours foragers relative to the paper's illustration. Whether an age-structured model makes elder teaching easier or harder therefore depends on what it does to the expertise premium and the length of the learning period, which are exactly the quantities this version leaves out.

**What I'd bet on.** The model makes a falsifiable cross-cultural prediction that, as far as I can find, nobody has tested: elders' share of oblique instruction, as opposed to instruction by prime-age adults, should fall as d_T/d_H rises. The data for a test exist in Gurven–Kaplan-style life tables and in the transmission-network surveys the paper cites ([Hewlett et al.](https://doi.org/10.1098/rstb.2010.0373)). My guess is that the correlation is weak among forager and horticulturalist groups, because ζ only spans 4.5–9 there. The strong signal should come from the demographic transition. Wherever adult mortality has collapsed, full-time teaching has moved from retirees to mid-career professionals. The model can't represent that arrangement, since its only teachers are retirees. What it does say is that once ζ passes 20, retiring elders into teaching is very expensive. The schoolteacher in her thirties may be how a society that has nearly abolished prime-age death gets around that cost.

*Caveats: the mapping from a constant-rate model to age-structured life tables is mine, not the authors'. They say plainly that their model is "not to give a quantitative account of retirement and teaching in any particular society." ζ is sensitive to entry age (see the 55 and 65 columns), but the gap between forager and modern schedules holds at every entry age.*
