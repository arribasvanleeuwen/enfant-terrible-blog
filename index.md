---
layout: page
title: "Daily videos about upcoming videogames"
---

<div class="posts-list">
  {% for post in site.posts %}
    <div style="display: flex; gap: 20px; margin-bottom: 30px; align-items: flex-start; border-bottom: 1px solid #f0f0f0; padding-bottom: 25px;">
      
      <div style="flex-shrink: 0; width: 180px;">
        <a href="{{ post.url }}">
          <img src="{{ post.thumbnail }}" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.12); display: block;">
        </a>
      </div>

      <div style="flex-grow: 1;">
        <h3 style="margin-top: 0; margin-bottom: 8px; font-size: 1.25em;">
          <a href="{{ post.url }}" style="text-decoration: none; color: #222; font-weight: 700;">{{ post.title }}</a>
        </h3>
        
        <div style="font-size: 0.95em; color: #555; line-height: 1.5; margin-bottom: 12px; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden;">
          {{ post.excerpt | default: (post.content | strip_html | truncatewords: 25) }}
        </div>

        <div style="display: flex; align-items: center; gap: 10px;">
           <small style="color: #bbb; font-weight: 500;">{{ post.date | date: "%d/%m/%Y" }}</small>
        </div>
      </div>

    </div>
  {% endfor %}
</div>
