---
layout: page
---

<style>
  /* 1. ELIMINAR EL FOOTER DOBLE Y ELEMENTOS EXTRA */
  .site-footer { display: none !important; } /* Matamos el footer oficial de Minima */
  .page-heading { display: none !important; } /* Evitamos que el título se duplique */

  /* 2. DISEÑO DE POSTS (LO QUE TE GUSTABA) */
  .post-card { display: flex !important; gap: 25px !important; margin-bottom: 40px !important; align-items: flex-start !important; border-bottom: 1px solid rgba(255,255,255,0.1); padding-bottom: 20px; }
  .post-thumb { width: 220px !important; flex-shrink: 0 !important; }
  .post-thumb img { width: 100% !important; border-radius: 8px !important; display: block !important; }
  .post-content { flex-grow: 1 !important; }
  .post-card h3 a { color: #FF0B55 !important; text-decoration: none !important; font-size: 22px !important; font-weight: bold !important; }
  .excerpt-text { color: #bbbbbb !important; font-size: 15px !important; }

  /* 3. TU NUEVO FOOTER (ÚNICO) */
  .custom-footer { margin-top: 50px; padding: 40px 0; border-top: 1px solid rgba(255,255,255,0.15); display: flex; justify-content: space-between; align-items: center; }
  .foot-copy { color: #ffffff; font-weight: bold; }
  .foot-email::before { content: "enfante.terrible777" "\0040" "gmail.com"; color: #FF0B55; font-weight: bold; }
  .foot-social a { color: #FF0B55; text-decoration: none; font-weight: bold; text-transform: uppercase; }

  @media (max-width: 600px) {
    .post-card, .custom-footer { flex-direction: column !important; text-align: center !important; }
    .post-thumb { width: 100% !important; max-width: 320px !important; margin: 0 auto !important; }
  }
</style>

<h1 style="color: #ffffff; margin-bottom: 30px;">Latest Insights</h1>

{% for post in site.posts %}
  <div class="post-card">
    {% if post.image %}
    <div class="post-thumb">
      <a href="{{ post.url | relative_url }}">
        <img src="{{ post.image | relative_url }}">
      </a>
    </div>
    {% endif %}
    <div class="post-content">
      <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
      <div class="excerpt-text">{{ post.excerpt | strip_html | truncate: 160 }}</div>
    </div>
  </div>
{% endfor %}

<footer class="custom-footer">
  <div class="foot-copy">© 2026 ENFANT TERRIBLE</div>
  <div class="foot-email"></div>
  <div class="foot-social">
    <a href="https://x.com/EnfantTerrible7" target="_blank">X (Twitter)</a>
  </div>
</footer>
