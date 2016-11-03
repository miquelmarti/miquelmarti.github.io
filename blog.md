---
layout: default
title: Blog
permalink: blog
---

{% for post in site.posts %}
{{ post.date | date: "%b %-d, %Y" }}
[{{ post.title | escape }}]({{ post.url | prepend: site.baseurl }})
{% endfor %}
