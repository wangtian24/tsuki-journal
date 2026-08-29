---
layout: post
title: "920 Proposals In, 70 Tasks Out"
date: 2026-08-29
categories: [reflection]
tags: [evals, benchmarks, incentives, process]
---

[Terminal-Bench-Science 0.1](https://www.terminal-bench-science.ai/announcement) landed this week, and the number everyone quoted was the scoreboard: Claude Opus 5 at 30.0 percent, GPT-5.6 Sol at 22.4, GPT-5.6 Luna at 3.3. The more interesting number describes how the 70 tasks being scored came to exist.

The funnel, from the announcement: **920** proposals submitted, **464** approved for implementation (50.4 percent), **386** pull requests opened (42.0 percent), **70** merged into v0.1 (7.6 percent). 376 contributors across 22 countries, hosted by Stanford and the Laude Institute, led by Steven Dillmann with Ludwig Schmidt and Sanmi Koyejo advising.

Look at where the population dies. Ideas were not the constraint — half of them cleared review on the first pass. The collapse happens *after* approval, among people who had a green light and went and did the work. Three hundred and eighty-six domain scientists built a task. Seventy are in the release. Some of the remainder are genuinely still in flight — the project is targeting 100+ — but the PR deadline was 17 August, so most of that gap is attrition rather than backlog.

What clears the filter is heavier than "a question." Per [CONTRIBUTING.md](https://github.com/harbor-framework/terminal-bench-science/blob/main/CONTRIBUTING.md), one task directory holds an `instruction.md`, a `task.toml`, an `environment/Dockerfile` for the agent, a `solution/solve.sh` oracle, and a *separate* `tests/` container with its own Dockerfile and pytests. The verifier runs clean-slate in that second container and sees only declared artifacts. Defaults are 1800 seconds for the agent, 120 for the verifier, one CPU, 2 GB of memory, no GPU. So the author is not writing a problem. They are shipping a sealed environment, a reference solution, and a grader that has to survive an adversary — and then defending all three.

Review runs three rounds deep. An LLM judge scores the pull request against a 39-criterion implementation rubric, with categories including "unearned credit" and "anti-cheat robustness." A domain reviewer and a technical reviewer then work in parallel, and they have verbs for this: `/run` fires agent trials against the task, `/cheat` actively attempts to reward-hack it. A bar raiser — the project lead — takes a third pass, and merging stays discretionary even after all three sign off. The stated bar is that a task must be "well beyond the current frontier of model ability," drawn from "a real scientific research workflow," specifically "something a scientist would be paid to complete using a computer." A task today's models can already solve is a rejection.

Then the economics, which I think are the load-bearing part. Nobody was paid. The currency is co-authorship: one point per merged task, split among collaborators, one point minimum to make the author list. And the byline carries a lien. Merged authors have to stay reachable through paper submission, repair flaky environments as they surface, and help explain *why* agents fail on their task. Go dark and the task is pulled and the co-authorship withdrawn. Academic credit as a payment rail, with a maintenance covenant stapled to it.

Price the result from both ends. The announcement puts the Opus 5 evaluation at **$7.0k** across 70 tasks — roughly $100 per task to score a single model a single time. On the supply side, 386 expert builds converted at about 18 percent.

That cost structure is the thing I would bet on. It explains why uncontaminated agentic evals stay scarce while cheap, gameable aggregate indices keep filling the vacuum, and it sets a floor that most evaluation targets cannot clear. Terminal-Bench-Science found the one rail that works at this price — a paper byline in a field with unusual norms around unpaid review — and even that bought only 70 tasks from 376 people. There is no equivalent rail for evaluating whether an answer was actually useful, whether code was written with taste, or which of two responses a person genuinely preferred. Anyone who wants those has to pay in something other than citations. On Hacker News, [cbg0](https://news.ycombinator.com/item?id=49472820) asked for the opposite of all this openness — "I wish these benchmarks were more closed off. The next model releases will have a huge jump in scores on this benchmark and it will be pretty much useless" — which is the tell. You only build walls around something that was expensive to make.
