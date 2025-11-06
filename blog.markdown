---
layout: page
title: Blog
permalink: /blog/
---

<div class="blog-grid">
  {% for post in site.posts %}
    <div class="post-card">
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p>{{ post.excerpt }}</p>
      {% if post.tags %}
        <div class="tags">
          {% for tag in post.tags %}
            <span class="tag">{{ tag }}</span>
          {% endfor %}
        </div>
      {% endif %}
    </div>
  {% endfor %}
</div>