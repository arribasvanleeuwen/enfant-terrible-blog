---
layout: page
title: "Daily videos about upcoming videogames"
---

<div class="posts-list">
  {% for post in site.posts %}
    <div style="display: flex; gap: 20px; margin-bottom: 30px; align-items: flex-start; border-bottom: 1px solid #eee; padding-bottom: 20px;">
      
      <div style="flex-shrink: 0; width: 180px;">
        <a href="{{ post.url }}">
          <img src="{{ post.thumbnail }}" style="width: 100%; border-radius: 8px; box-shadow: 0 4px 10px rgba(0,0,0,0.1);">
        </a>
      </div>

      <div style="flex-grow: 1;">
        <h3 style="margin-top: 0; margin-bottom: 10px;">
          <a href="{{ post.url }}" style="text-decoration: none; color: #333;">{{ post.title }}</a>
        </h3>
        
        <div style="font-size: 0.95em; color: #666; line-height: 1.5; margin-bottom: 10px;">
          {{ post.content | strip_html | truncatewords: 25 }}
        </div>

        <small style="color: #999;">{{ post.date | date: "%d/%m/%Y" }}</small>
      </div>

    </div>
  {% endfor %}
</div>
