---
layout: page
title: "Daily videos about upcoming videogames"
---

<style>
  /* Mantenemos tus estilos del buscador y post-cards */
  .search-wrapper-box { margin-top: -25px !important; padding-bottom: 30px !important; position: relative; width: 100%; display: block; z-index: 10; }
  #search-input { width: 100%; padding: 12px 15px; background: #2b2b2b; color: #fff; border: 2px solid #444; border-radius: 8px; font-size: 16px; box-sizing: border-box; outline: none; display: block; }
  #results-container { list-style: none; margin: 5px 0 0 0; padding: 0; position: absolute; width: 100%; background: #1d1d1d; z-index: 1000; border: 1px solid #444; border-radius: 8px; }
  
  .load-status { text-align: center; padding: 40px 0; color: #888; font-size: 14px; }
  .post-card { animation: fadeIn 0.5s ease both; margin-bottom: 30px; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
</style>

<div class="search-wrapper-box">
  <input type="text" id="search-input" placeholder="Search videos...">
  <ul id="results-container"></ul>
</div>

<div id="posts-container" class="posts-list">
  {% comment %} Cargamos los primeros 10 posts de forma estática para el SEO {% endcomment %}
  {% for post in site.posts limit: 10 %}
    <div class="post-card">
      {% if post.thumbnail and post.thumbnail != "" %}
      <div class="post-thumb">
        <a href="{{ post.url | relative_url }}">
          <img src="{{ post.thumbnail }}" alt="{{ post.title }}">
        </a>
      </div>
      {% endif %}
      <div class="post-excerpt-container">
        <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
        <div class="excerpt-text">{{ post.excerpt }}</div>
        <small class="post-date">{{ post.date | date: "%d/%m/%Y" }}</small>
      </div>
    </div>
  {% endfor %}
</div>

<div id="infinite-scroll-trigger" class="load-status">
  <p>Loading more videos...</p>
</div>

<script src="https://unpkg.com/simple-jekyll-search@latest/dest/simple-jekyll-search.min.js"></script>

<script>
  // 1. TU BUSCADOR (Se mantiene igual)
  SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('results-container'),
    json: '{{ "/search.json" | relative_url }}',
    searchResultTemplate: '<li><a href="{url}">{title}</a></li>',
    noResultsText: '<li style="padding:10px; color:#888;">No results found</li>'
  });

  // 2. INFINITE SCROLL POR JSON
  (function() {
    let allPosts = [];
    let currentIndex = 10; // Empezamos en el 10 porque los primeros 10 ya están en el HTML
    const postsPerLoad = 10;
    const container = document.getElementById('posts-container');
    const trigger = document.getElementById('infinite-scroll-trigger');

    // Cargamos la base de datos del search.json
    fetch('{{ "/search.json" | relative_url }}')
      .then(response => response.json())
      .then(data => {
        allPosts = data;
        // Si hay menos de 10 posts en total, quitamos el mensaje de carga
        if (allPosts.length <= currentIndex) {
          trigger.innerHTML = "<p>End of feed.</p>";
        } else {
          startObserver();
        }
      });

    function startObserver() {
      const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
          loadMore();
        }
      }, { rootMargin: '400px' });
      observer.observe(trigger);
    }

    function loadMore() {
      const nextPosts = allPosts.slice(currentIndex, currentIndex + postsPerLoad);
      
      nextPosts.forEach(post => {
        // Creamos el HTML dinámicamente. 
        // IMPORTANTE: Asegúrate de que los nombres de los campos coincidan con tu search.json
        const postHTML = `
          <div class="post-card">
            ${post.thumbnail ? `
              <div class="post-thumb">
                <a href="${post.url}">
                  <img src="${post.thumbnail}" alt="${post.title}">
                </a>
              </div>` : ''}
            <div class="post-excerpt-container">
              <h3><a href="${post.url}">${post.title}</a></h3>
              <div class="excerpt-text">${post.excerpt || ''}</div>
              <small class="post-date">${post.date || ''}</small>
            </div>
          </div>`;
        container.insertAdjacentHTML('beforeend', postHTML);
      });

      currentIndex += postsPerLoad;

      if (currentIndex >= allPosts.length) {
        trigger.innerHTML = "<p>All videos loaded.</p>";
      }
    }
  })();
</script>
