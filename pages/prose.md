---
layout: page
title: Проза
permalink: /prose/
---

### Проза

{% for post in site.posts %}
    {% if post.categories contains 'prose' %}
* <a href="{{ site.url }}{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
    {% endif %}
{% endfor %}

