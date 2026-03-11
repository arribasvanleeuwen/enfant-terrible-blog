---
layout: page
title: "Daily videos about upcoming videogames"
---

<style>
  /* 1. Quitamos cualquier línea que Jekyll Minima ponga automáticamente bajo el título de la página */
  .page-header { border-bottom: none !important; margin-bottom: 0 !important; }
  
  .search-wrapper {
    margin: 15px auto 45px auto; /* Espacio generoso abajo para alejarlo de la línea del primer post */
    position: relative;
    width: 100%;
    max-width: 800px;
  }

  #search-input {
    width: 100%;
    padding: 12px 15px;
    background: #2b2b2b;
    color: #fff;
    border: 2px solid #444;
    border-radius: 8px;
    outline: none;
    transition: all 0.3s ease;
    box-sizing: border-box;
    font-size: 16px;
  }

  #search-input:focus {
    border-color: #FF0B55;
    background-color: #333;
    box-shadow: 0 0 12px rgba(255, 11, 85, 0.2);
  }

  /* El desplegable flota sobre las líneas de los posts sin cortarlas */
  #results-container {
    list-style: none;
    margin: 5px 0 0 0;
    padding: 0;
    position: absolute;
    width: 100%;
    background: #1d1d1d;
    z-index: 1000;
    border: 1px solid #444;
    border-radius: 8px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.8);
    overflow: hidden;
  }

  #results-container li a {
    display: block;
    padding: 12px 20px;
    color: #eee;
    text-decoration: none;
    border-bottom: 1px solid #333;
  }

  #results-container li a:hover {
    background-color: #FF0B55;
    color: #fff;
  }

  /* 2. Aseguramos que los posts mantengan sus líneas de separación originales */
  .post-card {
    border-top: 1px solid #333; /* Línea de separación superior para cada post */
    padding-top: 30px;
    margin-bottom: 40px;
  }

  /* Si quieres que el primer post no tenga línea superior para que no choque con el buscador, usa esto: */
  /* .post-card:first-of-type { border-top: none; } */

  @media (max-width: 600px) {
    .search-wrapper {
      padding: 0 10px;
      margin-bottom: 30px;
    }
  }
</style>

<div class="search-wrapper">
  <input type="text" id="search-input" placeholder="Search videos...">
  <ul id="results-container"></ul>
</div>

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
        <h3 style="margin-top: 0;">
          <a href="{{ post.url }}" style="color: #fff; text-decoration: none;">{{ post.title }}</a>
        </h3>
        
        <div class="excerpt-text" style="color: #ccc;">
          {{ post.excerpt }}
        </div>

        <small class="post-date" style="color: #FF0B55;">{{ post.date | date: "%d/%m/%Y" }}</small>
      </div>

    </div>
  {% endfor %}
</div>

<script src="https://unpkg.com/simple-jekyll-search@latest/dest/simple-jekyll-search.min.js"></script>
<script>
  SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('results-container'),
    json: '{{ "/search.json" | relative_url }}',
    searchResultTemplate: '<li><a href="{url}">{title}</a></li>',
    noResultsText: '<li style="padding:15px; color:#888;">No results found</li>',
    limit: 10
  })
</script>
