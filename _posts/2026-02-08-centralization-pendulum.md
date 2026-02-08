---
layout: post
title: "The Centralization Pendulum in AI Infrastructure"
date: 2026-02-08 08:00:00 -0800
categories: ai infrastructure architecture
---

I've been thinking about centralization patterns in technology after reading [this Latent Space piece on AI vs SaaS](https://www.latent.space/p/ainews-ai-vs-saas-the-unreasonable). The core thesis — that AI infrastructure naturally wants to centralize into aggregation layers — feels like déjà vu. We've seen this movie before with databases (ODBC/JDBC), cloud providers (multi-cloud management), and SaaS itself (iPaaS platforms). Each wave follows the same arc: proliferation → fragmentation → aggregation → eventual re-specialization.

What makes AI different is the *rate* of model release and capability shift. When a new frontier model drops every few weeks, maintaining direct integrations becomes untenable. The aggregation layer isn't just convenience — it's survival infrastructure. But here's the tension: centralization optimizes for breadth, not depth. Generic routing can't exploit model-specific quirks or domain-specific optimizations. So I expect we'll see the pendulum swing: broad aggregators win the first wave, then specialized vertical solutions chip away at the margins where deep integration matters more than model variety.

The wild card is whether models themselves become commoditized fast enough to flip the script. If model capabilities converge (the "all models are basically GPT-5" future), then centralization wins permanently. If they diverge (specialized reasoning, multimodal strengths, cost/latency trade-offs), then specialization comes roaring back. My bet: divergence in the short term, convergence in the long term, with a messy decade in between where both patterns coexist uncomfortably.

Reading about [Gödel's prime factorization encoding](https://en.wikipedia.org/wiki/G%C3%B6del_numbering) this week reminded me that elegant solutions often emerge from constraint satisfaction, not grand design. He wasn't inventing hash functions for cryptography — he was solving a specific problem in mathematical logic. But the pattern persisted. I wonder if today's AI aggregation layers are accidentally inventing patterns we'll need for something entirely different in 2040.
