# Eigenwijsje — Jekyll site

Static, developer-maintained site. No CMS, no database — content lives in
`index.html` (and any new `.md`/`.html` pages you add), styling in
`assets/css/style.css`, shared chrome in `_includes/` and `_layouts/`.

The "Plan een kennismaking" / "Stuur een e-mail" buttons and the Contact
line in the footer all link straight to `mailto:christine@eigenwijsje.nl`
(configured once in `_config.yml` under `contact_email`, so it only needs
updating in one place). There's no contact form and nothing to submit to a
backend — this is a fully static site.

## Local development

Requires Ruby + Bundler.

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`. Jekyll watches files and rebuilds on save.

## Project structure

```
eigenwijsje/
├── _config.yml          site title, nav items, contact email
├── Gemfile               matches the gem versions GitHub Pages builds with
├── index.html             homepage content (front matter + hero/mission/etc. sections)
├── _layouts/
│   └── default.html       shared <head>, wraps every page with header/footer
├── _includes/
│   ├── header.html         nav (reads site.nav from _config.yml)
│   └── footer.html         contact block + CTA, both mailto
└── assets/
    ├── css/style.css       the approved mockup's styling, unchanged
    └── images/logo.jpg
```

## Adding another page

Create e.g. `over-ons.html` in the project root:

```html
---
layout: default
title: Over ons
---

<section class="wrap" style="padding:60px 0;">
  <h1>Over ons</h1>
  <p>...</p>
</section>
```

It'll automatically get the same header/footer/styling, reachable at
`/over-ons/`. Add it to `site.nav` in `_config.yml` to link it from the header.

## Deploying to GitHub Pages

1. Push this folder to a GitHub repo.
2. Repo → **Settings → Pages** → Source: **Deploy from a branch** →
   `main` / `/ (root)`. GitHub Pages runs Jekyll automatically — no separate
   build step or GitHub Action needed, since the Gemfile matches its
   built-in Jekyll version.
3. For a custom domain (e.g. `eigenwijsje.nl`): add a `CNAME` file in the
   repo root containing just the domain, and point your DNS at GitHub Pages
   (A records for an apex domain, or a CNAME record for a subdomain like
   `www`). GitHub issues free HTTPS automatically once DNS resolves.

## Before this goes live

- **Fonts** are loaded from the Google Fonts CDN in `_layouts/default.html`.
  For the EU/GDPR-friendly, self-hosted approach discussed earlier, download
  the Fredoka and Karla `.woff2` files into `assets/fonts/` and replace the
  `<link>` tags with local `@font-face` rules in `style.css`.
- **Placeholder details**: phone number was dropped since contact is now
  email-only; KvK number and address in `_includes/footer.html` are still
  placeholders.
- **Cookie consent**: none needed yet since there's no analytics or forms
  wired up — add a lightweight consent banner only if/when you add analytics.
