---
layout: default
title: Home
head: index
aliases: ['/web/3/index.html', '/web/index.html', '/web', '/web/']
sitemap: {priority: 0.9, changes: weekly}
---
## Current position

Since May 2013 I work for Booking.com as a full-time employee.

## Bio sketch

I was born in Treviso (Italy, near Venice) January the 8th, 1979.

I obtained the "Laurea Specialistica in Informatica",
roughly equivalent to a MSc in Computer Science, October the 10th, 2003.

I work in IT as a developer. In my free time (which is becoming
less and less...) I participate to some Open Source projects.

[Curriculum Vitae](mbarbon_en.pdf) ([Italian version](mbarbon_it.pdf))

## Contact

You can mail me at [mattia@barbon.org](mailto:mattia@barbon.org) or
[mbarbon@cpan.org](mailto:mbarbon@cpan.org).

*Skype*: mattia.barbon

*Jabber/Google Talk*: mattia.barbon@jabber.org

*Yahoo! Messenger*: mattiabarbon

*MSN Messenger*: mbarbon@cpan.org

## Last posts

{% for i in site.posts limit:4 %}
{{ i.date | date_to_string }} - [{{ i.title }}]({{ i.url }})<br />
{{ i.description }}
{% endfor %}

[All posts](/all-posts.html)

<div style="display: none;"><a href="http://lurch.barbon.org/php/mixtureshare.cgi">abashed-lost</a></div>
