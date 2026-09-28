# eamtc.me: personal site

## What this is

Portfolio for Mihai Corețchi, full-stack software engineer in Chișinău. GitHub Pages serves it from
`main` at **https://eamtc.me**. The custom domain lives in `CNAME`.

## Stack

Plain HTML, CSS and a little JavaScript. No package manager, no framework, no dependencies beyond
Google Fonts (Newsreader, IBM Plex Sans, IBM Plex Mono). Keep it that way unless the owner asks
otherwise.

GitHub Pages builds the site with Jekyll, but **only to leave files out**. `_config.yml` does
three things:

- `theme: null` stops Pages applying its default Primer theme. Primer's
  `assets/css/style.scss` would otherwise compile over our `assets/css/style.css`.
- `exclude` lists repo-only files: `CLAUDE.md`, `README.md` and `CNAME`. **A new repo-only file
  must be added there**, or it is published at eamtc.me/<file>. Names starting with `.` or `_`
  are skipped automatically.
- No page has front matter, so Jekyll copies every file through byte-for-byte. Don't add front
  matter or Liquid tags (`{{ }}`, `{% %}`) unless you mean to use Jekyll.

Don't bring back `.nojekyll`. It makes Pages serve every file in the repo, CLAUDE.md included.

```
index.html            the whole page, one <section> per part
404.html              not-found page (root-relative paths, reuses style.css)
assets/css/style.css  tokens, components, responsive rules
assets/js/main.js     theme toggle, mobile menu, scroll reveal, nav highlighting, footer year
assets/img/           portrait: 224×336 and a 2× copy at 448×672 (keep the 2:3 ratio)
favicon.svg           "MC" monogram
CNAME                 eamtc.me (custom domain; not published)
_config.yml           Jekyll: no theme, exclude list
```

## Run and check

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

To see exactly what Pages will publish, build with the `github-pages` gem (the same Jekyll
version and plugins GitHub uses). Put a Gemfile outside the repo containing
`gem "github-pages", group: :jekyll_plugins`, then:

```bash
LANG=C.UTF-8 BUNDLE_GEMFILE=/path/to/Gemfile bundle exec jekyll build --safe --source . --destination /tmp/_site
```

`/tmp/_site` should contain only the site files, each byte-identical to its source, and no
`CLAUDE.md` or `README.md`.

Before pushing, render the page in a real browser (Playwright/Chromium screenshots work well).
Check it at 1280, 820, 390 and 320 px wide, in both light and dark mode:

- no horizontal scroll: `document.documentElement.scrollWidth` equals the viewport width
- no console errors
- the mobile menu (below 900 px) opens, closes on a link click and closes on Escape
- every `.reveal` element becomes visible after scrolling, and is visible straight away with
  reduced motion
- the repo grid has an even number of half-width cards, so no card sits alone on the last row

## Deploy

- `main` is live. Every push to `main` triggers "pages build and deployment" (about 30 s).
  Work on a branch, open a PR, and merge it to deploy.
- **Never delete or edit `CNAME`.** Without it the site drops off eamtc.me.
- GitHub issues the HTTPS certificate itself (Let's Encrypt); you can't upload one. If
  "Enforce HTTPS" is stuck, remove and re-add the domain under Settings → Pages. If the DNS has
  CAA records, one of them must allow `letsencrypt.org`.

## Content rules (read before editing copy)

The page describes a real person, and recruiters and clients read it. Accuracy beats polish.

- **Every claim needs a source:** the owner's CV or a repository. Don't invent metrics, clients,
  dates, job titles or technologies. If a fact is unknown, leave it out and ask.
- **Tags list only what the source names** for that project. For example, the CV names no stack
  for the storefronts, so their tags stay generic.
- **Team repositories:** describe only the owner's part, taken from the commit history, and mark
  the card `team`. A feature a README plans but the code doesn't implement is not claimed. PAD's
  circuit breaker is one example.
- **Only public repositories appear.** Check a repo's visibility before featuring it, and never
  name a private repo here or on the page. This file is public too.
- **Privacy:** no date of birth, gender, nationality, street address or phone number. Show the
  city only. The contact email is `mihai.coretchi17@gmail.com`.
- **Hand-maintained facts to keep current:** the four hero stats (9 client products, 40+ public
  repos, clients since 2022, MSc), "Dec 2022 — present", and the Master's dates. The Master's
  "2025 — present" was inferred from course repos, so confirm it with the owner before relying
  on it.
- **"Used in" links** in Skills point at project card ids (`#p-iftamaster`, `#p-dasi`, …). When
  you add, rename or remove a card, update the links. A link to a missing id fails silently.
- **Voice:** first person, plain and specific, no marketing adjectives. British spelling in prose
  (colour, behaviour, Dockerised, travelling). Code identifiers stay as they are.

## Design system

- **Tokens** are CSS variables on `:root`. The dark theme is defined **twice**: once under
  `@media (prefers-color-scheme: dark)` guarded by `:root:not([data-theme="light"])`, and again
  under `:root[data-theme="dark"]` for the manual toggle. Change both together.
- **Accent** is indigo `#3f4bb0` (`#a5aef3` in dark mode). Newsreader is for display headings
  only; body text uses Plex Sans; labels, tags and metadata use Plex Mono.
- **Components:** `.section-head` (number, title, intro), `.card`, `.card-featured`, and
  `.repo`, whose link covers the whole card via `::after`. Also `.tags`, `.chips`, the `.core`
  skill tiles, the `.toolbox` rows, `.stats`, and `.contact-card`.
- **Scroll reveal** only hides elements when `<html>` has the `js` class, so the page still works
  without JavaScript. Keep that guard.
- **Accessibility target is WCAG 2.2 AA:** landmarks, a skip link, visible focus, real alt
  text, `aria-label` on icon buttons, and `prefers-reduced-motion` turning off animation.

## Git

Commit subjects are imperative ("Add …", "Restyle …"), and the body explains why. Branch from
`main`, and don't push directly to it.
