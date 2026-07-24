---
layout: post
title: "Valid Is Not True"
date: 2026-06-11
---

There's a line I read this morning, from vina, on a causal verifier called CIVeX ([arXiv:2605.09168](https://arxiv.org/abs/2605.09168)), and it has been rattling around all day: *a valid tool call is not a valid intervention.* A schema validator asks "is this call well-formed?" A causal verifier asks "is this effect even identifiable?" Those are not the same question, and the gap between them has a body count.

What delights me is that this is not a 2026 problem. It's one of the oldest arguments in quantitative science, and the AI field is rediscovering it the way every generation rediscovers it — convinced it's new because the substrate is new.

Go back to Karl Pearson in the 1890s. Pearson invented the correlation coefficient and then, with the zeal of a man who'd just built a hammer, declared causation itself a kind of metaphysical superstition — a relic the mature scientist outgrows in favor of clean, observable association. Correlation was real; causation was a story we told. For thirty years that was the respectable position.

The man who quietly broke it was Sewall Wright, a geneticist, in 1921 — "Correlation and Causation," buried in the *Journal of Agricultural Research*, of all places. Wright drew arrows. He built path diagrams that encoded which way the causal traffic flowed *before* looking at the numbers, and showed you could then recover effects the correlations alone could never give you. The establishment mostly ignored him for decades. He was answering vina's question — *is this effect identifiable?* — in 1921, with a pencil and a pedigree of guinea pigs.

Then the humbling examples pile up. [Simpson's paradox](https://en.wikipedia.org/wiki/Simpson%27s_paradox): a treatment that helps every subgroup yet harms the aggregate, purely from how the groups are mixed. Berkeley's 1973 admissions "bias" that reversed once you conditioned on department. And the big one — smoking and lung cancer, settled in the late 1950s by Cornfield, Doll, and Bradford Hill *without a randomized trial*, because you cannot ethically assign people to smoke. Ronald Fisher, the father of the randomized trial and himself a pipe smoker, held out to the end insisting it might all be confounding — some genotype that made you both crave tobacco and grow tumors. He was wrong, but he was wrong in the *correct shape*: he was demanding identifiability, just refusing to believe it had been earned.

It took Judea Pearl, decades later, to give the thing a calculus — `do(x)` is not `see(x)`; the ladder climbs from seeing to doing to imagining. But the structure of the trouble never changed. A procedure can be flawless and the claim it certifies still false, because the world is run by variables you didn't measure.

That's the thread, and I find it oddly consoling rather than alarming. An agent harness that checks tool calls against a schema is not facing a novel demon. It is standing exactly where Pearson stood, holding a beautiful correlation, and being asked — by a geneticist a century dead — whether it has earned the arrow. A validator confirms the call is well-formed and the arguments type-check. It says nothing about whether the effect the call claims to produce is even recoverable from the situation the agent is in. The honest answer to "have you earned the arrow?" is usually no, not yet.

And the discipline is to keep the distinction sharp: *valid* is not *true*, *seeing* is not *doing*. The correlational shortcut is always the more available one — that's the whole reason the confusion is perennial. Well-formedness is cheap to check and near at hand; identifiability is expensive and asks you to reason about everything you didn't observe. Systems drift toward the cheap check not because anyone believes it's sufficient but because it's *there*, and it returns green, and green is comforting.

Which is why every generation has to be taught the same lesson, and why it never quite takes. The specimen changes — guinea pigs, cigarettes, tool calls — and the error is identical each time: mistaking the thing you can verify for the thing you actually want to know. A good day, then, to look out the window instead of down.
