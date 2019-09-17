---
layout: page
permalink: /teknik/git/
title: git
icon: fas fa-code-branch
description: En sida om git
---

## GitHub/Bitbucket

### Fork

Gör du i webbinterfacet. Sedan klonar du din fork till din dator.

```shell
git clone https://github.com/your-username/forked-repo.git
```

### Lägg till upstream

```shell
git remote add upstream https://github.com/user/repo.git
```

### Hålla en fork uppdaterad

```shell
git fetch upstream
git rebase upstream/master
git push origin
```
