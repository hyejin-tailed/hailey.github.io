---
layout: archive
permalink: memory-leak/
title : "Memory Leaks"
author_profile: true
header:
  image: "_pages/_images/1.0.jpg"
---

See? It was just simple segue between profile tab in main.async thread using Grand Central Dispatch.

{% include group-by-array collection=site.post field="tags" %}

{% for tag in group names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }} class="archive_subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor%}
