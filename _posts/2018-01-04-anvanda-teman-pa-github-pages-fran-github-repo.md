---
title: "Använda teman på Github pages från Github repo"
date: 2018-01-04
categories: github
---
Denna sida använder ett tema som jag gjort själv som använder sig av bootstrap 4.

Källkoden till temat finns här: [granbom/jekyll-theme-bootstrap4-navbar-cdn](https://github.com/granbom/jekyll-theme-bootstrap4-navbar-cdn)
För att använda detta tema till Github pages så kan du i `_config.yml` ta bort theme och sätta remote_theme så här:

```yml
remote_theme: granbom/jekyll-theme-bootstrap4-navbar-cdn
```

Då kommer detta tema att användas istället för de inbyggda som gh-pages tillhandahåller.
