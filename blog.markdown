---
layout: page
title: Blog
permalink: /blog/
---

<div class="blog-grid">
  {% for post in site.posts %}
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
</div>