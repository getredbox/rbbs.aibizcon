# Update history

Changelog of content and layout updates delivered by the external web developer for the AIBIZCON/CCBIZCON landing page (`index.html`). Each entry is compared against the site version in git immediately before integration.

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
