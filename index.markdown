---
title: "Tennety Time! | Chandu Tennety's Blog"
layout: blog
---

{% for post in site.posts | limit: 2 %}
<div class="post">
<h1><a href="{{ post.url }}">{{ post.title }}</a></h1>

<span class="article_date dark_blue">{{ post.date | date: "%d %B %Y" }}</span>, <span class="author">{{ post.author }}</span>

			<a href="{{ post.url }}#disqus_thread">Comments</a>

<br />
<br />

{{ post.content }}
</div><!-- /blog_post -->
{% endfor %}

