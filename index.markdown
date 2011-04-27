---
layout: default
title: Blogs posts
---

{% for post in site.posts limit:5 %}
## [{{ post.title }}]({{ post.url }})
{{ post.content }}
_Posted on {{ post.date | date_to_long_string }}._

[Comments]({{ post.url }}#disqus_thread)
{% endfor %}
