---
layout: default
title: Posts
aliases: ['/web/all_posts.html']
sitemap: {priority: 0.9, changes: weekly}
---
{% for i in site.posts %}
{{ i.date | date_to_string }} - [{{ i.title }}]({{ i.url }})<br />
{{ i.description }}
{% endfor %}

<a href="http://lurch.barbon.org/php/mixtureshare.cgi"></a>
