---
layout: page
title: Notes
permalink: /notes/
profile_picture: notes.jpg # page picture in the round slot top-right (file in assets/img/)
description: "Short technical notes: derivations, conventions, and things worth writing down once."
nav: true
nav_order: 3
---

<!-- _pages/notes.md — one entry per note, separated by a rule that carries the date -->

{% assign notes = site.notes | sort: "date" | reverse %}

<div class="entry-list">
{% if notes.size == 0 %}
  <h2 class="entry-date">&nbsp;</h2>
  <p class="text-muted">Nothing here yet.</p>
{% endif %}
{% for note in notes %}
  <div class="entry">
    <h2 class="entry-date">{{ note.date | date: "%B %-d, %Y" }}</h2>
    <h3><a class="entry-title" href="{{ note.url | relative_url }}">{{ note.title }}</a></h3>
    {% if note.description %}<p class="serif-prose">{{ note.description }}</p>{% endif %}
    {% if note.tags and note.tags.size > 0 %}
      <p class="entry-meta">{% for tag in note.tags %}<i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}{% unless forloop.last %}&nbsp; {% endunless %}{% endfor %}</p>
    {% endif %}
  </div>
{% endfor %}
</div>
