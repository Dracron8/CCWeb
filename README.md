# C&C Coatings Website

Website for **C&C Coatings** — powder coating and PTFE/fluoropolymer non-stick coatings in Sarnia, Ontario.

- 1380 Lougar Ave, Sarnia, ON N7S 5N7
- (519) 332-8175 · tom@cccoatings.com
- www.cccoatings.com

## Structure

- `index.html` — the site (single page, no build step; just open it in a browser)
- `404.html` — shown for old URLs from the previous site; sends visitors to the home page
- `CNAME`, `.nojekyll` — GitHub Pages custom-domain config
- `.github/workflows/pages.yml` — publishes `index.html` + `assets/` to GitHub Pages on every push to `main`
- `docs/hosting-migration.md` — runbook for moving off the old host
- `assets/` — logos and photos used by the page; `assets/video/black-white.mp4` is the 8.5 s intro clip (trimmed from BLACK WHITE.mp4)
- `reference/` — source material, not part of the live site:
  - `old-site-snapshot.mhtml` — saved copy of the previous website
  - `old-site-images/` — images extracted from the old site
  - `old-versions/` — earlier drafts of the current page

## To do

- [x] Quote form: opens the visitor's email app with the request pre-filled (mailto). Upgrade to a form service (e.g. Formspree) if you want submissions delivered without relying on the visitor's mail app
- [ ] Replace stock photos with real photos of C&C's shop and finished work
- [ ] Hosting: moving to GitHub Pages — see `docs/hosting-migration.md` for the step-by-step (repo must be public, Pages source = GitHub Actions, DNS moves to GoDaddy)
