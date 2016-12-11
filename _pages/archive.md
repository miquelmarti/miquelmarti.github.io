---
layout: archive
title: Archive
permalink: /archive/
---
{% include base_path %}
{% for post in site.posts %}
  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  <h2 id="{{ year | slugify }}" class="archive__subtitle">{{ year }}</h2>
  {% include archive-single.html %}
{% endfor %}
