# C&C Coatings Website

Live at **https://cccoatings.com** (www redirects there). Single-page site for
**C&C Coatings**, Sarnia, Ontario: Teflon™/PTFE non-stick and release coatings,
Halar® ECTFE, low-friction fluoropolymers, sandblasting and powder coating.

- 1380 Lougar Ave, Sarnia, ON N7S 5N7
- (519) 332-8175 · tom@cccoatings.com
- Mon–Fri 8:30 am – 4:30 pm

## How it is hosted

| Piece | Where | Notes |
|---|---|---|
| Site files | this repo, `main` branch | every push to `main` deploys automatically |
| Hosting | GitHub Pages | free; `.github/workflows/pages.yml` publishes `index.html`, `404.html`, `assets/`, `CNAME`, `robots.txt`, `sitemap.xml` |
| DNS | Cloudflare (account: tom@cccoatings.com) | A/AAAA records point at GitHub Pages, "DNS only" (grey cloud); MX/SPF/DMARC for Google Workspace mail are unchanged |
| Domain registration | GoDaddy, currently in Abstract Marketing's account | transfer into Tom's GoDaddy account requested Nov 2026; paid up to 2027-04-27 |
| Email | Google Workspace | nothing on the web host; not affected by the site |
| HTTPS | GitHub-issued certificate, "Enforce HTTPS" on | automatic renewal |

`docs/hosting-migration.md` records how the move off Abstract Web Host was done.

## Editing the site

There is no build step. Edit `index.html`, open it in a browser to check, commit to
`main`, push. GitHub deploys it within about a minute. `v1.0-prelaunch` and later
tags mark approved versions if you ever need to go back.

## Structure

- `index.html` — the whole site: layout, styles, scripts, content
- `404.html` — shown for old URLs from the previous site; sends visitors to the home page
- `robots.txt`, `sitemap.xml` — search-engine hints (sitemap is submitted in Google Search Console)
- `CNAME`, `.nojekyll` — GitHub Pages custom-domain config
- `assets/` — logos, photos, favicons; `assets/video/black-white.mp4` is the 8.5 s intro clip (trimmed from BLACK WHITE.mp4)
- `reference/` — source material, not part of the live site:
  - `old-site-snapshot.mhtml` — saved copy of the previous website
  - `old-site-images/` — images extracted from the old site
  - `old-versions/` — earlier drafts of the page

## What the page does

- Desktop: fixed red sidebar (logo, contact, Get a Quote, hours), coating names either
  side of the intro video with hover cards, scroll-linked RAL colour strip on the right
  edge (click a colour to add it to the quote), services, quote form.
- Phone: compact red header, eight coating words with tap cards, video, RAL ribbon down
  the right edge, pinned Get a Quote bar, "Email us a photo" quick-quote button.
- Quote requests open the visitor's email app addressed to tom@cccoatings.com with the
  details pre-filled (subject starts "Website quote request"). No form service, no cost.

## To do

- [ ] Replace the three stock process photos with real photos of C&C's shop and finished work
- [ ] Domain transfer: Abstract Marketing to move cccoatings.com into Tom's GoDaddy account (email sent Nov 2026)
- [ ] After the transfer, decline the Abstract Marketing hosting renewal (end of December)
- [ ] Optional: trim the SPF record in Cloudflare to `v=spf1 include:_spf.google.com ~all` (drops the old host's server)
- [ ] Optional: one page per service (Teflon/PTFE, Halar, sandblasting, powder) for better search ranking
- [ ] Optional: Formspree or similar if desktop quote requests don't arrive via the mail-app route
