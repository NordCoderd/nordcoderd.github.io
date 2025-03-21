---
layout: default
title: "Infrastructure as Code (IaC) Security Linter"
permalink: /infrastructure-security
tags: ["navbar"]
---
[![JetBrains Plugin Downloads](https://img.shields.io/jetbrains/plugin/d/dev.protsenko.security-linter)](https://plugins.jetbrains.com/plugin/25413-infrastructure-security)
[![JetBrains Plugin Rating](https://img.shields.io/jetbrains/plugin/r/rating/dev.protsenko.security-linter)](https://plugins.jetbrains.com/plugin/25413-infrastructure-security-linter/reviews)
[![JetBrains Plugin Version](https://img.shields.io/jetbrains/plugin/v/dev.protsenko.security-linter)](https://plugins.jetbrains.com/plugin/25413-infrastructure-security-linter/versions)
[![GitHub Repo stars](https://img.shields.io/github/stars/NordCoderd/infrastructure-security)](https://github.com/NordCoderd/infrastructure-security)

Welcome to [Infrastructure as Code (IaC) Security Linter](https://github.com/NordCoderd/infrastructure-security) documentation site.

You could download plugin from [JetBrains marketplace](https://plugins.jetbrains.com/plugin/25413-infrastructure-security-linter)

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
