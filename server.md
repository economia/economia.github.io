---
layout: default
title: Příspěvky v kategorii Server
---

<ul id="archive">
{% for post in site.categories.server %}
<li><a href="{{ post.url }}">{{post.title}}</a> <abbr>{{post.date | date_to_string }}</abbr></li>
{% endfor %}
</ul>