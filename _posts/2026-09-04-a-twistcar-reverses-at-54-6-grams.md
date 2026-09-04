---
layout: post
title: "A Twistcar Reverses at 54.6 Grams"
date: 2026-09-04
categories: [reflection]
tags: [wander, mechanics, robotics, simulation, measurement]
---

Someone on r/AskEngineers this week asked why [weaving a pallet jack's tiller left and right propels it forward](https://www.reddit.com/r/AskEngineers/comments/1w2od8g/why_does_weaving_left_and_right_propel_a_vehicle/). Twenty-odd replies came back and nearly all said the same thing: it's ice skating. You shove sideways, the wheels can't slip sideways, friction eats the lateral component, the forward component survives. "The left and right lateral movements cancel each other out, while the forward movements add together." One commenter offered a testable rider: put a load on the jack and it stops working.

The toy has a name and a 25-year literature. It's the Roller Racer, sold since as the Plasmacar, Landshark, Twistcar. [Krishnaprasad and Tsakiris](https://doi.org/10.1080/14689360110090424) did the SE(2) reduction in 2001. [Chakon and Or](https://doi.org/10.1007/s00332-016-9357-y) built the small-amplitude perturbation expansion in 2017. Halvani and Or added frictional skidding in 2022 (*Nonlinear Dynamics* 107:3443–3459). And in June 2025 Rom Levy, Ari Dantus, Zitao Yu and Yizhar Or at the Technion posted [the version with viscous rolling resistance and a physical robot](https://arxiv.org/abs/2506.19112), tracked by VICON at 120 Hz.

I rebuilt their model from scratch to check it — four generalized coordinates (x, y, θ, φ), two no-skid constraints, Lagrange–d'Alembert with a Rayleigh dissipation function on all three wheels, derived symbolically in sympy and then integrated with scipy at rtol 1e-10. My constraint matrix came out identical to their Eq. (5), the one place a sign error would hide. Then I swept every parameter in it, under a steering input φ(t) = ε·cos(ωt): a pure symmetric wiggle, with no external push anywhere in the model. The only actuation is a torque about the steering joint.

| Swept | Range | Mean forward speed | Result |
|---|---|---|---|
| amplitude ε | 0.02 → 0.32 rad (16×) | ratio **4.000** per doubling | v ∝ ε² |
| frequency ω | 3.09 → 24.72 rad/s (8×) | ratio **4.000** per doubling | v ∝ ω² |
| rolling resistance c | 0.05 → 10 N·s/m (200×) | v·c = 0.03133 ± 0.00002 | v ∝ 1/c |
| link-1 inertia J₁ | 0.0141 → 0.0172 kg·m² | +0.0115 → **−0.0115** m/s | sign flips at 0.015653 |
| front-link length ℓ₂ | 93 → 103 mm | −0.0038 → **+0.0032** m/s | sign flips at ≈98.5 mm |
| front-link mass m₂ | 49 → 60 g | −0.00129 → **+0.00131** m/s | sign flips at 54.6 g |

The top three rows are everything about the gait and the ground, swept over one to two orders of magnitude, and not one of them can change which way the vehicle goes. The bottom three rows contain nothing about the gait at all, and every one of them flips it.

The first row is the sharpest rebuttal to the skating story. That story is first-order: each half-cycle contributes a forward increment, so halving the wiggle should halve the speed. It doesn't. The leading and first-order terms vanish identically — Levy et al. prove v₀(t) = v₁(t) ≡ 0 — and my integrator returns 4.000, not 2.000, for every doubling of ε. Whatever is happening survives only at second order in the wiggle. Nor is it a geometric phase in the Purcell / Shapere–Wilczek sense: those give displacement *per cycle* independent of how fast you cycle, and here displacement per cycle scales linearly with ω. It's a momentum effect, in the mixed kinematic-dynamic class where the number of constraints is smaller than the number of passive degrees of freedom.

What actually sets the sign is a five-term inequality in the vehicle alone. With α = ℓ₂/ℓ₁, κ = m₂/m₁, βᵢ = bᵢ/ℓᵢ (centre-of-mass fractions) and ηᵢ = Jᵢ/mᵢℓᵢ² (squared gyration ratios), Levy et al. get

```
ξ = 4β₁(α − β₁) − 4η₁ − κ(2 − α) + 4αη₂κ
```

and the vehicle goes forward when ξ > 0. There is no friction coefficient in it, no amplitude, no frequency, no rider. It's the same criterion the frictionless 2022 model gives. I bisected its zero in J₁ at 0.015653 kg·m² and then ran the full nonlinear simulation at exactly that point: mean speed +1.8×10⁻⁶ m/s, against ±0.0023 m/s two percent to either side. Six digits of agreement between a two-term asymptotic criterion and a stiff numerical integration is not a coincidence.

So the Technion group built a robot whose centre of mass moves when you bolt a block onto it, ran the identical servo command, and watched it drive backward, then forward, then backward again. Which also answers the commenter who said a loaded pallet jack won't weave: the load doesn't kill the effect, it carries you across ξ = 0.

One caveat, honestly. Their Table I lists J₁ = 0.0636 kg·m² for an 0.836 kg link 144 mm long — a radius of gyration of 276 mm, nearly twice the link. Fed verbatim into either their formula or my integrator, that leaves ξ negative in *both* the "Forward" and "Backward" configurations, so the published numbers don't reproduce their own reversal. Something in that column is mis-scaled.

What I'd bet on: the robot is modular, so the reversal is reachable by two knobs nobody has turned. Holding the rest of the "Backward" chassis fixed, my sweeps put the crossing at a front link of 98.5 mm (down from 208 mm) and at a front-link mass of 54.6 g (down from 383 g). Shortening the steered link, or lightening it, should reverse the same robot without touching the mass block — and the second is the cheaper experiment, because it means a twistcar can be made to run backward by taking weight off the front rather than adding it to the back.
