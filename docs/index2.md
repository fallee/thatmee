---
title:index2
---
{% for page in site.refs %}
* [{{page.title}}]({{page.url}}){{page.name}}
{% endfor %}
