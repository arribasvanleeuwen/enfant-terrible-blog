---
layout: page
title: "Daily videos about upcoming videogames"
---

<style>
  /* Alineación de los posts */
  .post-card { 
    display: flex; 
    gap: 25px; 
    margin-bottom: 40px; 
    padding-bottom: 20px; 
    border-bottom: 1px solid rgba(255,255,255,0.1); 
    align-items: flex-start; 
  }

  .post-thumb { width: 220px; flex-shrink: 0; }
  .post-thumb img { width: 100%; border-radius: 8px; display: block; }

  /* Esto asegura que el texto ocupe el espacio sobrante si no hay imagen */
  .post-excerpt-container { flex: 1; }

  .post-excerpt-container h3 a { 
    color: #FF0B55 !important; 
    text-decoration: none; 
    font-size: 22px; 
    font-weight: bold; 
  }
  
  .excerpt-text { color: #bbbbbb; font-size: 15px; }
  .post-date { color: #888; }

  @media (max-width: 600px) {
    .post-card { flex-direction: column; text-align: center; }
    .post-thumb { width: 100%; max-width: 320px; margin: 0 auto; }
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
