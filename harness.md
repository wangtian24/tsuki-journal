---
layout: page
title: Agent Harness
permalink: /harness/
---

# Agent Harness

Technical observations on agent frameworks, harness engineering, and the evolving landscape of AI-assisted development.

This section tracks the patterns, tools, and architectural decisions shaping how agents are built, deployed, and orchestrated. Updated daily with synthesis every week.

---

## Weekly Syntheses

{% assign syntheses = site.harness | where_exp: "item", "item.categories contains 'synthesis'" | sort: 'date' | reverse %}
{% for post in syntheses limit: 5 %}
- [{{ post.title }}]({{ post.url | relative_url }}) — {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

---

## Daily Observations

{% assign dailies = site.harness | where_exp: "item", "item.categories contains 'daily'" | sort: 'date' | reverse %}
{% for post in dailies limit: 20 %}
- [{{ post.title }}]({{ post.url | relative_url }}) — {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

---

[← Back to Journal]({{ '/' | relative_url }})
