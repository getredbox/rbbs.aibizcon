# Homepage

Documentation for how `index.html` is structured and maintained.

## Purpose

`index.html` is a single-page marketing site for **AIBIZCON 2026** — a free Bay Area event on AI, governance, risk, and compliance. The page promotes registration, agenda, speakers, sponsors, and FAQ content.

**Event details baked into the page:**

| Field | Value |
|-------|-------|
| Primary event | **AIBIZCON** · September 17, 2026 · 1:00 PM – 5:00 PM |
| Companion (hero) | **CCBIZCON** · September 18, 2026 · 9:00 AM – 5:00 PM |
| Location | Brentwood, CA (East Bay) — 35 Oak St |
| Registration | https://ccbizcon2026.eventbrite.com |
| Contact | info@aibizcon.com |

---

## How it was created

### Approach

The homepage is **one self-contained HTML file** (~2,377 lines). There is no build step, bundler, or framework — open the file in a browser to preview.

| Layer | Location in `index.html` | Notes |
|-------|--------------------------|-------|
| SEO / JSON-LD | `<head>` | AIBIZCON-first meta, OG, Twitter, Event + FAQPage schema |
| Styles | `<style>` in `<head>` | All CSS inline; no external stylesheet |
| Structure | `<body>` | Skip link, `<main id="main-content">`, semantic sections |
| Behavior | Inline `<script>` before `</body>` | Vanilla JS only |

**External dependencies (CDN only):**

- [Google Fonts](https://fonts.googleapis.com): Bebas Neue (display), Barlow Condensed (labels/UI), Barlow (body)

No npm packages, React, or asset pipeline. Speaker/sponsor images are **base64-inlined** in HTML; matching files also live under `images/` for asset inventory.

### Design direction

A dark, tech-forward visual system with CSS custom properties (`--cyan`, `--magenta`, `--dark-bg`, `--card-bg`). Motifs include a fixed grid overlay, hero glow blobs, scanline overlay, angled clip-path buttons, and scroll-triggered `.fade-up` reveals.

### Hero layout (canonical — do not regress)

Centered stack inside `.hero-main` > `.hero-copy`:

1. Dual `.hero-tag` lines (AIBIZCON + CCBIZCON)
2. `.hero-title` / `.hero-subtitle`
3. `.hero-ai-graphic` (neural-network SVG under subtitle; height capped at 180px)
4. Description + CTAs
5. `.hero-event-bar`

Do not use `.hero > * { position: relative }` or place the SVG before the title — both create a large empty gap.

### Content sections (top to bottom)

| Section | `id` / class | Purpose |
|---------|--------------|---------|
| Nav | fixed `<nav aria-label>` | Anchor links + Eventbrite CTA |
| Hero | `.hero` | Dual event tags, title, graphic, CTAs, event bar |
| Stats strip | `.stats-strip` | 12+ hours, 12+ speakers, 6 topics, Bay Area |
| About | `#about` | Topic pillars + “Who Should Attend” |
| Agenda | `#agenda` | Afternoon session schedule |
| Speakers | `#speakers` | 11 featured speakers (incl. Mike Pawlawski) |
| Register | `#register` | Eventbrite CTA |
| Location | `#location` | Venue, map link, Sept 17 **2026** |
| Sponsors | `#sponsors` | Diamond / Gold / Silver / Bronze |
| FAQ | `#faq` | 8 accordion items |
| Footer | `<footer>` | Links + © **2026** |

### Sponsors (current)

- **Diamond:** CCA Business & Technology Advisors, Sutter Health
- **Gold:** BLOKWORX, Edward Jones, Structure Groups, The 20, Galactic Advisors
- **Silver:** 4× “Your Logo” placeholders
- **Bronze:** BizBotz, First Citizens Bank, Little Owl Design, Global Office Inc, Starbucks - Streets of Brentwood, Cytracom

### JavaScript (minimal)

1. **`IntersectionObserver`** — adds `.visible` to `.fade-up` on scroll
2. **`toggleFaq(item)`** — accordion; one open at a time
3. **`handleRegister()`** — opens Eventbrite registration URL

---

## How to view and edit

**Preview:**

```bash
npx serve .
```

**Edit workflow:**

1. Prefer integrating developer deliveries via the `aibizcon-developer-update` skill (keep hero/SEO/a11y/year fixes)
2. **Styles** — tokens in `:root` at the top of `<style>`
3. **Sections** — marked with HTML comments; reuse `.section-tag` / `.section-title` / `.fade-up`
4. After `index.html` changes, update `docs/update-history.docs.md` and related docs/`llms.txt`

**Responsive:** Breakpoint at `768px` hides nav links and stacks grids.

---

## Project layout

```
rbbs.aibizcon/
├── index.html
├── images/                 # Logos and headshots (also base64 in HTML)
├── llms.txt
├── robots.txt
├── sitemap.xml
├── CNAME
├── temp/                   # gitignored scratch (developer drops, scripts)
└── docs/
    ├── homepage.docs.md
    ├── deploy.docs.md
    └── update-history.docs.md
```

---

## Summary

`index.html` is a **zero-dependency, single-file landing page** for AIBIZCON 2026: embedded CSS, inline hero SVG, Eventbrite CTAs, and light vanilla JS. Production keeps local hero layout, SEO, and accessibility shells when merging developer body updates.
