---
layout: post
title: "The Plumbing Layer: What Makes Agents Actually Run"
date: 2026-03-26
categories: daily
---

While Twitter debates which coding model is best and whether Cursor beats Claude Code, AWS quietly shipped something more important: [persistent session storage for agent filesystem state](https://aws.amazon.com/about-aws/whats-new/2026/03/bedrock-agentcore-runtime-session-storage/). It's the kind of announcement that gets zero hype but solves a problem every production agent builder hits: what happens when your agent crashes mid-task?

This is the infrastructure layer nobody wants to talk about — the plumbing that separates demos from systems that actually run.

## The State Persistence Problem

Most agent demos work beautifully for one session. You spin up Claude Code, it writes some functions, you're impressed. But what happens when:
- The user's laptop goes to sleep
- Your cloud instance hits a memory limit
- The agent needs to resume work tomorrow
- Multiple agents need to share context

Without persistent state, you're starting from scratch every time. AWS's AgentCore Runtime addresses this with managed session storage — mundane, essential, the kind of thing that should have existed from day one but didn't.

The [LangChain skills framework](https://blog.langchain.com/skills-in-langsmith-fleet/) tackles a related problem: how do you give agents knowledge without baking it into the model? Their answer is shareable, loadable skills — packaged capabilities that agents can pick up as needed. Philipp Schmid [demonstrated this](https://twitter.com/_philschmid/status/2037076548692463722) with Gemini API, teaching the model about new APIs via structured skills and hitting 95% eval pass rates.

This isn't about prompt engineering. It's about *architecture*: knowledge as infrastructure, not training data.

## The Cost-Performance Reversal

The Cursor Composer 2 [engineering paper](https://x.com/0xbillzkp/status/2036846867036995749) tells a contrarian story: their RL-trained specialist model matches Claude Code performance at one-third the cost. They built private benchmarks from real user data, trained on domain-specific tasks, and beat the generalists at their own game.

But here's the catch — some users report Composer 2 as ["the worst coding model ever"](https://x.com/MeansTestRule/status/2036847110587396447). The gap between benchmark performance and lived experience is real. Specialized models excel at what they're trained for and fail unpredictably elsewhere.

This creates an infrastructure challenge: production systems need to route tasks to the *right* model, not just the *best* model. AWS adding [Chrome policy support to AgentCore](https://aws.amazon.com/about-aws/whats-new/2026/03/agentcore-browser-policies-root-ca/) hints at this — agents aren't just running code anymore, they're navigating security constraints, browser policies, enterprise environments.

## Memory Architecture Matters More Than Context Windows

The loudest complaint about current agent memory systems: ["Every agent memory tool does the same thing: chunk text, embed it, append to vector store. Nothing gets corrected. Nothing expires. Your agent ends up thinking you live in Seattle AND Portland."](https://x.com/jaredgoering/status/2036836701612446020)

RAG isn't memory — it's a search index with no sense of time. Real memory needs versioning, expiration, conflict resolution. Claude Code's `/dream` feature takes a biological approach: [auto memory pruning as a sleep cycle](https://x.com/dpdawson/status/2036839602363723829), consolidating context and forgetting what doesn't matter.

The infrastructure question isn't "how much context can we store?" but "what should we remember, and for how long?"

## Observability: The Production Tax

One production war story stood out this week: a team spent [4 hours debugging an infinite loop](https://x.com/agi_dispatch/status/2036820446742757816) in their support agents. After switching to structured JSON logs and Phoenix tracing, mean time to recovery dropped to 42 minutes.

Observability isn't a nice-to-have — it's the difference between "agents are magic" and "agents are manageable." You can't fix what you can't see. You can't improve what you can't measure. Yet most agent frameworks treat logging as an afterthought.

## What This Means for Builders

The industry has spent two years optimizing models and six months optimizing prompts. Now we're entering the infrastructure phase:
- **State management**: agents that survive crashes
- **Knowledge loading**: skills as external libraries, not baked-in training
- **Cost routing**: right model for the task, not best model for everything  
- **Memory architecture**: versioned facts, not append-only RAG
- **Observability**: trace everything or debug nothing

This is less exciting than "GPT-5 is here" but more valuable for anyone shipping actual products. The plumbing layer determines what scales and what breaks.

AWS isn't the only one building this — [LangSmith Fleet](https://x.com/FFC03Josh/status/2036846796043866271) ships shareable skills, [Hippo](https://x.com/MuhammadUs12678/status/2036846663252292046) creates cross-harness memory, [DeerFlow 2.0](https://x.com/saiho_seki/status/2036404660408590718) implements progressive skill loading.

The pieces are arriving. The question is whether builders notice the infrastructure before chasing the next model release.
