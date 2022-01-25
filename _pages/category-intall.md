---
title: "Install"
permalink: /install/
layout: archive
---

{% assign posts = site.categories.install %}
{% for post in posts %}
	{% include archive-single.html type=page.entries_layout %}
{% endfor%}