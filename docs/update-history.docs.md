# Update history

Changelog of content and layout updates delivered by the external web developer for the AIBIZCON/CCBIZCON landing page (`index.html`). Each entry is compared against the site version in git immediately before integration.

---

## 2026-08-12 20:35:56 — Developer update (speakers + sponsors)

**Source:** `temp/20260812 Updates/ccbizcon-website (2).html`  
**Compared to:** production `index.html` (post–2026-06-18 local fixes)  
**Integrated into:** `index.html` (+ docs / `llms.txt` / `images/` listed below)

### From developer delivery

| Change | Notes |
|--------|-------|
| Speakers | Replaced Gretchen Evans with **Mike Pawlawski**; removed **Crystal Conkle** (11 speakers) |
| Sponsors | New **Diamond** tier (CCA, Sutter Health); Gold adds Galactic Advisors; refreshed Edward Jones logo; Bronze adds Global Office Inc, Starbucks - Streets of Brentwood, Cytracom |
| Assets | New logos/headshot copied into `images/` (HTML remains base64-inlined) |

### Fixed locally (hero / SEO / a11y / year)

| Change | Notes |
|--------|-------|
| Hero / SEO / a11y | Kept production `<head>`, skip link, `<main id="main-content">`, centered `hero-main` / `hero-copy` stack |
| Year | Location date and footer remain **2026** (developer file had 2025) |
| Internal links | Kept production section intro links (speakers, sponsors, etc.) |
| Alt text | Corrected Mike Pawlawski `alt` (developer file still said Gretchen Evans) |
| JSON-LD | Refreshed `Event.performer` list to match new speakers |
| Responsive | Diamond sponsor cards full-width on small screens (same as gold) |

### Docs updated

- `docs/update-history.docs.md` — this entry
- `docs/homepage.docs.md` — event dates, speakers/sponsors structure
- `llms.txt` — speaker/sponsor summary line

### Follow-up items

- FAQ still says “Gold, Silver, and Bronze” (no Diamond) — leave until developer updates copy
- Stats strip still shows “12+ Expert Speakers” with 11 listed
- New diamond/gold/bronze sponsor cards mostly lack outbound `href`s (as delivered)
- Optional: wire base64 embeds to `images/` file paths later

---

## 2026-06-18 — Developer update (stats + Mark Adair)

**Based on:** `temp/index.20260618-update.html` (developer delivery)  
**Compared to:** commit `b241681`  
**Integrated into:** `index.html`

### From developer delivery

| Change | Notes |
|--------|-------|
| Stats strip | Hours of Content: `4+` → `12+` |
| Mark Adair | Role: IT Business Owner, Adair Technology Compliance; updated headshot image |

### Fixed locally (not in raw developer file)

| Change | Notes |
|--------|-------|
| Year | Location date and footer remain **2026** (developer file had 2025) |
| SEO / a11y / links | Production `<head>`, JSON-LD, skip link, internal section links, hero layout unchanged |

### Docs updated

- `docs/update-history.docs.md` — this entry
- `docs/homepage.docs.md` — stats strip note

---

## 2026-06-17 — Location map link visibility

**Integrated into:** `index.html`

### Fixed locally

| Change | Notes |
|--------|-------|
| Venue image layout | Label overlay scoped to `.venue-image-frame` only — was anchored to full wrap and overlapped the Google Maps link |
| Map link | Larger padding/font; sits below image frame with clear gap |

### Docs updated

- `docs/update-history.docs.md` — this entry

---

## 2026-06-17 — SEO audit recommendations (Open WebUI)

**Based on:** Open WebUI SEO audit of `https://www.aibizcon.me/`  
**Integrated into:** `index.html`

### Implemented

| Change | Notes |
|--------|-------|
| JSON-LD expansion | `FAQPage` (8 Q&amp;A), `Person` performers on `Event`, postal code, free-ticket `Offer`, event `url`/`image` |
| Internal links | Contextual in-section links (hero, about, agenda, speakers, register, location, sponsors, FAQ) |
| Footer Connect | Eventbrite registration link added |
| Title &amp; keywords | Reverted audit-only keyword phrases; title/keywords match developer-facing copy only |
| Link styling | `.section-body a` / `.hero-desc a` use site cyan |

### Reverted (developer content authority)

Audit-suggested keyword targets (**CISO networking event**, **compliance workshop 2026**, **cybersecurity leadership conference**, **NIST framework training**) were removed from `<title>` and `meta keywords`. Those phrases are not in the developer’s body copy; SEO meta should describe the page as written, not invent positioning.

### Deferred (per site owner)

| Item | Notes |
|------|-------|
| `favicon.ico` | Not added — no favicon asset yet |

### Docs updated

- `docs/update-history.docs.md` — this entry
- `docs/deploy.docs.md` — structured data and favicon note
- `.cursor/skills/aibizcon-seo/` — SEO-while-building skill (project pattern)

---

## 2026-06-17 — Remove internal docs from llms.txt

**Change:** Dropped `## Documentation` links to `docs/` and `README.md` from `llms.txt`. Those paths are maintainer-only (`robots.txt` disallows `/docs/`); listing them in a sitemap-listed file exposed URLs to crawlers without SEO benefit.

### Docs updated
- `llms.txt` — removed Documentation section
- `docs/deploy.docs.md` — clarified llms.txt is public/LLM-facing only
- `docs/update-history.docs.md` — this entry

---

## 2026-06-17 — SEO, hero layout, and 2026 year fixes

**Based on:** `temp/index.20260617-update.html` (developer delivery)  
**Integrated into:** `index.html`

### Kept from developer delivery (body content)

- Nav/footer **AIBIZCON** branding, dual hero date lines (AIBIZCON + CCBIZCON)
- Hero event bar, stats strip, agenda, speakers, sponsors, FAQ, register, and location copy unchanged from developer file

### Added or fixed locally (not in raw developer file)

| Change | Notes |
|--------|-------|
| Hero layout | Centered stack (`hero-main` / `hero-copy`); neural-network graphic under subtitle; SVG height capped |
| SEO `<head>` | AIBIZCON-first title, meta, Open Graph, Twitter Card, JSON-LD (`Event` for AIBIZCON 2026) |
| Accessibility | Skip link, `<main id="main-content">`, nav `aria-label` |
| Year corrections | Location date and footer `© 2026` (developer file still had 2025 in those spots) |

### Follow-up items

- Add dedicated `og:image` (1200×630) for social sharing
- Developer may update location/footer to match hero 2026 dates in a future delivery

---

## 2026-06-17 11:11:33 — Developer delivery (`index.20260617-update.html`)

**Source file:** `index.20260617-update.html` (saved 2026-06-17 11:11:33 local time)  
**Compared to:** `index.html` at commit `8db5009` (2026-06-15 12:21:02 PDT)  
**Integrated into:** `index.html` (hero layout repaired; existing SEO and accessibility markup retained)

### Content changes

| Area | Before | After |
|------|--------|-------|
| Navigation logo | `CC`BIZCON | `AI`BIZCON |
| Footer logo | `CC`BIZCON | `AI`BIZCON |
| Hero event line(s) | September 17, 2025 · Brentwood, CA | **AIBIZCON** · September 17, 2026 · 1PM–5PM · Brentwood, CA |
| | | **CCBIZCON** · September 18, 2026 · 9AM–5PM · Brentwood, CA |

### Unchanged in this delivery

- Page `<title>` still reads **AIBIZCON 2025**
- Location section still shows **September 17, 2025**
- Footer still shows **© 2025**
- Agenda, speakers, sponsors, FAQ body copy (no text differences detected vs. prior `index.html`)
- Eventbrite registration link (`https://ccbizcon2026.eventbrite.com`) unchanged
- Speaker photos remain embedded as base64 data URIs (not external image files)

### Layout / delivery issues (fixed on integration)

The raw developer file regressed the hero layout that had been fixed on 2026-06-15:

1. **Large empty gap** at the top of the hero — caused by the neural-network SVG’s glow filters (`overflow: visible`, unconstrained height) inflating the layout box.
2. **Hero alignment reset** — content order and CSS no longer matched the centered stack used in production (`hero-main` / `hero-copy`, graphic under subtitle).

On integration, hero CSS and HTML order were restored to match the prior production layout while keeping the developer’s content changes above.

### Follow-up items (not addressed by developer)

- Align page title, location block, footer year, and JSON-LD event dates with the **2026** dual-event schedule shown in the hero.
- Consider adding a dedicated `og:image` for social sharing.

---

## 2026-06-15 12:12:38 PDT — Developer delivery (integrated as commit `93a12f3`)

**Compared to:** `index.html` before the refresh (commit `b9d39d9`, 2026-06-12)  
**Commit message:** `fix: refresh AIBIZCON homepage and repair hero two-column layout`

### Summary

Major homepage refresh delivered by the web developer and merged locally:

- Rebuilt `index.html` with updated agenda, speakers, sponsors, and Eventbrite CTAs
- Added speaker headshots and sponsor logos under `images/` (also embedded inline in HTML)
- Introduced neural-network hero graphic and two-column hero layout (later adjusted in `8db5009` to center the graphic under the subtitle)
- Branding in nav still showed **CCBIZCON** at this stage; site title referenced CCBIZCON 2025

A follow-up hero layout fix (`8db5009`, 2026-06-15 12:21:02 PDT) centered the hero stack and moved the neural-network graphic below the subtitle before the 2026-06-17 developer delivery arrived.
