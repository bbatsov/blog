---
layout: default
title: Blogs posts
---

{% for post in site.posts limit:5 %}
## [{{ post.title }}]({{ post.url }})
{{ post.content }}
<div style="font-style: italic; color: #7f9f7f;">Posted on {{ post.date | date_to_string }} by Bozhidar.</div>

[Comments]({{ post.url }}#disqus_thread)
{% endfor %}
