---
title: "Java"
permalink: /java/
layout: archive
---

{% assign posts = site.categories.java %}
{% for post in posts %}
	{% include archive-single.html type=page.entries_layout %}
{% endfor%}