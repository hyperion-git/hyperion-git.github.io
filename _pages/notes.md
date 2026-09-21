---
layout: page
title: notes
permalink: /notes/
description: Short technical notes — derivations, conventions, and things worth writing down once.
nav: true
nav_order: 3
---

<!-- _pages/notes.md -->

{% assign notes = site.notes | sort: "date" | reverse %}

{% if notes.size == 0 %}

<p class="text-muted">Nothing here yet.</p>

{% else %}

<div class="post">
  <ul class="post-list">
    {% for note in notes %}
      <li>
        <h3><a class="post-title" href="{{ note.url | relative_url }}">{{ note.title }}</a></h3>
        {% if note.description %}<p>{{ note.description }}</p>{% endif %}
        <p class="post-meta">
          {% if note.date %}{{ note.date | date: '%B %d, %Y' }}{% endif %}
          {% if note.tags and note.tags.size > 0 %}
            &nbsp; &middot; &nbsp;
            {% for tag in note.tags %}<i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}{% unless forloop.last %}&nbsp;{% endunless %}{% endfor %}
          {% endif %}
        </p>
      </li>
    {% endfor %}
  </ul>
</div>

{% endif %}
