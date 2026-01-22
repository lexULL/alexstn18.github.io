---
layout: default
title: About
---

# Hey, I'm Alex 👋

I'm a third-year Engine/Tools programming student at [Breda University of Applied Sciences](https://buas.nl/), passionate about building the technology that powers games.

## What I Do
- Game engine development
- Tools programming
- Graphics programming

## Hobbies/Interests
- Demoscene
- Games
- Video Editing
- Music
- Travel

[Check out my projects](/projects/) or [read my blogposts](/blog/)

<strong>Below I've included some previews of the projects that I'm the most proud of. If you're interested in any of them make sure after reading the project card to click on it to read their full description!</strong>

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