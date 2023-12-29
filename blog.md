---
layout: v2
title: Blog
bodyclass: blog-page
---

## Leaflet Developer Blog 0.x archive

Archived posts from the Leaflet developers before 1.x times.

---

{% for post in site.posts %}
<div class="clearfix">
	<div class="post-date">
		{{ post.date | date_to_string }}
	</div>
	<div class="post-info">
		<h3 class="post-title"><a href="{{ post.url | replace_first: '/', '' }}">{{ post.title }}</a></h3>
		<p>{{ post.description }} <span class="quiet">&hellip;</span></p>
	</div>
</div>
{% unless forloop.last %}<hr />{% endunless %}
{% endfor %}
