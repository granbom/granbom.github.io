---
layout: home
permalink: /
title: Hem
description: En site om lite av varje
---

## Artiklar

<div class="row">
{% for post in site.posts %}
 {% assign mod3 = forloop.index | modulo: 3 %}
  {% if mod3 == 0 %}</div><div class="row">{% endif %}
<div class="col-md-6 col-xl-4">
<div class="card">
  <div class="card-body">
    <h5 class="card-title">{{ post.title }}</h5>
    <h6 class="card-subtitle mb-2 text-muted">{{ post.date | date: "%Y-%m-%d" }}</h6>
    <p class="card-text">{{ post.excerpt }}</p>
    <a href="{{ post.url }}" class="btn btn-primary">Läs mer</a>
  </div>
</div>
</div>
{% endfor %}
</div>