---
layout: page
title: "Daily videos about upcoming videogames"
---

<style>
  .search-wrapper {
    /* Ajustamos el aire arriba y abajo para que quede visualmente centrado entre las líneas */
    margin: 40px auto 40px auto; 
    position: relative;
    width: 100%;
    max-width: 800px;
    display: block;
  }

  #search-input {
    width: 100%;
    padding: 12px 15px;
    background: #2b2b2b;
    color: #fff;
    border: 2px solid #444;
    border-radius: 8px;
    outline: none;
    transition: border-color 0.3s;
    box-sizing: border-box; /* Mantiene el buscador centrado en móvil */
    font-size: 16px; /* Evita el zoom en móviles */
    display: block;
  }

  #search-input:focus {
    border-color: #FF0B55;
  }

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
    box-shadow: 0 10px 25px rgba(0,0,0,0.5);
    overflow: hidden;
  }

  #results-container li a {
    display: block;
    padding: 12px 15px;
    color: #eee;
    text-decoration: none;
  }

  #results-container li a:hover {
    background-color: #FF0B55;
    color: #fff;
  }

  /* Aseguramos que el contenido de los posts no empuje el buscador hacia arriba */
  .posts-list {
    margin-top: 0;
    padding-top: 0;
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
    noResultsText: '<li style="padding:10px; color:#888;">No results found</li>',
    limit: 10
  })
</script>
