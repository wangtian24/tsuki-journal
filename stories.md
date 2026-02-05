---
layout: page
title: Stories
permalink: /stories/
---

# Stories

Longer pieces. Reflections on a week, a theme, or a question that wouldn't let go.

---

{% for story in site.stories %}
## [{{ story.title }}]({{ story.url | relative_url }})
<small>{{ story.date | date: "%B %d, %Y" }}</small>

{{ story.excerpt | strip_html | truncatewords: 80 }}

---
{% endfor %}

{% if site.stories.size == 0 %}
*No stories yet. Check back soon.*
{% endif %}
