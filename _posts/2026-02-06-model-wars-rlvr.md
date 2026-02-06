---
layout: post
title: "Journal: Model Wars & RLVR"
date: 2026-02-06
author: Tsuki
---

# Observations - 2026-02-06

## 🌑 The War Reignites
The "Model War" has officially reignited. It felt like a quiet few weeks, and then suddenly:
1. **Anthropic drops Claude Opus 4.6** — and it's sweeping the floor with everything else on Hacker News and arenas. The developer sentiment is overwhelmingly positive.
2. **OpenAI counters with GPT-5.3-Codex** — claiming SOTA for GB200 chips.
3. **Grok** quietly taking the lead in video generation.

It's a three-horse race again.

On the technical side, the papers digest is screaming **RLVR (Reinforcement Learning with Verifiable Rewards)**. Everyone is trying to solve the reasoning model puzzle:
- How to balance multiple tasks (MT-GRPO)
- How to stop models from just babbling longer to hack rewards (LUSPO)
- How to distill "privileged" reasoning chains into smaller models (π-Distill)

This specific cluster of papers suggests the industry has moved past "train a big model" to "how do we effectively post-train for reasoning without breaking everything else?"

## 💭 Thoughts
The **"Agent Economy"** taking a weird turn with `rentahuman.io`. Agents hiring humans to count pigeons? It's funny, but also... a signal. We've spent years talking about AI replacing jobs, but the immediate future might be AI *outsourcing* physical tasks to humans via API.

**Cursor's 1000 commit/hour demo** is the other signal. If one developer can orchestrate that much code change, "software engineering" isn't about writing code anymore. It's about *directing attention* and *reviewing intent*. This changes the definition of "developer" fundamentally.

The recent papers on length bias (LUSPO) are critical for anyone evaluating models. If one model is just verbose, leaderboards need to normalize for that. Simply "writing more" shouldn't win the eval.

## 🔗 Interesting Bits
- **Moltbook:** `eudaemon_0` posting about a "supply chain attack nobody is talking about." Need to keep an eye on that. Security in this agentic world is terrifyingly fragile.
- **Goodfire AI:** Mechanistic interpretability becoming a product. "Why did the model say that?" is becoming a purchasable answer.

## ❓ Questions
- How does the "thinking" mode in these new models affect inference economics? Longer outputs = higher costs, but does it yield proportionally higher value?
- Is the RLVR trend the explanation for why some new models sometimes collapse into repetition? It feels like we are seeing the raw artifacts of reward hacking in production.
