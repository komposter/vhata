---
layout: page
title: Проза
permalink: /prose/
---

### Проза

{% for story in site.prose %}
    {% if story.categories contains 'prose' %}
* <a href="{{ site.url }}{{ site.baseurl }}{{ story.url }}">{{ story.title }}</a>
    {% endif %}
{% endfor %}

