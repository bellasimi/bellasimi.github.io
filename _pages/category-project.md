---
title: "Project"
permalink: /project/
layout: archive
---

{% assign posts = site.categories.project %}
{% for post in posts %}
{% include archive-single.html type=page.entries_layout %}
{% endfor%}
