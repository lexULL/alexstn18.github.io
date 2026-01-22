---
layout: page
title: Projects
permalink: /projects/
---

<div class="projects-grid">
  {% for project in site.projects %}
    <article class="project-card">
      {% if project.image %}
        <a href="{{ project.url }}" class="project-image">
          <img src="{{ project.image | relative_url }}" alt="{{ project.title }}">
        </a>
      {% endif %}
      
      <div class="project-content">
        <h2 class="project-title">
          <a href="{{ project.url }}">{{ project.title }}</a>
        </h2>
        
        <p class="project-description">{{ project.description | default: project.excerpt | strip_html | truncatewords: 30 }}</p>
        
        {% if project.tags %}
          <div class="project-tags">
            {% for tag in project.tags %}
              <span class="tag">{{ tag }}</span>
            {% endfor %}
          </div>
        {% endif %}
      </div>
    </article>
  {% endfor %}
</div>