---
layout: default
---

# Blog

{% for post in site.posts %}
- {{ post.date | date: "%d.%m.%Y" }} [**{{ post.title }}**]({{ post.url }})

  {{ post.content | strip_html | truncatewords:75 }}

{% endfor %}