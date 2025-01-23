---
layout: page
title: Черновики
permalink: /prose/drafts/
---
### Черновики

{% for story in site.prose %}
    {% if story.categories contains 'drafts' %}
* <a href="{{ site.url }}{{ site.baseurl }}{{ story.url }}">{{ story.title }}</a>
    {% endif %}
{% endfor %}
