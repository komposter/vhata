---
layout: page
title: Prose
permalink: /prose/
---

#### Prose

{% for post in site.posts %}
    {% if post.categories contains 'prose' %}
* <a href="{{ site.url }}{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
    {% endif %}
{% endfor %}

