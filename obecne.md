---
layout: default
title: Příspěvky v kategorii Obecně
---

<ul id="archive">
{% for post in site.categories.obecne %}
<li><a href="{{ post.url }}">{{post.title}}</a> <abbr>{{post.date | date_to_string }}</abbr></li>
{% endfor %}
</ul>