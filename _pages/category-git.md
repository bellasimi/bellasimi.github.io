---
title: "Git"
permalink: /git/
layout: archive
---

{% assign posts = site.categories.git %}
{% for post in posts %}
	{% include archive-single.html type=page.entries_layout %}
{% endfor%}