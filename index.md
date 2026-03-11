---
layout: page
title: "Daily videos about upcoming videogames"
---

<style>
  /* 1. ESPACIO EXCLUSIVO DEL BUSCADOR */
  .search-wrapper-container {
    /* Padding igual arriba y abajo crea la simetría visual */
    padding: 30px 0 !important; 
    /* Eliminamos márgenes externos para no empujar el título ni los posts */
    margin: 0 !important;
    position: relative;
    width: 100%;
    display: block;
  }

  /* 2. EL INPUT (Sin márgenes que lo desvíen) */
  #search-input {
    width: 100%;
    padding: 12px 15px;
    background: #2b2b2b;
    color: #fff;
    border: 2px solid #444;
    border-radius: 8px;
    font-size: 16px; 
    box-sizing: border-box;
    outline: none;
    margin: 0 !important; /* Evita que el navegador le añada espacio extra */
    display: block;
  }

  #search-input:focus { border-color: #FF0B55; }

  /* 3. RESULTADOS (Capa superior) */
  #results-container {
    list-style: none;
    margin: 5px 0 0 0;
    padding: 0;
    position: absolute;
    width: 100%;
    background: #1d1d1d;
    z-index: 100;
    border: 1px solid #444;
    border-radius: 8px;
    box-shadow: 0 5px 15px rgba(0,0,0,0.5);
  }

  #results-container li a { display: block; padding: 10px; color: #eee; text-decoration: none; }
  #results-container li a:hover { background: #FF0B55; color: #fff; }
</style>

<div class="search-wrapper-container">
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

<script src="https://unpkg.com/simple-jekyll-search@latest/dest/simple-jekyll-search.min.js"></script>
<script>
  SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('results-container'),
    json: '{{ "/search.json" | relative_url }}',
    searchResultTemplate: '<li><a href="{url}">{title}</a></li>',
    noResultsText: '<li style="padding:10px; color:#888;">No results found</li>'
  })
</script>
