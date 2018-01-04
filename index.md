---
layout: default
permalink: /
title: Hem
description: En site om lite av varje
author: PG Granbom
---

## Granbom
---
Samlar lite av varje om teknik på ett ställe.

# Artiklar
{% for post in site.posts %}
<div class="card" style="width: 18rem;">
  <div class="card-body">
    <h5 class="card-title">{{ post.title }}</h5>
    <h6 class="card-subtitle mb-2 text-muted">{{ post.date | date: "%Y-%m-%d" }}</h6>
    <p class="card-text">{{ post.excerpt }}</p>
    <a href="{{ post.url }}" class="btn btn-primary">Läs mer</a>
  </div>
</div>  
{% endfor %}