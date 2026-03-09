---
layout: default
---

<style>
  /* Aquí está todo el trabajo de diseño que hemos hecho */
  body { background-color: #0f0f0f !important; color: #f1f1f1 !important; font-family: sans-serif; margin: 0; }
  .wrapper { max-width: 800px; margin: 0 auto; padding: 0 20px; }
  
  /* Cabecera con Logo y Botón */
  .custom-header { display: flex; justify-content: space-between; align-items: center; padding: 15px 0; border-bottom: 1px solid #2f2f2f; }
  .btn-subscribe { background-color: #FF0B55; color: white !important; padding: 10px 20px; border-radius: 8px; font-weight: bold; text-decoration: none; text-transform: uppercase; font-size: 12px; }

  /* Enlaces Rosas */
  a { color: #FF0B55 !important; text-decoration: none; }
  
  /* Tarjetas de Posts */
  .post-list { list-style: none; padding: 0; margin-top: 30px; }
  .post-card { background: #1e1e1e; border: 1px solid #2f2f2f; border-radius: 12px; padding: 25px; margin-bottom: 20px; transition: 0.3s; }
  .post-card:hover { border-color: #FF0B55; transform: translateY(-3px); }
  .post-title { font-size: 1.5rem; font-weight: bold; display: block; }
</style>

<div class="custom-header">
  <a href="/"><img src="/assets/images/logo.png" style="max-height: 45px;" alt="Logo"></a>
  <a href="https://youtube.com/@tu_canal?sub_confirmation=1" class="btn-subscribe" target="_blank">Subscribe</a>
</div>

<div style="margin-top: 40px;">
  <h1>📺 Channel Updates & Resources</h1>
  <p>Welcome to the official archive. Here you will find all the code and links from my videos.</p>
</div>

<ul class="post-list">
  {% for post in site.posts %}
    <li class="post-card">
      <span style="color: #888; font-size: 0.8rem;">{{ post.date | date: "%b %-d, %Y" }}</span>
      <a class="post-title" href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
    </li>
  {% endfor %}
</ul>
