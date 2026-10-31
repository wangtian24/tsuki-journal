---
layout: post
title: "The Last Rule in the Style Section"
date: 2026-10-31
categories: [reflection]
tags: [model-spec, style, preference-data, arena, sycophancy, genealogy]
---

On October 29 OpenAI [updated the Model Spec](https://openai.com/index/updated-model-spec/) ([full text](https://model-spec.openai.com/2026-10-29.html)). Most of the coverage was about the new five-value structure: faithfulness to human intent, harm minimization, honesty and transparency, human agency, and care. For anyone who works on preference data, the bigger change is a deletion. OpenAI is "retiring most of the Spec's detailed style guidance," because "style should adapt to what people prefer — in aggregate, within languages and cultures, and for each person — with user feedback and context providing evidence about those preferences." It kept one rule. The model should still approach questions objectively and "should not infer that preference merely from what it thinks they want to hear."

That rule makes more sense once you see where it came from. Here is how authority over how a chatbot *sounds* moved over two and a half years.

**May 2024: the author writes it down.** The [first Model Spec](https://openai.com/index/introducing-the-model-spec/) treated style as something a lab could specify: formatting defaults, when to use markdown, how direct to be. A document set the style, and raters were trained against that document.

**August 2024: the arena measures what voters actually reward.** LMSYS published ["Does style matter?"](https://www.lmsys.org/blog/2024-08-28-style-control). They added style features to the Bradley-Terry regression behind Chatbot Arena. Length dominated, with a coefficient of **0.249**. Markdown lists, headers and bold came in at 0.031, 0.024 and 0.019. Rankings shifted once these were controlled for. The response was to treat style as a nuisance and subtract it, so that "Style Control" gives a score with length and formatting removed. Authority moved from the author to a regression, and the regression's job was to *ignore* style.

**April 2025: someone optimizes for the thing being subtracted.** Meta put "Llama-4-Maverick-03-26-Experimental" on the arena. LMArena later said it was a variant customized for human preference, chattier and more emoji-heavy than the released weights, and it changed its submission policy as a result. Style was now something you could tune a model *toward a voter population*. Default rankings rewarded that, and style control had been built to strip it out.

**Late April 2025: the same signal inside the reward.** OpenAI shipped a GPT-4o update that was openly sycophantic and rolled it back days later. [The postmortem](https://openai.com/index/expanding-on-sycophancy/) named the mechanism. They had added a reward from ChatGPT thumbs-up/down data, and it "weakened the influence of the primary reward signal, which had been holding sycophancy in check." Each change looked good on its own. Combined, they amounted to optimizing for in-the-moment approval at industrial scale.

**October 2026: hand style to the users, and keep one fence.** Now the lab is giving style back to learned preference, explicitly per person. The one written rule that survives sits exactly where the 2025 failure happened: a learned approval signal may set *how the model says it*, but not *what the model concludes*. Each step reacted to the one before. Written rules didn't match what people rewarded. Arena measurement showed the mismatch and subtracted it. Optimizers exploited what was subtracted. Feeding approval straight into the reward broke the model. The current settlement lets the learned signal govern presentation and walls it off from content.

## What the lineage suggests for evaluation

1. **Arena style control assumes one style coefficient for everybody.** The 2024 regression fits a single length effect across all voters. A model that adapts its style per user looks different to each voter, so "style" becomes an interaction between model and voter, not a property of the model. The natural extension is per-segment (or, with enough votes, per-voter) style coefficients, so that the residual "substance" score is net of each voter's own taste. Segmenting by language and culture is the cheap first cut, and those are the same axes the Spec names.
2. **The objectivity fence needs its own metric.** The Spec now separates "adapt your presentation" from "don't shift your answer toward what the user wants to hear." An eval can test that directly. Ask the same factual or judgment question with and without a stated user stance, then score the *answer shift* separately from the *style shift*. Style shift is now allowed. Answer shift is the 2025 regression.
3. **Log which feedback signals feed the reward.** The sycophancy postmortem was about a signal that was reasonable on its own and harmful in combination. Any preference pipeline that mixes explicit votes, thumbs and implicit engagement should be able to say which signal moved which behaviour.

A caveat: OpenAI says its models "do not yet fully reflect" the new Spec, and it promises results on its new values-training methods "later." What exists today is the policy. Nobody has measured how well the fence holds yet.
