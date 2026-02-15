---
layout: default
title: Strona główna
---

# Witaj na moim blogu!

Tutaj dzielę się swoimi przemyśleniami o programowaniu, technologii i nie tylko.

## Najnowsze posty

<ul>
  {% for post in site.posts limit:5 %}
    <li>
      <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

[Zobacz wszystkie posty →](/archive/)
