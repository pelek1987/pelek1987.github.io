# Mój Blog Jekyll

Blog oparty na Jekyll i hostowany na GitHub Pages.

## Struktura projektu

```
.
├── _config.yml          # Konfiguracja Jekyll
├── _posts/              # Posty blogowe
├── _layouts/            # Szablony HTML
├── docs/                # Dokumentacja
├── images/              # Obrazki
├── index.md             # Strona główna
├── about.md             # O mnie
├── search.md            # Wyszukiwarka
├── archive.md           # Archiwum postów
└── search.json          # Dane dla wyszukiwarki
```

## Jak dodać nowy post?

1. Utwórz nowy plik w katalogu `_posts/` z nazwą: `YYYY-MM-DD-tytuł-posta.md`
2. Dodaj front matter na początku pliku:
   ```yaml
   ---
   layout: post
   title: "Tytuł posta"
   published: true
   categories:
     - Kategoria
   tags:
     - tag1
     - tag2
   ---
   ```
3. Napisz treść w Markdown
4. Commit i push do repozytorium

## Uruchomienie lokalnie

```bash
# Instalacja Jekyll (jeśli nie masz)
gem install bundler jekyll

# Uruchomienie serwera lokalnego
bundle exec jekyll serve

# Blog będzie dostępny pod: http://localhost:4000
```

## Tutorial

Pełny tutorial znajduje się w pliku [docs/JEKYLL-TUTORIAL.md](docs/JEKYLL-TUTORIAL.md)

## Licencja

Treść bloga - Paweł Sioda
Motyw - [no-style-please](https://github.com/riggraz/no-style-please)
