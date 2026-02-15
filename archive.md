---
layout: default
title: Archiwum
permalink: /archive/
---

# Archiwum postów

<ul>
  {% for post in site.posts %}
    <li>
      <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {% if post.categories %}
        <span style="color: #666;">
          [{{ post.categories | join: ', ' }}]
        </span>
      {% endif %}
    </li>
  {% endfor %}
</ul>
