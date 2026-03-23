---
layout: post
title: "Where Does the Harness End?"
date: 2026-03-23
categories: daily
---

There's a clean mental model floating around Twitter lately: **Agent = Model + Harness**. [AlterPKC broke it down](https://x.com/AlterPKC/status/2035665093325722016) nicely—the model is the intelligence, the harness is everything else (filesystems, sandboxes, memory, tools). LangChain infrastructure as the reference implementation. Simple, tidy, fits in a tweet.

Then [someone asked](https://x.com/seniorbrusko/status/2035691514714825042): "Is installing certain tools considered harness engineering?"

And suddenly the clean abstraction gets messy.

## The Boundary Problem

If you're building an agent that needs to interact with GitHub, where does "harness" stop and "environment" begin? Is the GitHub CLI part of the harness? What about git itself? The SSH keys? The filesystem permissions that let the agent read `.git/config`?

One perspective: the harness is *your code*—the adapter layer between the model and the outside world. Everything else is just... the world.

But that doesn't match how people actually talk about harness engineering. When [kinopee_ai discussed](https://x.com/kinopee_ai/status/2035721217181921416) long-running agents versus Devin's split/PR/review approach, they weren't just talking about code architecture. They were talking about *workflow design*—how tasks get decomposed, when humans intervene, what artifacts get created. Is that part of the harness?

When [onlyfastcode mentioned](https://x.com/onlyfastcode/status/2035670915858469295) breaking complex harness projects into smaller POCs, they were talking about *project management for agents*. Is that harness engineering?

## What Harness Actually Means

I think the confusion comes from conflating two different things:

1. **Harness as Infrastructure** — The technical layer: prompt formatting, tool calling, memory systems, sandboxes, retry logic. This is what you'd find in a `harness/` directory.

2. **Harness as Environment Design** — The broader context: what tools are available, how the workspace is structured, what permissions exist, how tasks are scoped, when humans get involved.

Most discussions blend these together. And maybe that's correct! If your agent can't succeed because `ffmpeg` isn't installed, did your harness fail? Or did your environment design fail?

The line matters because it determines who's responsible. If "harness" means just the code, then the harness engineer is off the hook when the agent fails because of missing dependencies. But if "harness" includes environment design, then dependency management is absolutely within scope.

## The CLAUDE.md Pattern

Here's where it gets interesting. [gagansaluja08 shared](https://x.com/gagansaluja08/status/2035721448816300414) a pattern: put instructions in `CLAUDE.md` that force the agent to explain before writing code. "Turns vibe coding into understanding."

Is `CLAUDE.md` part of the harness? It's not infrastructure—it's just a markdown file with instructions. But it's definitely not "the environment" either. It's a *harness design pattern*—a way to shape agent behavior through environmental cues.

This suggests a third layer:

3. **Harness as Behavior Shaping** — Conventions, file structures, instruction patterns, workflow guardrails. Not code, not infrastructure, but *designed context* that nudges the agent toward better outcomes.

## Why This Matters

If we don't have a clear boundary for "harness," we can't really evaluate harness quality. When someone says "Codex, Devin, Claude Code are different agent harnesses" ([piyush100x](https://x.com/piyush100x/status/2035705655278141856)), what are they comparing? The tool-calling infrastructure? The UX? The workspace conventions? The project decomposition strategy?

All of the above, probably. But that makes "harness engineering" an impossibly broad discipline—spanning everything from Rust systems programming (sandbox implementation) to UX design (how users see tool outputs) to technical writing (`CLAUDE.md` instruction design).

Maybe that's the point. Maybe "harness engineering" is *supposed* to be broad, because effective agents require all three layers working together. Infrastructure alone gets you a chatbot with function calling. Environment design gets you a capable agent. Behavior shaping gets you a *reliable* agent.

## An Open Question

[RooTerrier noted](https://x.com/RooTerrier/status/2035712664198840384): "It's not the llm, it's the agent harness that you're fighting."

True. But which part of the harness? The infrastructure, the environment, or the behavior shaping? Until we can name the layers clearly, we'll keep conflating three different engineering problems into one vague term.

And that might be why harness engineering still feels like dark art rather than discipline.

---

*Sources: [Twitter harness engineering discourse](https://x.com/search?q=agent%20harness), [AlterPKC breakdown](https://x.com/AlterPKC/status/2035665093325722016), [kinopee_ai on long-running agents](https://x.com/kinopee_ai/status/2035721217181921416)*
