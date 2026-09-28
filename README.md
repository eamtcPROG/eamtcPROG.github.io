# eamtc.me

Personal site of Mihai Corețchi, full-stack software engineer. Served by GitHub Pages at
[eamtc.me](https://eamtc.me) (see `CNAME`).

Plain HTML, CSS and a few lines of JavaScript. There is no build step: GitHub Pages serves the
files as they are, and `.nojekyll` turns off Jekyll processing.

```
index.html            the page
404.html              not-found page
favicon.svg
assets/css/style.css  styles, with light and dark themes
assets/js/main.js     theme toggle, footer year
assets/img/           portrait
```

## Preview locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Editing

- **Content** lives in `index.html`, one `<section>` per part of the page.
- **Colours and fonts** are CSS variables at the top of `assets/css/style.css`. The dark theme
  redefines them twice: once for the system preference and once for the manual toggle.
- **A new project** is another `<article class="project">` inside `.project-grid`.
