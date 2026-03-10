---
layout: page
title: "Daily videos about upcoming videogames"
---

<style>
  /* 1. MANTENEMOS TU ESTRUCTURA PERO CON TUS COLORES */
  .post-card { 
    display: flex !important; 
    gap: 25px !important; 
    margin-bottom: 40px !important; 
    align-items: flex-start !important; 
    border-bottom: 1px solid rgba(255,255,255,0.1) !important; 
    padding-bottom: 20px !important; 
  }
  .post-thumb { width: 220px !important; flex-shrink: 0 !important; }
  .post-thumb img { width: 100% !important; border-radius: 8px !important; }
  
  .post-excerpt-container h3 a { 
    color: #FF0B55 !important; 
    text-decoration: none !important; 
    font-size: 22px !important; 
    font-weight: bold !important; 
  }
  .excerpt-text { color: #bbbbbb !important; }
  .post-date { color: #888 !important; }

  /* 2. ARREGLAMOS EL FOOTER DE MINIMA SIN ROMPERLO */
  /* Izquierda: Copyright */
  .footer-col-1 .footer-heading { display: none !important; }
  .footer-col-1::before { content: "© 2026 ENFANT TERRIBLE"; color: #ffffff; font-weight: bold; }

  /* Centro: Email Rosa */
  .footer-col-2 .footer-heading, .footer-col-2 .contact-list { display: none !important; }
  .footer-col-2::before { 
    content: "contact" "\0040" "enfant-terrible.media"; 
    color: #FF0B55; 
    font-weight: bold; 
  }

  /* Derecha: Iconos Sociales en Rosa */
  .social-media-list li a, .social-media-list li a .svg-icon { 
    fill: #FF0B55 !important; 
    color: #FF0B55 !important; 
  }

  @media (max-width: 600px) {
    .post-card { flex-direction: column !important; text-align: center !important; }
    .post-thumb { width: 100% !important; max-width: 320px !important; margin: 0 auto !important; }
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
