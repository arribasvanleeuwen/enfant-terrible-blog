---
layout: default
---

<style>
  /* 1. ARREGLO DE TÍTULO Y COLORES */
  .site-title { color: #ffffff !important; }
  .post-list-heading { color: #ffffff !important; font-size: 28px; margin-bottom: 30px; }

  /* 2. ESTRUCTURA DE POSTS (CON IMAGEN IZQUIERDA) */
  .post-card { display: flex; gap: 25px; margin-bottom: 40px; padding-bottom: 20px; border-bottom: 1px solid rgba(255,255,255,0.1); align-items: flex-start; }
  .post-thumb { width: 220px; flex-shrink: 0; }
  .post-thumb img { width: 100%; border-radius: 8px; display: block; }
  .post-content { flex-grow: 1; }
  .post-card h3 a { color: #FF0B55 !important; text-decoration: none; font-size: 22px; font-weight: bold; }
  .excerpt-text { color: #bbbbbb; font-size: 15px; }

  /* 3. FOOTER PERSONALIZADO (SOBREESCRIBE AL DE MINIMA) */
  .site-footer { border-top: 1px solid rgba(255,255,255,0.1) !important; padding: 40px 0 !important; }
  .footer-col-wrapper { display: flex; justify-content: space-between; align-items: center; }
  .footer-col-1::before { content: "© {{ 'now' | date: '%Y' }} ENFANT TERRIBLE"; color: #ffffff; font-weight: bold; }
  .footer-col-2::before { content: "enfante.terrible777" "\0040" "gmail.com"; color: #FF0B55; font-weight: bold; }
  .footer-col-1 .footer-heading, .footer-col-2 .contact-list, .footer-col-3 .footer-heading { display: none !important; }
  .social-media-list li a { color: #FF0B55 !important; font-weight: bold; }

  @media (max-width: 600px) {
    .post-card, .footer-col-wrapper { flex-direction: column; text-align: center; }
    .post-thumb { width: 100%; max-width: 320px; margin: 0 auto; }
  }
</style>

<h1 class="post-list-heading">Latest Insights</h1>

{% for post in site.posts %}
  <div class="post-card">
    {% if post.image %}
    <div class="post-thumb">
      <a href="{{ post.url | relative_url }}">
        <img src="{{ post.image | relative_url }}" alt="{{ post.title }}">
      </a>
    </div>
    {% endif %}
    <div class="post-content">
      <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
      <div class="excerpt-text">{{ post.excerpt | strip_html | truncate: 160 }}</div>
    </div>
  </div>
{% endfor %}
