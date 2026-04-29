---
layout: page
title: Tags
permalink: /tags/
---

<div class="taxonomy-cloud">
  {% assign tags = site.tags | sort %}
  {% for tag in tags %}
    <a href="#{{ tag[0] | slugify }}">{{ tag[0] }} <span>{{ tag[1].size }}</span></a>
  {% endfor %}
</div>

<div class="taxonomy-sections">
  {% for tag in tags %}
    <section id="{{ tag[0] | slugify }}">
      <h2>{{ tag[0] }}</h2>
      <ol>
        {% for post in tag[1] %}
          <li>
            <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
            <span>{% include date-es.html date=post.date %}</span>
          </li>
        {% endfor %}
      </ol>
    </section>
  {% endfor %}
</div>
