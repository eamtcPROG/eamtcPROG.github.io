# eamtc.me

Personal site of Mihai Corețchi, full-stack software engineer. Served by GitHub Pages at
[eamtc.me](https://eamtc.me) (see `CNAME`).

Plain HTML, CSS and a few lines of JavaScript. GitHub Pages runs Jekyll over the repo, but
`_config.yml` switches off the default theme and only uses Jekyll to leave repo files (this
README, `CLAUDE.md`, `CNAME`) out of the published site. Every page is copied through unchanged.

```
index.html            the page
404.html              not-found page
favicon.svg
_config.yml           Jekyll config: no theme, files to leave unpublished
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

- **Content** lives in `index.html`, one `<section>` per part of the page: intro and stats,
  experience, client projects, GitHub projects, skills, education, contact.
- **Colours and fonts** are CSS variables at the top of `assets/css/style.css`. The dark theme
  redefines them twice: once for the system preference and once for the manual toggle.
- **A new client project** is another `<article class="card reveal">` inside `.grid-2`.
- **Skills** "Used in" links point at project card ids (`#p-mac`, `#p-dasi`, …). Update them
  when you add, rename or remove a card.
- **A new GitHub project** is another `<article class="card repo reveal">` inside `.repo-grid`.
  Keep an even number of half-width cards so the last row isn't left with one card; smaller
  repos go in the "Also on GitHub" list instead.
- **The portrait** is `assets/img/mihai-coretchi.jpg` (224×336) with a 2× copy (448×672) for
  sharp screens; phones use `mihai-coretchi-avatar.jpg` (160×160) instead. To use a better
  photo, replace all three and keep the portrait at 2:3.

Conventions for editing, especially the content-accuracy and privacy rules, are in `CLAUDE.md`.
