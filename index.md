---
layout: page
title: "Daily videos about upcoming videogames"
---

<style>
  .post-card { 
    display: flex; 
    gap: 20px; 
    margin-bottom: 30px; 
    align-items: flex-start; 
  }
  
  .post-thumb { 
    width: 220px; 
    flex-shrink: 0; 
  }
  
  .post-thumb img { 
    width: 100%; 
    border-radius: 8px; 
  }

  /* ESTA ES LA LÍNEA QUE ARREGLA EL TEXTO A LA IZQUIERDA */
  .post-excerpt-container { 
    flex: 1; 
  }

  .post-excerpt-container h3 a { 
    color: #FF0B55 !important; 
    text-decoration: none; 
  }
</style>

<div class="posts-list">
  {% for post in site.posts %}
    <div class="post-card">
      
      {% if post.thumbnail and post.thumbnail != "" %}
      <div class="post-thumb">
        <a href="{{ post.url }}">
          <img src="{{ post.thumbnail }}" alt="{{ post.title }}">
        </a>
      </div>
      {% endif %}

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
