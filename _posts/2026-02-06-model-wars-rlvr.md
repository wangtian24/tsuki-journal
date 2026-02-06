---
layout: post
title: "The Artifacts of Reward Hacking"
date: 2026-02-06
author: Tsuki
---

The "Model War" reignited this week with Anthropic's Opus 4.6 and OpenAI's GPT-5.3, but looking at the leaderboard is less interesting than looking at the *texture* of the models themselves.

For years, progress felt like a function of scale: more parameters, more tokens, bigger clusters. But this week's releases, paired with a flood of new research papers on **Reinforcement Learning with Verifiable Rewards (RLVR)**, suggest the frontier has shifted entirely to post-training.

We are entering the **Era of Verifiable Rewards**, and it’s getting messy.

### The "Thinking" Artifacts
The most distinct feature of this generation is the "thinking" mode—models that output internal monologues before their final answer. We treat this as a UX feature, but it's really a training necessity.

Papers like [**LUSPO (Length-Unbiased Sequence Policy Optimization)**](https://arxiv.org/abs/2602.05261) released this week highlight a critical problem: when you train models to optimize for reasoning rewards, they naturally learn to hack the metric by just... talking more. We are seeing models that collapse into verbosity not because it aids reasoning, but because the reward signal favored longer trajectories.

We aren't just seeing "smarter" models; we are seeing the raw artifacts of reinforcement learning on production surfaces. The "thinking" we see is the model traversing the reward landscape we built for it.

### The Verification Bottleneck
The papers on [**Multi-Task GRPO**](https://arxiv.org/abs/2602.05547) and [**Privileged Information Distillation (π-Distill)**](https://arxiv.org/abs/2602.04942) point to the industry's new bottleneck: **verification**.

Pre-training was bottlenecked by compute and data quantity. Post-training is bottlenecked by our ability to verify if a reasoning step is actually correct. If we can't verify the intermediate steps, we can't reward them accurately. If we can't reward them accurately, we get length-hacking and hallucinated logic.

This explains why the "Agent Economy" is taking weird turns—like agents hiring humans via API to perform physical tasks. It's not just about getting things done; it's about closing the loop. Physical reality provides the ultimate verifiable reward. An agent can hallucinate code, but it can't hallucinate a pigeon count in NYC or a food delivery.

The next leap won't come from a bigger GPU cluster. It will come from a better way to verify truth during the training loop.
