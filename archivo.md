---
layout: page
title: Archivo
permalink: /archivo/
---

<div class="archive-list">
  {% for post in site.posts %}
    {% assign current_year = post.date | date: "%Y" %}
    {% if current_year != previous_year %}
      {% unless forloop.first %}</ol>{% endunless %}
      <h2>{{ current_year }}</h2>
      <ol>
      {% assign previous_year = current_year %}
    {% endif %}
      <li>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
        <span>{% include date-es.html date=post.date %}</span>
      </li>
    {% if forloop.last %}</ol>{% endif %}
  {% endfor %}
</div>
