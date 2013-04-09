---
layout: default
title: Posts
---
{% for i in site.posts %}
    {% if i.old %}
- {{ i.date | date_to_string }} - {{ i.title }}<br />
  {{ i.description }}
    {% else %}
- {{ i.date | date_to_string }} - [{{ i.title }}]({{ i.url }})<br />
  {{ i.description }}
    {% endif %}
{% endfor %}
