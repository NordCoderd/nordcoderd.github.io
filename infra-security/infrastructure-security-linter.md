---
layout: default
title: "Infrastructure Security Linter"
permalink: /infrastructure-security
---

Welcome to [Infrastructure Security Linter](https://github.com/NordCoderd/infrastructure-security) documentation site.

On that page you could find information about plugin inspections, what problem he could find and about included features.

{% for post in site.pages %}
{% if post.tags contains 'plugin' %}
## [{{ post.title }}]({{ post.url }})
{% endif %}
{% endfor %}