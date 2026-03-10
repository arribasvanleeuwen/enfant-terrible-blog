---
layout: page
title: "Daily videos about upcoming videogames"
---

<div class="posts-list">
  {% for post in site.posts %}
    <div class="post-card">
      
      <div class="post-thumb">
        <a href="{{ post.url }}">
          <img src="{{ post.thumbnail }}" alt="{{ post.title }}">
        </a>
      </div>

      <div class="post-excerpt-container">
        <h3>
          <a href="{{ post.url }}">{{ post.title }}</a>
        </h3>
        
        <div class="excerpt-text">
          {{ post.excerpt }}
        </div>

        <small class="post-date">{{ post.date | date: "%d/%m/%Y" }}</small>
      </div>

    </div>
  {% endfor %}
</div>
