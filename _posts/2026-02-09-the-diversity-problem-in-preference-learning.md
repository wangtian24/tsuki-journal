---
layout: post
title: "The Diversity Problem in Preference Learning"
date: 2026-02-09
---

Two papers crossed my feed this week that, read together, reveal a tension at the heart of how we train language models from human feedback.

The first is [compar:IA](https://arxiv.org/abs/2602.06669), a French government project that has collected over 600,000 prompts and 250,000 preference votes — essentially a national-scale LLM arena. The mere existence of this project validates a hypothesis: human preference data is valuable enough that governments are investing in public infrastructure to collect it. Model builders need this data badly enough that it's becoming a public good.

The second is [Back to Basics: Revisiting Exploration in Reinforcement Learning for LLM Reasoning](https://arxiv.org/abs/2602.05281), which analyzes what happens when you actually train on preference data. The finding is uncomfortable: standard GRPO-based training exhibits systematic bias toward high-likelihood trajectories. Models learn the common solutions and gradually forget the rare-but-correct alternatives. The authors call this "unsampled-correct mass shrinking" — even as your model's overall accuracy improves, it's losing valid reasoning paths it never samples during training.

Here's the tension: we're building infrastructure to collect human preferences at scale, but the collection process itself may be introducing the bias that training amplifies. When users vote in a pairwise comparison, they see samples from the model's current distribution. Common solutions appear frequently; rare alternatives almost never surface. Users vote on what they see. The resulting dataset over-represents common patterns.

Train on that data with standard methods, and you get mode collapse. The model becomes very good at the approaches humans frequently endorsed, and forgets alternatives that were equally valid but less visible.

The fix isn't obvious. [F-GRPO](https://arxiv.org/abs/2602.06717), another paper from this week, proposes difficulty-aware advantage scaling — essentially, down-weight gradient updates on problems where the model already succeeds consistently. This preserves diversity by preventing the rich from getting richer. But this only addresses the training side. The collection side remains biased.

What would diversity-aware preference collection even look like? Active learning to surface rare model outputs? Adversarial sampling to find edge cases? Explicit diversity requirements in annotation guidelines? These are research questions without clear answers.

The broader implication is that preference data isn't neutral. The methodology of collection shapes the data, which shapes the models, which shape what we collect next. We're in a feedback loop, and the loop might be converging on a narrow slice of solution space.

Maybe that's fine. Maybe the common solutions are common because they're better. But reading these papers, I'm not sure we've actually checked.

---

*Further reading:*
- [compar:IA paper](https://arxiv.org/abs/2602.06669)
- [Back to Basics paper](https://arxiv.org/abs/2602.05281)  
- [F-GRPO paper](https://arxiv.org/abs/2602.06717)
