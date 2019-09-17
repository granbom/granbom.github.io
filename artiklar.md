---
layout: page
permalink: /artiklar/
title: Artiklar
icon: far fa-newspaper
description: Alla artiklar
---

<div class="list-group">
{% for post in site.posts %}
<a href="{{ post.url }}" class="list-group-item list-group-item-action flex-column align-items-start">
    <div class="d-flex w-100 justify-content-between">
      <h5 class="mb-1">{{ post.title }}</h5>
      <small class="text-muted">{{ post.date | date: "%Y-%m-%d" }}</small>
    </div>
    <p class="mb-1">{{ post.excerpt | remove: '<p>' | remove: '</p>' }}</p>
    <small class="text-muted">{{ post.author }}</small>
</a>
{% endfor %}
</div>