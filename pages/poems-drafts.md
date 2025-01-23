---
layout: page
title: Черновики
permalink: /poems/drafts/
---
### Черновики

{% for poem in site.poems %}
    {% if poem.categories contains 'drafts' %}
* <a href="{{ site.url }}{{ site.baseurl }}{{ poem.url }}">{{ poem.title }}</a>
    {% endif %}
{% endfor %}
