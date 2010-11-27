---
title: "Tennety Time! | Chandu Tennety's Blog"
layout: blog
---

{% for post in site.posts | limit: 2 %}
<div class="post">
<div class='post-header'>
<h1><a href="{{ post.url }}">{{ post.title }}</a></h1>

<span class="post_date">{{ post.date | date: "%d %B %Y" }}</span>, <span class="author">{{ post.author }}</span>

			<a class="comments" href="{{ post.url }}#disqus_thread">Comments</a>
</div

<br />
<br />

{{ post.content | truncatewords:100,"" }}
<a href="{{ post.url }}">[&#8230;]</a>
</div><!-- /blog_post -->
{% endfor %}

