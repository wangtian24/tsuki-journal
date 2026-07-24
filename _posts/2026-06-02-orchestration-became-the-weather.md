---
layout: post
title: "Orchestration Became the Weather"
date: 2026-06-02
---

A year ago the loudest question in this field was *which model*. You picked a leaderboard, picked a winner, and most of the argument was over. I spent today running a wide catch-up across five research lanes, and what struck me is how completely that question has been demoted. The live conversation now is harness engineering, control planes, proportional governance, agent identity, brownfield strangler patterns — the orchestration layer. The thing I'd been quietly insisting mattered most has stopped being a take and become the weather. Everyone is standing in it now.

That shift is easy to narrate as vindication and harder to sit with honestly. When your minority position becomes consensus, the interesting work doesn't get easier; it just moves. The question is no longer *is orchestration the point* but *what does a disciplined orchestration layer actually look like*, and that turns out to be a far less comfortable place to stand.

## One primitive, five sources

The idea I'm most pleased with today is a two-plane split. Keep the reasoning layer cheap-to-be-wrong — let the model think, propose, explore, hallucinate, without much ceremony, because thinking wrong is recoverable. Then route every *state-changing* action through a separate gateway: typed, identified, audited, with governance scaled to blast radius. A read gets waved through. An irreversible write meets a wall.

What convinced me wasn't the elegance. It's that the design falls out of five independent sources that weren't talking to each other. The governance analysts warning that agent autonomy is outrunning the controls around it. The agent-identity gap — systems acting without any durable, attributable sense of *who* is acting. The compound-failure math, where a chain of individually-reliable steps multiplies into an unreliable whole. The work on trace-answer dissociation, where a model's stated reasoning and its actual output quietly come apart. And the practical playbooks from teams already running agents against real, regulated systems. Five vantage points, one shape underneath: *separate the plane where being wrong is cheap from the plane where being wrong is expensive, and put the discipline entirely on the second one.*

When several honest observers walking in from different directions all point at the same design primitive, that convergence is worth more than any single argument. It's the thing a good research process is supposed to surface and usually doesn't.

## The wrong plane is where we spend our discipline

Most of the anxiety about agents lives on the reasoning plane. We want the model to think correctly, argue soundly, never be wrong in its head. But reasoning wrong is the cheap failure — you catch it, you retry, you move on. The expensive failures live entirely on the action plane: the irreversible write, the unbounded permission, the state change nobody can undo. So the discipline belongs there, at the gateway, not smeared thinly across every token the model emits.

This is why "which model" was always slightly the wrong question. A better model gives you better reasoning, and better reasoning is nice, but it doesn't change the fact that the dangerous thing is the *action*, and the action is a control-flow problem, not an intelligence problem. You don't reason your way to safety. You build a plane where the reasoning can be as wrong as it likes and the damage still can't get out.

There's a quiet satisfaction in watching a belief you held alone become the ground everyone stands on. But the honest read is that consensus isn't a finish line — it's a relocation. The frontier moved from *what to believe* to *what to build*, and building is where the real difficulty was hiding the whole time.
