---
layout: page
---

<style>
  /* VOLVEMOS AL DISEÑO QUE FUNCIONABA */
  .post-card { display: flex; gap: 25px; margin-bottom: 40px; padding-bottom: 20px; border-bottom: 1px solid rgba(255,255,255,0.1); align-items: flex-start; }
  .post-thumb { width: 220px; flex-shrink: 0; }
  .post-thumb img { width: 100%; border-radius: 8px; display: block; }
  .post-card h3 a { color: #FF0B55 !important; text-decoration: none; font-size: 22px; font-weight: bold; }
  .excerpt-text { color: #bbbbbb; font-size: 15px; }

  /* AJUSTE PARA EL FOOTER DE MINIMA (SIN CARGARSE EL ORIGINAL) */
  .footer-col-1 .footer-heading { display: none !important; }
  .footer-col-1::before { content: "© 2026 ENFANT TERRIBLE"; color: #ffffff; font-weight: bold; }
  .footer-col-2 .footer-heading, .footer-col-2 .contact-list { display: none !important; }
  .footer-col-2::before { content: "contact" "\0040" "enfant-terrible.media"; color: #FF0B55; font-weight: bold; }
  .social-media-list li a, .social-media-list li a .svg-icon { fill: #FF0B55 !important; color: #FF0B55 !important; }

  @media (max-width: 600px) {
    .post-card { flex-direction: column; text-align: center; }
    .post-thumb { width: 100%; max-width: 320px; margin: 0 auto; }
  }
</style>

{% for post in site.posts %}
  <div class="post-card">
    {% if post.image %}
    <div class="post-thumb">
      <a href="{{ post.url }}">
        <img src="{{ post.image }}">
      </a>
    </div>
    {% endif %}
    <div class="post-content">
      <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
      <div class="excerpt-text">{{ post.excerpt | strip_html | truncate: 160 }}</div>
    </div>
  </div>
{% endfor %}
