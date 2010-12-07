---
title: Post Archives
layout: home
---

<div class="post-list">
	<h3>All posts:</h3>
{% for post in site.posts %}
	<div class='entry'>
		<div class='post-header'><a href="{{ post.url }}">{{ post.title }}</a><div class='metadata'>on {{ post.date | date: "%d %B %Y" }}</div></div>
		<div class='excerpt'>
		{% if post.excerpt %}
			{{ post.excerpt | textilize | truncatewords: 30 }}
		{% endif %}
		</div>
	</div>
{% endfor %}
</div>
