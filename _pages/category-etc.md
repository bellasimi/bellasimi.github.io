---
title: "ETC"
permalink: /etc/
layout: archive
---

{% assign posts = site.categories.etc %}
{% for post in posts %}
	{% include archive-single.html type=page.entries_layout %}
{% endfor%}