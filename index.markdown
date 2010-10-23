---
title: "&#9998; Tennety Time! | Chandu Tennety's Blog"
layout: blog
---

{% for post in site.posts | limit: 2 %}
<div class="blog_post">
<h1><a href="{{ post.url }}">{{ post.title }}</a></h1>

<span class="article_date dark_blue">{{ post.date | date: "%d %B %Y" }}</span>, <span class="author">{{ post.author }}</span><br />
<br />

{{ post.content }}
</div><!-- /blog_post -->
{% endfor %}

