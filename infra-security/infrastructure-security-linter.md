---
layout: default
title: "Infrastructure Security Linter"
permalink: /infrastructure-security
tags: ["navbar"]
---
[![JetBrains Plugin Version](https://img.shields.io/jetbrains/plugin/v/dev.protsenko.security-linter)](https://plugins.jetbrains.com/plugin/25413-infrastructure-security)
[![JetBrains Plugin Downloads](https://img.shields.io/jetbrains/plugin/d/dev.protsenko.security-linter)](https://plugins.jetbrains.com/plugin/25413-infrastructure-security)

Welcome to [Infrastructure Security Linter](https://github.com/NordCoderd/infrastructure-security) documentation site.

On that page you could find information about plugin inspections, what problem he could find and about included features.

## Security

{% for post in site.pages %}
{% if post.tags contains 'security' %}
### [{{ post.title }}]({{ post.url }})
{% endif %}
{% endfor %}

## Maintainability

{% for post in site.pages %}
{% if post.tags contains 'maintainability' %}
### [{{ post.title }}]({{ post.url }})
{% endif %}
{% endfor %}
