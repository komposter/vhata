---
layout: page
title: Valentin Hata
permalink: /
---

### A page in memory of one good man

#### Random poem

{% assign random_poem = site.posts | where: "categories", "poems" | sample %}
<div style="font-family: Arial, sans-serif; line-height: 1.6; font-size: 16px;">
  {{ random_poem.content }}
</div>

<br /><br />
