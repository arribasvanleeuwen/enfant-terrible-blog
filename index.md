---
layout: page
title: "Daily videos about upcoming videogames"
---

<style>
  /* 1. ARREGLO DE ALINEACIÓN (Post con y sin imagen) */
  .post-card { 
    display: flex !important; 
    gap: 25px !important; 
    margin-bottom: 40px !important; 
    align-items: flex-start !important; 
    border-bottom: 1px solid rgba(255,255,255,0.1) !important; 
    padding-bottom: 20px !important;
    width: 100%;
  }

  .post-thumb { 
    width: 220px !important; 
    flex-shrink: 0 !important; 
  }
  
  .post-thumb img { 
    width: 100% !important; 
    border-radius: 8px !important; 
    display: block !important; 
  }

  .post-excerpt-container { 
    flex: 1 !important;
    display: flex !important;
    flex-direction: column !important;
    justify-content: center !important;
  }
  
  .post-excerpt-container h3 a { 
    color: #FF0B55 !important; 
    text-decoration: none !important; 
    font-size: 22px !important; 
    font-weight: bold !important; 
    display: block !important;
    margin-bottom: 8px !important;
  }

  .excerpt-text { color: #bbbbbb !important; font-size: 15px !important; line-height: 1.4 !important; }
  .post-date { color: #888 !important; margin-top: 10px !important; display: block !important; }

  /* 2. FOOTER PROTEGIDO Y ROSA */
  /* Forzamos que la columna del email (col-2) muestre tu correo vía CSS */
  .footer-col-2 .contact-list::before {
    content: "contact" "\0040" "enfant-terrible.media";
    color: #FF0B55;
    font-weight: bold;
    font-size: 14px;
    display: block;
    padding-top: 10px;
  }

  /* Limpiamos textos por defecto de Minima */
  .footer-col-1 .footer-heading, .footer-col-2 .footer-heading { display: none !important; }
  .footer-col-1::before { content: "© 2026 ENFANT TERRIBLE"; color: #ffffff; font-weight: bold; font-size: 14px; }

  /* Iconos en rosa */
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
          {{ post.excerpt | strip_html | truncate: 160 }}
        </div>

        <small class="post-date">{{ post.date | date: "%d/%m/%Y" }}</small>
      </div>

    </div>
  {% endfor %}
</div>
