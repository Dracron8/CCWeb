# Moving cccoatings.com off Abstract Web Host onto GitHub Pages

> **Status (2026-11-14): done.** cccoatings.com is live on GitHub Pages with HTTPS.
> The plan below was written for GoDaddy DNS; in practice DNS went to **Cloudflare**
> (Abstract Marketing switched the nameservers on 2026-11-12 at Tom's request), and the
> site records were changed there by API on 2026-11-14. Mail records were not touched.
> Still open: the domain registration moving from Abstract's GoDaddy account to Tom's,
> and cancelling Abstract's hosting after that. Kept for the record.

Snapshot of the current setup, taken 2026-09-12 from public records:

| Item | Current value |
|---|---|
| Registrar | GoDaddy (registered 2005-04-27, expires 2027-04-27) |
| Nameservers | ns1.abstractwebhost.com, ns2.abstractwebhost.com (zone contact: mark@abstractmarketing.ca) |
| Website | Apache on 162.241.159.214 (abs.abstractwebhost.com) |
| Email | Google Workspace (MX at Google). Email is NOT on the web host. |

Nothing below touches email delivery as long as the MX, SPF and DMARC records are
copied exactly. Do the steps in order. **Do not cancel the host until step 6.**

---

## 1. Enable GitHub Pages (Tom, ~2 minutes)

GitHub Pages needs the repo to be **public** (or a paid GitHub plan). The site is
public anyway, and the workflow publishes only `index.html`, `assets/`, `CNAME`
and `.nojekyll`; the `reference/` folder never goes live.

1. GitHub → repo → **Settings → General**, scroll to *Danger Zone* → **Change visibility → Public**.
2. **Settings → Pages** → *Build and deployment* → Source: **GitHub Actions**.
3. Merge this branch into `main` (or push it to `main`). The workflow in
   `.github/workflows/pages.yml` runs and deploys.
4. **Settings → Pages → Custom domain**: enter `cccoatings.com`, save.
   Leave *Enforce HTTPS* unchecked until DNS (step 3) has propagated, then check it.

Check: `https://dracron8.github.io/ccweb/` should show the site.

## 2. Move DNS from Abstract Web Host to GoDaddy (Tom, ~10 minutes)

Do this at GoDaddy → **My Products → Domains → cccoatings.com → DNS**.

a. **Nameservers** → *Change* → *GoDaddy nameservers* (default). GoDaddy will
   then show its own DNS records page for the domain.
b. Delete any records GoDaddy pre-fills (parking A record, `_domainconnect`, etc.).
c. Add every record in section 3 below.

Nameserver changes take up to 48 hours to fully propagate; usually under an hour.

## 3. Records to enter at GoDaddy

### Website (GitHub Pages)

| Type | Name | Value | TTL |
|---|---|---|---|
| A | @ | 185.199.108.153 | 1 hr |
| A | @ | 185.199.109.153 | 1 hr |
| A | @ | 185.199.110.153 | 1 hr |
| A | @ | 185.199.111.153 | 1 hr |
| AAAA | @ | 2606:50c0:8000::153 | 1 hr |
| AAAA | @ | 2606:50c0:8001::153 | 1 hr |
| AAAA | @ | 2606:50c0:8002::153 | 1 hr |
| AAAA | @ | 2606:50c0:8003::153 | 1 hr |
| CNAME | www | dracron8.github.io | 1 hr |

### Email (copied from the current zone; keep identical)

| Type | Name | Value | Priority | TTL |
|---|---|---|---|---|
| MX | @ | aspmx.l.google.com | 1 | 1 hr |
| MX | @ | alt1.aspmx.l.google.com | 5 | 1 hr |
| MX | @ | alt2.aspmx.l.google.com | 5 | 1 hr |
| MX | @ | aspmx2.googlemail.com | 10 | 1 hr |
| MX | @ | aspmx3.googlemail.com | 10 | 1 hr |
| TXT | @ | `v=spf1 include:_spf.google.com -all` | | 1 hr |
| TXT | _dmarc | `v=DMARC1;p=none;sp=none;adkim=r;aspf=r;pct=100;fo=0;rf=afrf;ri=86400` | | 1 hr |

Notes:
- The current SPF also allows the old host's IP (`ip4:162.241.159.214`). It is
  dropped above because nothing should send mail from the old server once the
  site moves. If the old site's contact form was emailing you through the host,
  that is the only thing that used it.
- No DKIM record was found at Google's default selector (`google._domainkey`).
  If Google Admin → Apps → Google Workspace → Gmail → Authenticate email shows
  DKIM as "Authenticating", ask the host for the exact TXT record and copy it,
  or generate a fresh one in Google Admin and add it at GoDaddy.
- `mail.cccoatings.com` currently points at the old server. It is not needed
  (mail is on Google) and is intentionally not recreated.
- No other subdomains were found (checked: www, mail, webmail, cpanel, ftp,
  autodiscover, autoconfig, calendar, docs, sites, blog, shop, m).

## 4. Point the domain at GitHub Pages

Already done by the `CNAME` file in the repo plus the custom-domain setting
in step 1.4. Once DNS has propagated, go back to **Settings → Pages** and tick
**Enforce HTTPS** (GitHub issues the certificate automatically; can take up to
an hour after DNS resolves).

## 5. Verify

- `https://cccoatings.com` and `https://www.cccoatings.com` both load the new site with a valid padlock.
- Send a test email to tom@cccoatings.com from an outside address and reply to it.
- https://toolbox.googleapps.com/apps/checkmx/ → enter `cccoatings.com` → no red errors.

## 6. Cancel Abstract Web Host

Only after step 5 passes. Ask them to confirm in writing that cancelling
hosting does **not** cancel or transfer the domain (the domain is at GoDaddy
and should stay there). Ongoing cost after this: GoDaddy domain renewal only.
