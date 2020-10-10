---
layout: archive
title: "Portfolio and projects"
permalink: /portfolio/
author_profile: true
---
<div class="grid__wrapper">
    {% for post in site.posts %}
        {% if post.categories contains 'project' %}
            {% include archive-single.html type="grid" %}
        {% endif %}
    {% endfor %}
</div>
