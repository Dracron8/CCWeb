# C&C Coatings Website

Website for **C&C Coatings** — powder coating and PTFE/fluoropolymer non-stick coatings in Sarnia, Ontario.

- 1380 Lougar Ave, Sarnia, ON N7S 5N7
- (519) 332-8175 · tom@cccoatings.com
- www.cccoatings.com

## Structure

- `index.html` — the site (single page, no build step; just open it in a browser)
- `assets/` — logos and photos used by the page; `assets/video/black-white.mp4` is the 8.5 s intro clip (trimmed from BLACK WHITE.mp4)
- `reference/` — source material, not part of the live site:
  - `old-site-snapshot.mhtml` — saved copy of the previous website
  - `old-site-images/` — images extracted from the old site
  - `old-versions/` — earlier drafts of the current page

## To do

- [ ] Quote form doesn't actually send anything (it only shows an alert) — hook it up to a form service (e.g. Formspree/Netlify Forms) or a mailto fallback
- [ ] Replace stock photos with real photos of C&C's shop and finished work
- [ ] Decide on hosting (GitHub Pages works for a static page like this)
