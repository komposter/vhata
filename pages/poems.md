---
layout: page
title: Стихи
permalink: /poems/
---

### Стихи

{% for post in site.posts %}
    {% if post.categories contains 'poems' %}
* <a href="{{ site.url }}{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
    {% endif %}
{% endfor %}

