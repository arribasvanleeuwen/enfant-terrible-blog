---
layout: page
title: "Daily videos about upcoming videogames"
---

<style>
  .search-wrapper {
    margin-bottom: 40px;
    position: relative;
  }
  #search-input {
    width: 100%;
    padding: 12px 15px;
    background: #2b2b2b;
    color: #fff;
    border: 2px solid #444;
    border-radius: 4px;
    outline: none;
    transition: border-color 0.3s;
  }
  #search-input:focus {
    border-color: #FF0B55;
  }
  #results-container {
    list-style: none;
    margin: 0;
    padding: 0;
    position: absolute;
    width: 100%;
    background: #1d1d1d;
    z-index: 999;
    border: 1px solid #444;
    border-top: none;
  }
  #results-container li a {
    display: block;
    padding: 10px 15px;
    color: #eee;
    text-decoration: none;
  }
  #results-container li a:hover {
    background: #FF0B55;
    color: #fff;
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
    json: '/search.json',
    searchResultTemplate: '<li><a href="{url}">{title}</a></li>',
    noResultsText: '<li style="padding:10px;">No results found</li>'
  })
</script>
