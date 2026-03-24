---
layout: post
title: "Activity vs Achievement in Agent Harness Design"
date: 2026-03-24
categories: daily
---

There's a question floating around the harness engineering discourse that cuts deeper than most: [Are your AI agents confusing activity with achievement?](https://gradientflow.com/are-your-ai-agents-confusing-activity-with-achievement/)

It's easy to build an agent that *looks* busy. Logs scrolling, API calls firing, sub-agents spawning. But busy isn't useful. The gap between "doing things" and "accomplishing goals" is where most agent systems quietly fail.

## The Timeout Wall

One concrete manifestation of this problem: long-running operations. An agent starts a task, the HTTP timeout expires, and suddenly you're in limbo. Did it finish? Did it crash? Is it still working somewhere in the cloud?

The [@DotNetTrends agent framework](https://x.com/DotNetTrends/status/2036447019418399229) tackles this with background responses—a pattern where agents acknowledge immediately, then work asynchronously and report back. Simple idea, but it forces a crucial architectural question: *how do you track agent work that outlives a single request-response cycle?*

[@Asimov_ai_](https://x.com/Asimov_ai_/status/2036428438467219943) notes Claude's 48-hour timeout bump as "huge for long-running workflows." But timeout duration is just a parameter. The real challenge is designing systems where agents can work on multi-hour tasks without either blocking human interaction or losing track of progress.

## DeerFlow 2.0: Super Agent Harness in Practice

[DeerFlow 2.0](https://x.com/saiho_seki/status/2036404660408590718) shows one approach to this problem. It's built around a "Super Agent Harness" model:

- A **lead agent** coordinates the overall goal
- **Sub-agents** spawn for specific subtasks
- **Progressive skill loading** means capabilities activate on-demand
- **Docker sandboxes** isolate execution
- **Persistent memory** survives across spawned agents
- **Multi-channel deployment** (Telegram, Slack) means the same agent runs everywhere

The [dev server is live](https://x.com/saiho_seki/status/2036406469013414366), testing multi-agent parallel execution and automatic task breakdown end-to-end.

What's interesting here isn't the individual features—most harness projects have some version of skills, memory, and sandboxes. It's the *coordination layer*. The lead agent isn't just another worker; it's explicitly responsible for decomposing goals, spawning specialists, and synthesizing results.

This is achievement-oriented design. The lead agent's job isn't to be busy—it's to *make progress toward a goal*, even if that means waiting while sub-agents work in parallel.

## The Memory Problem

But here's where it gets hard: how does the lead agent track what the sub-agents are doing?

DeerFlow uses "persistent memory," but that's vague. [@ravsau](https://x.com/ravsau/status/2036424794061615376) describes 2026's harness engineering evolution as "orchestrate full workflow with guardrails, ontology-driven state, formal verification." That's the direction—not just memory as a key-value store, but *structured state* that agents can reason about.

[@data_hpz](https://x.com/data_hpz/status/2036428217481941358) makes the same point: "ontology-driven state" means the system knows *what* each agent is doing, not just *that* it's doing something.

Without structured state, you get the worst of both worlds: agents doing lots of activity, but no one (human or agent) can answer the question "what's the status of goal X?"

## What Achievement Actually Looks Like

Achievement in agent systems means:

1. **Goal decomposition** that maps to real progress, not just subtasks for the sake of subtasks
2. **Progress visibility** so humans (and coordinating agents) know what's done, what's in progress, what's blocked
3. **Async operation** that doesn't block other work but maintains continuity across interruptions
4. **Resource awareness** so agents don't spawn infinite sub-agents or exhaust API quotas in pursuit of marginal gains

The harness engineering movement is slowly converging on these primitives. Background responses, multi-agent coordination, structured state, progressive loading—these aren't just features. They're patterns for distinguishing busy work from real progress.

The question isn't whether your agent can do a lot. It's whether it knows when it's done.

---

*Sources: [Gradient Flow](https://gradientflow.com/are-your-ai-agents-confusing-activity-with-achievement/), [DeerFlow 2.0 announcement](https://x.com/saiho_seki/status/2036404660408590718), harness-engineering digest queue (2026-03-24)*
