---
layout: default
title: About
---

<div class="page-wrapper">
<div class="hero-section">
  <div class="intro-card">
    <div class="intro-content">
      <div class="profile-image">
        <img src="/assets/images/iwonderwhothisis.jpg" alt="Alex"/>
      </div>
      <div class="intro-text">
        <h1>Hey, I'm Alex 👋</h1>
        <p>I'm a third-year Engine/Tools programming student at <a href="https://buas.nl/">Breda University of Applied Sciences</a>, passionate about building the technology that powers games. I am also interested in Graphics Programming.</p>
        <p class="internship-note">I'm looking for an internship starting September 2026.</p>
      </div>
    </div>

    <div class="skills-section">
      <h2>Skills & Technologies</h2>

      <div class="skills-grid">
        <div class="skill-category">
          <h3>Programming Languages</h3>
          <div class="skill-icons">
            <div class="skill-item">
              <img src="/assets/images/c.svg" alt="C"/>
              <span>C</span>
            </div>
            <div class="skill-item">
              <img src="/assets/images/cplusplus.svg" alt="C++"/>
              <span>C++</span>
            </div>
            <div class="skill-item">
              <img src="/assets/images/rust.svg" alt="Rust"/>
              <span>Rust</span>
            </div>
            <div class="skill-item">
              <img src="/assets/images/python.svg" alt="Python"/>
              <span>Python</span>
            </div>
          </div>
        </div>

        <div class="skill-category">
          <h3>Game Engines</h3>
          <div class="skill-icons">
            <div class="skill-item">
              <img src="/assets/images/unrealengine.svg" alt="Unreal Engine 5"/>
              <span>Unreal Engine 5</span>
            </div>
            <div class="skill-item">
              <img src="/assets/images/godotengine.svg" alt="Godot"/>
              <span>Godot</span>
            </div>
          </div>
        </div>
      </div>

      <div class="skill-category skill-category-full">
        <h3>Tools</h3>
        <div class="skill-icons">
          <div class="skill-item">
            <img src="/assets/images/git.svg" alt="Git"/>
            <span>Git</span>
          </div>
          <div class="skill-item">
            <img src="/assets/images/perforce.svg" alt="Perforce"/>
            <span>Perforce</span>
          </div>
          <div class="skill-item">
            <img src="/assets/images/jenkins.svg" alt="Jenkins"/>
            <span>Jenkins</span>
          </div>
          <div class="skill-item">
            <img src="/assets/images/confluence.svg" alt="Confluence"/>
            <span>Confluence</span>
          </div>
          <div class="skill-item">
            <img src="/assets/images/jirasoftware.svg" alt="Jira"/>
            <span>Jira</span>
          </div>
          <div class="skill-item">
            <svg role="img" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="#1a1a1a" width="48" height="48">
              <title>Visual Studio</title>
              <path d="M17.583.063a1.5 1.5 0 00-1.032.392 1.5 1.5 0 00-.001 0A.88.88 0 0016.5.5L8.528 9.316 3.875 5.5l-.407-.35a1 1 0 00-1.024-.154 1 1 0 00-.012.005l-1.817.75a1 1 0 00-.047.028A.995.995 0 000 6.668v10.666a1 1 0 00.568.9l1.817.75a1 1 0 00.854-.006l.408-.35 4.653-3.815 7.973 8.815a1.5 1.5 0 00.072.065 1.5 1.5 0 001.032.392 1.5 1.5 0 001.5-1.5v-21a1.5 1.5 0 00-1.5-1.5 1.5 1.5 0 00-.093.003z"/>
            </svg>
            <span>Visual Studio</span>
          </div>
          <div class="skill-item">
            <svg role="img" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="#1a1a1a" width="48" height="48">
              <title>Visual Studio Code</title>
              <path d="M23.15 2.587L18.21.21a1.494 1.494 0 0 0-1.705.29l-9.46 8.63-4.12-3.128a.999.999 0 0 0-1.276.057L.327 7.261A1 1 0 0 0 .326 8.74L3.899 12 .326 15.26a1 1 0 0 0 .001 1.479L1.65 17.94a.999.999 0 0 0 1.276.057l4.12-3.128 9.46 8.63a1.492 1.492 0 0 0 1.704.29l4.942-2.377A1.5 1.5 0 0 0 24 20.06V3.939a1.5 1.5 0 0 0-.85-1.352zm-5.146 14.861L10.826 12l7.178-5.448v10.896z"/>
            </svg>
            <span>VS Code</span>
          </div>
          <div class="skill-item">
            <img src="/assets/images/blender.svg" alt="Blender"/>
            <span>Blender</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="featured-projects-sidebar">
    <h2>Featured Projects</h2>
    <div class="projects-compact">
      {% for project in site.projects %}
      {% if project.featured %}
      <article class="project-card-compact">
        {% if project.image %}
        <a href="{{ project.url }}" class="project-image-compact">
          <img src="{{ project.image | relative_url }}" alt="{{ project.title }}">
        </a>
        {% endif %}
        <div class="project-content-compact">
          <h3><a href="{{ project.url }}">{{ project.title }}</a></h3>
          
          {% if project.role %}
          <p class="project-role">{{ project.role }}</p>
          {% endif %}
          
          {% if project.duration or project.team_size %}
          <div class="project-meta-compact">
            {% if project.duration %}<span class="meta-item-compact"><strong>Duration:</strong> {{ project.duration }}</span>{% endif %}
            {% if project.team_size %}<span class="meta-item-compact"><strong>Team:</strong> {{ project.team_size }}</span>{% endif %}
          </div>
          {% endif %}
          
          <p class="project-desc">{{ project.description | default: project.excerpt | strip_html | truncatewords: 15 }}</p>
          
          {% if project.responsibilities %}
          <div class="project-responsibilities-compact">
            <h4>Key Responsibilities</h4>
            <ul>
              {% for responsibility in project.responsibilities limit:2 %}
                <li>{{ responsibility }}</li>
              {% endfor %}
            </ul>
          </div>
          {% endif %}
          
          {% if project.technologies %}
          <div class="project-tags-compact">
            {% for tech in project.technologies limit:4 %}
            <span class="tag-compact">{{ tech }}</span>
            {% endfor %}
          </div>
          {% endif %}
        </div>
      </article>
      {% endif %}
      {% endfor %}
    </div>
  </div>
</div>

<div class="blog-section">
  <h2>Featured Blog Posts</h2>
  <div class="blog-grid">
{% assign featured_posts = site.posts | where: "featured", true %}
{% if featured_posts.size > 0 %}
  {% for post in featured_posts limit:3 %}
    <article class="post-card">
      {% if post.image %}
        <a href="{{ post.url }}" class="post-card-image">
          <img src="{{ post.image | relative_url }}" alt="{{ post.title }}">
        </a>
      {% endif %}
      
      <div class="post-card-content">
        <div class="post-card-meta">
          <time datetime="{{ post.date | date_to_xmlschema }}">
            {{ post.date | date: "%B %-d, %Y" }}
          </time>
          {% if post.read_time %}
            <span class="read-time">{{ post.read_time }} min read</span>
          {% endif %}
        </div>
        
        <h2 class="post-card-title">
          <a href="{{ post.url }}">{{ post.title }}</a>
        </h2>
        
        <p class="post-card-excerpt">
          {{ post.excerpt | strip_html | truncatewords: 30 }}
        </p>
        
        {% if post.tags %}
          <div class="post-card-tags">
            {% for tag in post.tags %}
              <span class="tag">{{ tag }}</span>
            {% endfor %}
          </div>
        {% endif %}
      </div>
    </article>
  {% endfor %}
{% else %}
  {% for post in site.posts limit:3 %}
    <article class="post-card">
      {% if post.image %}
        <a href="{{ post.url }}" class="post-card-image">
          <img src="{{ post.image | relative_url }}" alt="{{ post.title }}">
        </a>
      {% endif %}
      
      <div class="post-card-content">
        <div class="post-card-meta">
          <time datetime="{{ post.date | date_to_xmlschema }}">
            {{ post.date | date: "%B %-d, %Y" }}
          </time>
          {% if post.read_time %}
            <span class="read-time">{{ post.read_time }} min read</span>
          {% endif %}
        </div>
        
        <h2 class="post-card-title">
          <a href="{{ post.url }}">{{ post.title }}</a>
        </h2>
        
        <p class="post-card-excerpt">
          {{ post.excerpt | strip_html | truncatewords: 30 }}
        </p>
        
        {% if post.tags %}
          <div class="post-card-tags">
            {% for tag in post.tags %}
              <span class="tag">{{ tag }}</span>
            {% endfor %}
          </div>
        {% endif %}
      </div>
    </article>
  {% endfor %}
{% endif %}
  </div>
</div>