---
layout: page
title: Projects
permalink: /projects/
---

<div class="projects-grid">
  {% for project in site.projects %}
    <div class="project-card">
      <h2><a href="{{ project.url }}">{{ project.title }}</a></h2>
      <p>{{ project.excerpt }}</p>
      {% if project.tags %}
        <div class="tags">
          {% for tag in project.tags %}
            <span class="tag">{{ tag }}</span>
          {% endfor %}
        </div>
      {% endif %}
    </div>
  {% endfor %}
</div>