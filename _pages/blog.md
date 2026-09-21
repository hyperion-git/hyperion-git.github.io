---
layout: page
title: Blog
permalink: /blog/
profile_picture: blog.jpg # page picture in the round slot top-right (file in assets/img/)
description: Occasional longer pieces. Notes are for the technical or the short ones.
nav: true
nav_order: 4
pagination:
  enabled: true
  collection: posts
  permalink: /page/:num/
  per_page: 10
  sort_field: date
  sort_reverse: true
  trail:
    before: 1 # The number of links before the current page
    after: 3 # The number of links after the current page
---

<!-- _pages/blog.md — one entry per post, separated by a rule that carries the date -->

{% if page.pagination.enabled %}
{% assign postlist = paginator.posts %}
{% else %}
{% assign postlist = site.posts %}
{% endif %}

<div class="entry-list">
{% if postlist.size == 0 %}
  <h2 class="entry-date">&nbsp;</h2>
  <p class="text-muted">Nothing here yet.</p>
{% endif %}
{% for post in postlist %}
  {% assign read_time = post.content | number_of_words | divided_by: 180 | plus: 1 %}
  <div class="entry">
    <h2 class="entry-date">{{ post.date | date: "%B %-d, %Y" }}</h2>
    <h3>
      {% if post.redirect == blank %}
        <a class="entry-title" href="{{ post.url | relative_url }}">{{ post.title }}</a>
      {% elsif post.redirect contains '://' %}
        <a class="entry-title" href="{{ post.redirect }}" target="_blank">{{ post.title }}</a>
      {% else %}
        <a class="entry-title" href="{{ post.redirect | relative_url }}">{{ post.title }}</a>
      {% endif %}
    </h3>
    {% if post.description %}<p class="serif-prose">{{ post.description }}</p>{% endif %}
    <p class="entry-meta">
      {{ read_time }} min read
      {% if post.tags and post.tags.size > 0 %}
        &nbsp;&middot;&nbsp;
        {% for tag in post.tags %}<a href="{{ tag | slugify | prepend: '/blog/tag/' | relative_url }}"><i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}</a>{% unless forloop.last %}&nbsp; {% endunless %}{% endfor %}
      {% endif %}
    </p>
  </div>
{% endfor %}
</div>

{% if page.pagination.enabled %}
{% include pagination.liquid %}
{% endif %}
