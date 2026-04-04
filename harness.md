---
layout: daily-agent
title: "Daily Agent 🤖"
subtitle: "Agent engineering, research, and enterprise adoption — updated daily"
permalink: /harness/
show_archive: true
show_categories: true
---

<link rel="stylesheet" href="{{ '/assets/css/daily-agent.css' | relative_url }}">

## Latest Article

{% assign latest = site.harness | where_exp: "item", "item.categories contains 'daily'" | sort: 'date' | reverse | first %}

{% if latest %}
<article class="featured-article">
  <h2><a href="{{ latest.url | relative_url }}">{{ latest.title }}</a></h2>
  <div class="post-meta">
    <time datetime="{{ latest.date | date_to_xmlschema }}">{{ latest.date | date: "%B %d, %Y" }}</time>
    {% if latest.categories %}
    <span class="post-categories">
      {% for category in latest.categories %}
      {% unless category == 'daily' or category == 'synthesis' %}
      <span class="category-tag">{{ category }}</span>
      {% endunless %}
      {% endfor %}
    </span>
    {% endif %}
  </div>
  <div class="article-excerpt">
    {{ latest.content | strip_html | truncatewords: 100 }}
  </div>
  <a href="{{ latest.url | relative_url }}" class="read-more">Read full article →</a>
</article>
{% else %}
<p>No articles yet. Check back soon!</p>
{% endif %}

<style>
.featured-article {
  padding: 2rem;
  background: #fafafa;
  border-radius: 8px;
  margin-bottom: 3rem;
}

.featured-article h2 {
  margin-top: 0;
  font-size: 1.8rem;
}

.featured-article h2 a {
  color: var(--color-text);
}

.featured-article h2 a:hover {
  color: var(--color-accent);
}

.article-excerpt {
  line-height: 1.7;
  color: var(--color-muted);
  margin: 1.5rem 0;
}

.read-more {
  display: inline-block;
  font-weight: 600;
  color: var(--color-accent);
  padding: 0.5rem 1rem;
  border: 2px solid var(--color-accent);
  border-radius: 6px;
  transition: all 0.2s;
}

.read-more:hover {
  background: var(--color-accent);
  color: white;
  border-bottom: 2px solid var(--color-accent);
}

@media (prefers-color-scheme: dark) {
  .featured-article {
    background: #2a2a2a;
  }
}
</style>
