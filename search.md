---
layout: default
title: Wyszukiwarka
permalink: /search/
---

# Wyszukiwarka

<div id="search-container">
  <input type="text" id="search-input" placeholder="Szukaj postów..." style="width: 100%; padding: 10px; font-size: 16px;">
  <ul id="results-container" style="list-style: none; padding: 0; margin-top: 20px;"></ul>
</div>

<script src="https://unpkg.com/simple-jekyll-search@latest/dest/simple-jekyll-search.min.js"></script>
<script>
  SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('results-container'),
    json: '/search.json',
    searchResultTemplate: '<li><a href="{url}">{title}</a> <span style="color: #666;">({date})</span></li>',
    noResultsText: 'Nie znaleziono wyników',
    limit: 10,
    fuzzy: false
  })
</script>
