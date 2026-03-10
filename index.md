---
layout: page
---

<style>
  /* 1. CONTENEDOR PRINCIPAL DE POSTS */
  .post-card {
    display: flex !important;
    gap: 25px !important;
    margin-bottom: 40px !important;
    padding-bottom: 30px !important;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1) !important;
    align-items: flex-start !important;
  }

  /* 2. MINIATURA (Solo si existe) */
  .post-thumb {
    flex-shrink: 0 !important;
    width: 220px !important;
  }

  .post-thumb img {
    width: 100% !important;
    border-radius: 8px !important;
    display: block !important;
  }

  /* 3. TEXTO Y TÍTULOS */
  .post-content {
    flex-grow: 1 !important;
  }

  .post-card h3 {
    margin: 0 0 10px 0 !important;
  }

  .post-card h3 a {
    color: #FF0B55 !important;
    text-decoration: none !important;
    font-size: 22px !important;
    font-weight: 700 !important;
  }

  .post-card h3 a:hover {
    color: #ffffff !important;
  }

  .excerpt-text {
    color: #bbbbbb !important;
    font-size: 15px !important;
    line-height: 1.5 !important;
  }

  /* 4. FOOTER FORZADO (Blanco y Rosa) */
  .custom-footer {
    margin-top: 60px !important;
    padding: 40px 0 !important;
    border-top: 1px solid rgba(255, 255, 255, 0.15) !important;
    display: flex !important;
    justify-content: space-between !important;
    align-items: center !important;
  }

  .foot-copy {
    color: #ffffff !important;
    font-weight: bold !important;
    font-size: 14px !important;
  }

  /* Email Invisible para Scrapers */
  .foot-email::before {
    content: "enfante.terrible777" "\0040" "gmail.com" !important;
    color: #FF0B55 !important;
    font-weight: bold !important;
    font-size: 14px !important;
  }

  .foot-social a {
    color: #FF0B55 !important;
    text-decoration: none !important;
    font-weight: bold !important;
    font-size: 14px !important;
    text-transform: uppercase !important;
  }

  .foot-social a:hover {
    color: #ffffff !important;
  }

  /* 5. RESPONSIVE MÓVIL */
  @media screen and (max-width: 600px) {
    .post-card {
      flex-direction: column !important;
      align-items: center !important;
      text-align: center !important;
    }
    .post-thumb { width: 100% !important; max-width: 320px !important; }
    .custom-footer {
      flex-direction: column !important;
      gap: 20px !important;
      text-align: center !important;
    }
  }
</style>

{% for post in site.posts %}
  <div class="post-card">
    {% if post.image %}
    <div class="post-thumb">
      <a href="{{ post.url | relative_url }}">
        <img src="{{ post.image }}" alt="{{ post.title }}">
      </a>
    </div>
    {% endif %}
    
    <div class="post-content">
      <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
      <div class="excerpt-text">
        {{ post.excerpt | strip_html | truncate: 160 }}
      </div>
    </div>
  </div>
{% endfor %}

<footer class="custom-footer">
  <div class="foot-copy">© {{ 'now' | date: "%Y" }} ENFANT TERRIBLE</div>
  <div class="foot-email"></div>
  <div class="foot-social">
    <a href="https://x.com/EnfantTerrible7" target="_blank">X (Twitter)</a>
  </div>
</footer>
