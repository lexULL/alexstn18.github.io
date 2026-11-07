---
layout: default
title: .home
---

<div class="home-wrapper">

  <section class="home-section">
    <h2 class="home-section-title">.featured-projects</h2>
    <div class="projects-compact">
      {% assign sorted_projects = site.projects | sort: "order" %}
      {% for project in sorted_projects %}
      {% if project.featured %}
      <article class="project-card-compact">
        {% if project.image %}
        <a href="{{ project.url }}" class="project-image-compact">
          <img src="{{ project.image | relative_url }}" alt="{{ project.title }}" loading="lazy">
        </a>
        {% endif %}
        <div class="project-content-compact">
          <div class="project-title-row">
            <h3><a href="{{ project.url }}">{{ project.title }}</a></h3>
            <div class="project-external-links">
              {% if project.github %}
              <a href="{{ project.github }}" target="_blank" rel="noopener" class="project-external-link" aria-label="GitHub">
                <img src="{{ '/assets/images/github.svg' | relative_url }}" alt="GitHub"/>
              </a>
              {% endif %}
              {% if project.itch %}
              <a href="{{ project.itch }}" target="_blank" rel="noopener" class="project-external-link" aria-label="itch.io">
                <img src="{{ '/assets/images/itchio.svg' | relative_url }}" alt="itch.io"/>
              </a>
              {% endif %}
            </div>
          </div>

          {% if project.duration or project.team_size %}
          <div class="project-meta-compact">
            {% if project.duration %}<span class="meta-item-compact"><strong>--duration=</strong>{{ project.duration }}</span>{% endif %}
            {% if project.team_size %}<span class="meta-item-compact"><strong>--team=</strong>{{ project.team_size }}</span>{% endif %}
          </div>
          {% endif %}

          <p class="project-desc">{{ project.summary | default: project.excerpt | strip_html | truncatewords: 20 }}</p>

          {% if project.responsibilities %}
          <div class="project-responsibilities-compact">
            <h4>${KEY_RESPONSIBILITIES}</h4>
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
    <div class="view-all-container">
      <a href="{{ '/projects/' | relative_url }}" class="view-all-btn">${ALL_PROJECTS}</a>
    </div>
  </section>

  <section class="home-section">
    <h2 class="home-section-title">.featured-blog-posts</h2>
    <div class="blog-grid">
      {% assign featured_posts = site.posts | where: "featured", true %}
      {% assign posts_to_show = featured_posts.size | default: 0 %}
      {% if posts_to_show > 0 %}
        {% assign display_posts = featured_posts %}
      {% else %}
        {% assign display_posts = site.posts %}
      {% endif %}
      {% for post in display_posts limit:3 %}
      <article class="post-card">
        {% if post.image %}
        <a href="{{ post.url }}" class="post-card-image">
          <img src="{{ post.image | relative_url }}" alt="{{ post.title }}" loading="lazy">
        </a>
        {% endif %}
        <div class="post-card-content">
          <div class="post-card-meta">
            <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%-m-%-d-%-Y" }}</time>
            {% if post.read_time %}<span class="read-time">{{ post.read_time }} min read</span>{% endif %}
          </div>
          <h2 class="post-card-title"><a href="{{ post.url }}">{{ post.title }}</a></h2>
          <p class="post-card-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
          {% if post.tags %}
          <div class="post-card-tags">
            {% for tag in post.tags %}<span class="tag">{{ tag }}</span>{% endfor %}
          </div>
          {% endif %}
        </div>
      </article>
      {% endfor %}
    </div>
    <div class="view-all-container">
      <a href="{{ '/blog/' | relative_url }}" class="view-all-btn">${ALL_BLOGPOSTS}</a>
    </div>
  </section>

<br>

</div>