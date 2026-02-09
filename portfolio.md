---
layout: default
title: Portfolio
permalink: /portfolio/
---

<h1>Portfolio</h1>

<p>Selected projects showcasing shipped and in-progress games, along with relevant technical experience.</p>

<div class="portfolio-grid">
  {% for project in site.data.portfolio %}
    <div class="portfolio-item">
      <h2 class="portfolio-title">{{ project.title }}</h2>
      <p class="portfolio-role">{{ project.subtitle }} • {{ project.role }}</p>
      
      <div class="portfolio-stack">
        {% for tech in project.stack %}
          <span class="portfolio-tag">{{ tech }}</span>
        {% endfor %}
      </div>
      
      <div class="portfolio-description">
        <ul>
          {% for item in project.description %}
            <li>{{ item }}</li>
          {% endfor %}
        </ul>
      </div>
      
      {% if project.links %}
        <div class="portfolio-links">
          {% if project.links.store %}
            <a href="{{ project.links.store }}" target="_blank" rel="noopener">Store Page</a>
          {% endif %}
          {% if project.links.trailer %}
            <a href="{{ project.links.trailer }}" target="_blank" rel="noopener">Trailer</a>
          {% endif %}
          {% if project.links.github %}
            <a href="{{ project.links.github }}" target="_blank" rel="noopener">GitHub</a>
          {% endif %}
        </div>
      {% endif %}
    </div>
  {% endfor %}
</div>
