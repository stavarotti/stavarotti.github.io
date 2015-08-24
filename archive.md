---
layout: default
title:  "archive"
permalink: /archive/
---

<h2>Previous musings</h2>

<ul class="post-list post-archives">
  {% for post in site.posts %}
    {% unless post.next %}
      <li class="group"><strong>{{ post.date | date: '%B %Y' }}</strong></li>
    {% else %}
      {% capture my %}{{ post.date | date: '%B %Y' }}{% endcapture %}
      {% capture nmy %}{{ post.next.date | date: '%B %Y' }}{% endcapture %}
      {% if my != nmy %}
        <li class="group"><strong>{{ post.date | date: '%B %Y' }}</strong></li>
      {% endif %}
    {% endunless %}

    <li class="post">
      <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      <span class="post-meta">{{ post.date | date: "%b %-d" }}</span>
    </li>
  {% endfor %}
</ul>