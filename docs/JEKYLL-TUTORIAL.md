# Tutorial: Tworzenie bloga z Jekyll i GitHub Pages

*Na podstawie artykułu Tomasza Dunii z [blog.tomaszdunia.pl](https://blog.tomaszdunia.pl/blog-jekyll-github/)*

## Spis treści

1. [Wprowadzenie](#wprowadzenie)
2. [Tworzenie repozytorium GitHub](#tworzenie-repozytorium-github)
3. [Struktura projektu](#struktura-projektu)
4. [Konfiguracja _config.yml](#konfiguracja-_configyml)
5. [Tworzenie postów](#tworzenie-postów)
6. [Tworzenie layoutu](#tworzenie-layoutu)
7. [Implementacja wyszukiwarki](#implementacja-wyszukiwarki)
8. [Konfiguracja domeny](#konfiguracja-domeny)
9. [Ustawienia GitHub Pages](#ustawienia-github-pages)

---

## Wprowadzenie

Jekyll to generator statycznych stron, który w połączeniu z GitHub Pages pozwala na stworzenie darmowego bloga bez konieczności posiadania zaawansowanych umiejętności technicznych. Blog korzysta z Markdown - prostego języka znaczników, który zapewnia przenośność i niezależność treści.

### Zalety tego rozwiązania:
- **Darmowy hosting** na GitHub Pages
- **Własna domena** (opcjonalnie)
- **Markdown** - wolność i przenośność treści
- **Minimalistyczny design** - skupienie na treści
- **Brak baz danych** - statyczne pliki HTML

---

## Tworzenie repozytorium GitHub

1. Zaloguj się na GitHub
2. Utwórz nowe repozytorium o nazwie: `(twoja-nazwa-użytkownika).github.io`
   - Przykład: jeśli Twój login to `jankowalski`, repozytorium powinno nazywać się `jankowalski.github.io`
3. Ustaw repozytorium jako publiczne
4. Zainicjalizuj z plikiem README (opcjonalnie)

---

## Struktura projektu

Podstawowa struktura katalogów i plików:

```
repository-root/
├── _config.yml              # Główny plik konfiguracyjny
├── _posts/                  # Katalog z postami
│   └── YYYY-MM-DD-post-title.md
├── _layouts/                # Szablony layoutów
│   └── default.html
├── index.md                 # Strona główna
├── search.json              # Plik dla wyszukiwarki
├── about.md                 # Strona "O mnie"
├── donate.md                # Strona wsparcia (opcjonalnie)
├── rodo.md                  # Polityka prywatności (opcjonalnie)
└── CNAME                    # Auto-generowany przez GitHub
```

---

## Konfiguracja _config.yml

Utwórz plik `_config.yml` w głównym katalogu projektu z następującą konfiguracją:

```yaml
# Podstawowe informacje
title: Tytuł Twojego Bloga
description: Krótki opis bloga

# URL i ścieżki
url: "https://twoja-domena.pl"  # Twoja domena lub username.github.io
baseurl: ""                      # Puste dla domeny głównej

# Motyw
remote_theme: riggraz/no-style-please

# Permalink (struktura URL)
permalink: /:title/              # Kompatybilna z WordPress struktura

# Wtyczki
plugins:
  - jekyll-feed
  - jekyll-seo-tag
  - jekyll-remote-theme
  - jekyll-sitemap

# Markdown
markdown: kramdown
kramdown:
  syntax_highlighter: rouge
  syntax_highlighter_opts:
    default_lang: html
```

### Kluczowe parametry:

- **title** - tytuł bloga wyświetlany w nagłówku
- **description** - opis używany przez wyszukiwarki
- **url** - pełny adres URL Twojego bloga
- **baseurl** - pozostaw puste dla głównej domeny
- **remote_theme** - motyw Jekyll (w tym przykładzie: minimalistyczny "no-style-please")
- **permalink** - struktura URL dla postów
- **plugins** - wtyczki rozszerzające funkcjonalność Jekyll

---

## Tworzenie postów

### Konwencja nazewnictwa

Pliki postów muszą być nazwane według schematu:

```
YYYY-MM-DD-identyfikator.md
```

**Przykłady:**
- `2026-02-15-hello-world.md` → URL: `/hello-world/`
- `2026-02-10-tutorial-jekyll.md` → URL: `/tutorial-jekyll/`

Data określa kolejność publikacji (najnowsze najpierw), a identyfikator staje się częścią URL.

### Front Matter (nagłówek YAML)

Każdy post wymaga nagłówka YAML:

```markdown
---
layout: post
title: "Tytuł Twojego Posta"
published: true
categories:
  - Programowanie
  - Tutorial
tags:
  - Jekyll
  - GitHub
image: "/images/post-cover.png"
---

# Treść posta

Tutaj piszesz treść w Markdown...
```

### Parametry Front Matter:

- **layout** - szablon layoutu (domyślnie `post`)
- **title** - tytuł posta
- **published** - `true` (opublikowany) lub `false` (wersja robocza)
- **categories** - kategorie posta
- **tags** - tagi
- **image** - obrazek wyróżniający (opcjonalnie)

### Podstawy Markdown

```markdown
# Nagłówek H1
## Nagłówek H2
### Nagłówek H3

**Pogrubiony tekst**
*Kursywa*

[Link](https://example.com)

![Obrazek](ścieżka/do/obrazka.png)

- Lista punktowana
- Punkt drugi

1. Lista numerowana
2. Punkt drugi

`kod inline`

```python
# Blok kodu
def hello():
    print("Hello World")
```
```

---

## Tworzenie layoutu

Utwórz katalog `_layouts` i plik `default.html`:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
  {% include head.html %}
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{{ page.title }} | {{ site.title }}</title>
</head>
<body>
  <header>
    <nav>
      <a href="/">Strona główna</a>
      <a href="/about/">O mnie</a>
      <a href="/search/">Szukaj</a>
    </nav>
  </header>

  <main>
    {{ content }}
  </main>

  <footer>
    <p>&copy; {{ site.time | date: '%Y' }} {{ site.title }}</p>
  </footer>
</body>
</html>
```

### Kluczowe elementy:

- `{% include head.html %}` - ładuje automatyczne zależności stylów
- `{{ page.title }}` - tytuł strony
- `{{ site.title }}` - tytuł bloga z _config.yml
- `{{ content }}` - miejsce na treść strony/posta
- `{{ site.time | date: '%Y' }}` - aktualny rok

---

## Implementacja wyszukiwarki

Utwórz plik `search.json` w głównym katalogu:

```liquid
---
layout: none
---
[
  {% for post in site.posts %}
    {
      "title"    : "{{ post.title | escape }}",
      "category" : "{{ post.category }}",
      "tags"     : "{{ post.tags | join: ', ' }}",
      "url"      : "{{ site.baseurl }}{{ post.url }}",
      "date"     : "{{ post.date | date: '%Y-%m-%d' }}",
      "content"  : {{ post.content | strip_html | jsonify }}
    } {% unless forloop.last %},{% endunless %}
  {% endfor %}
]
```

Ten plik generuje indeks JSON wszystkich postów, który może być wykorzystany przez bibliotekę wyszukiwania typu `simple-jekyll-search`.

### Dodanie wyszukiwarki do strony:

Utwórz `search.md`:

```markdown
---
layout: default
title: Wyszukiwarka
---

<div id="search-container">
  <input type="text" id="search-input" placeholder="Szukaj...">
  <ul id="results-container"></ul>
</div>

<script src="https://unpkg.com/simple-jekyll-search@latest/dest/simple-jekyll-search.min.js"></script>
<script>
  SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('results-container'),
    json: '/search.json'
  })
</script>
```

---

## Konfiguracja domeny

### Dla domeny głównej (apex domain):

Dodaj w ustawieniach DNS swojego dostawcy domeny:

**Rekordy A** (wszystkie cztery):
```
@    A    185.199.108.153
@    A    185.199.109.153
@    A    185.199.110.153
@    A    185.199.111.153
```

**Rekord CNAME dla www**:
```
www    CNAME    twoja-nazwa.github.io
```

### Dla subdomeny (np. blog.domena.pl):

**Rekord CNAME**:
```
blog    CNAME    twoja-nazwa.github.io
```

### Czas propagacji DNS

Zmiany DNS mogą zająć od kilku minut do 48 godzin.

---

## Ustawienia GitHub Pages

1. Przejdź do repozytorium na GitHub
2. Kliknij **Settings** (Ustawienia)
3. W menu po lewej wybierz **Pages**
4. W sekcji **Source**:
   - Branch: `main` (lub `master`)
   - Folder: `/root`
5. Kliknij **Save**

### Własna domena:

1. W sekcji **Custom domain** wpisz swoją domenę (np. `blog.domena.pl`)
2. GitHub automatycznie utworzy plik `CNAME` w repozytorium
3. Poczekaj na weryfikację DNS
4. Po weryfikacji zaznacz **Enforce HTTPS** dla bezpiecznego połączenia

---

## Filozofia minimalizmu

> "Treść jest kluczowa i stanowi prawdziwą wartość bloga"

Artykuł Tomasza Dunii promuje podejście minimalistyczne:
- Skupienie na **jakości treści** zamiast wizualnych dodatków
- **Markdown jako wolność** - przenośność treści
- Brak rozpraszaczy i zbędnych widgetów
- Szybkie ładowanie dzięki statycznym stronom

---

## Podsumowanie

Gratulacje! Masz już działający blog oparty na Jekyll i GitHub Pages:

✅ Darmowy hosting
✅ Własna domena
✅ Posty w Markdown
✅ Wyszukiwarka
✅ SEO i RSS
✅ HTTPS

---

## Źródło i licencja

Tutorial oparty na artykule **Tomasza Dunii**: [blog.tomaszdunia.pl/blog-jekyll-github](https://blog.tomaszdunia.pl/blog-jekyll-github/)

Treść udostępniona na licencji **CC BY-SA 4.0**

---

**Powodzenia z blogowaniem!** 🎉
