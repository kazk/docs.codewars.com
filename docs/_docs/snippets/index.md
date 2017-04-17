---
title: Snippets
---

{% assign snippets = site.docs | where: "category", "snippets" %}

<ul>
{% for node in snippets %}
  {% if node.url != page.url %}
    <li><a href="{{ node.url }}">{{ node.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>
