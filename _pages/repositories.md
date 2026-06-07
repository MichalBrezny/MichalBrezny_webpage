---
layout: page
permalink: /repositories/
title: repositories
description: Code and open resources I maintain on GitHub
nav: true
nav_order: 9
---

Code and open resources I maintain on GitHub. To add more, edit the `github_users` and `github_repos` lists in `_data/repositories.yml`.

{% if site.data.repositories.github_users %}

## Profile

<ul>
  {% for user in site.data.repositories.github_users %}
  <li><a href="https://github.com/{{ user }}">github.com/{{ user }}</a></li>
  {% endfor %}
</ul>
{% endif %}

{% if site.data.repositories.github_repos %}

## Repositories

<ul>
  {% for repo in site.data.repositories.github_repos %}
  <li><a href="https://github.com/{{ repo }}">{{ repo }}</a></li>
  {% endfor %}
</ul>
{% endif %}
