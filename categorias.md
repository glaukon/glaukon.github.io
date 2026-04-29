---
layout: page
title: Categorías
permalink: /categorias/
---

<div class="taxonomy-cloud">
  {% assign categories = site.categories | sort %}
  {% for category in categories %}
    <a href="#{{ category[0] | slugify }}">{{ category[0] }} <span>{{ category[1].size }}</span></a>
  {% endfor %}
</div>

<div class="taxonomy-sections">
  {% for category in categories %}
    <section id="{{ category[0] | slugify }}">
      <h2>{{ category[0] }}</h2>
      <ol>
        {% for post in category[1] %}
          <li>
            <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
            <span>{% include date-es.html date=post.date %}</span>
          </li>
        {% endfor %}
      </ol>
    </section>
  {% endfor %}
</div>
