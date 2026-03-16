---
layout: page
title: "Daily videos about upcoming videogames"
---

<style>
  /* TUS AJUSTES DE BUSCADOR EXISTENTES */
  .search-wrapper-box {
    margin-top: -25px !important; 
    padding-bottom: 30px !important;
    position: relative;
    width: 100%;
    display: block;
    z-index: 10;
  }

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
    margin: 0 !important;
    display: block;
  }

  #search-input:focus { border-color: #FF0B55; }

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
    box-shadow: 0 5px 15px rgba(0,0,0,0.5);
  }

  #results-container li a { display: block; padding: 12px; color: #eee; text-decoration: none; }
  #results-container li a:hover { background: #FF0B55; color: #fff; }

  /* ESTILOS PARA EL CARGANDO (INFINITE SCROLL) */
  .load-status {
    text-align: center;
    padding: 40px 0;
    color: #888;
    font-size: 14px;
    font-style: italic;
  }

  /* Animación suave para los nuevos posts que aparezcan */
  .post-card {
    animation: fadeIn 0.5s ease both;
  }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }
</style>

<div class="search-wrapper-box">
  <input type="text" id="search-input" placeholder="Search videos...">
  <ul id="results-container"></ul>
</div>

<div id="posts-container" class="posts-list">
  {% for post in paginator.posts %}
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

{% if paginator.next_page %}
  <div id="infinite-scroll-trigger" class="load-status" data-next-url="{{ paginator.next_page_path | relative_url }}">
    <p>Loading more videos...</p>
  </div>
{% else %}
  <div class="load-status">
    <p>You've reached the end of the world.</p>
  </div>
{% endif %}

<script src="https://unpkg.com/simple-jekyll-search@latest/dest/simple-jekyll-search.min.js"></script>

<script>
  // 1. LÓGICA DEL BUSCADOR (TUYA ORIGINAL)
  SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('results-container'),
    json: '{{ "/search.json" | relative_url }}',
    searchResultTemplate: '<li><a href="{url}">{title}</a></li>',
    noResultsText: '<li style="padding:10px; color:#888;">No results found</li>'
  });

  // 2. LÓGICA DE INFINITE SCROLL AUTODETECTABLE
  (function() {
    const trigger = document.getElementById('infinite-scroll-trigger');
    const container = document.getElementById('posts-container');
    if (!trigger) return;

    let isLoading = false;

    // El "ojo" que detecta cuando el usuario llega al final según su dispositivo
    const observer = new IntersectionObserver((entries) => {
      if (entries[0].isIntersecting && !isLoading) {
        loadMorePosts();
      }
    }, {
      rootMargin: '300px' // Carga 300px antes de que el usuario llegue al final (mejor UX en móvil)
    });

    observer.observe(trigger);

    async function loadMorePosts() {
      const nextUrl = trigger.getAttribute('data-next-url');
      if (!nextUrl) return;

      isLoading = true;

      try {
        const response = await fetch(nextUrl);
        const text = await response.text();
        const parser = new DOMParser();
        const doc = parser.parseFromString(text, 'text/html');

        // Seleccionamos los nuevos posts del HTML descargado
        const newPosts = doc.querySelectorAll('#posts-container .post-card');
        
        newPosts.forEach(post => {
          container.appendChild(post);
        });

        // Buscamos si hay una siguiente página en el nuevo HTML
        const nextTrigger = doc.getElementById('infinite-scroll-trigger');
        const nextNextUrl = nextTrigger ? nextTrigger.getAttribute('data-next-url') : null;

        if (nextNextUrl) {
          trigger.setAttribute('data-next-url', nextNextUrl);
          isLoading = false;
        } else {
          // Si no hay más páginas, detenemos el observador
          trigger.innerHTML = "<p>All videos loaded.</p>";
          observer.unobserve(trigger);
        }
      } catch (error) {
        console.error("Error loading posts:", error);
        isLoading = false;
      }
    }
  })();
</script>
