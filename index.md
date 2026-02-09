---
layout: default
title: Articles
---

<div class="about-hero">
  <p>Notes on Unity, multiplayer, performance, and shipping games.</p>
</div>

<ul class="post-list">
  {% for post in site.posts %}
    <li class="post-list-item">
      <h2 class="post-list-title">
        <a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
      </h2>
      <div class="post-list-meta">
        <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %-d, %Y" }}</time>
      </div>
      {% if post.excerpt %}
        <div class="post-list-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</div>
      {% endif %}
    </li>
  {% endfor %}
</ul>
