---
title: "Error"
permalink: /error/
layout: archive
---

{% assign posts = site.categories.error %}
{% for post in posts %}
	{% include archive-single.html type=page.entries_layout %}
{% endfor%}