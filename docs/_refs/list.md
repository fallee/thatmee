---
title: list
---
{% for page in site.refs %}
* [{{ page.title }}]({{ page.url }})
{% endfor %}
