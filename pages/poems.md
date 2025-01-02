---
layout: page
title: Стихи
permalink: /poems/
---

### Стихи

{% for poem in site.poems %}
    {% if poem.categories contains 'poems' %}
* <a href="{{ site.url }}{{ site.baseurl }}{{ poem.url }}">{{ poem.title }}</a>
    {% endif %}
{% endfor %}

