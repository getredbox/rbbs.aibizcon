# Homepage

Documentation for how `index.html` was created and how it is structured.

## Purpose

`index.html` is a single-page marketing site for **CCBIZCON 2025** — a free Bay Area event on AI, governance, risk, and compliance. The page promotes registration, agenda, speakers, sponsors, and FAQ content, with outbound links to [ccbizcon.com](https://ccbizcon.com).

**Event details baked into the page:**

| Field | Value |
|-------|-------|
| Date | September 17, 2025 |
| Time | 1:00 PM – 5:00 PM |
| Location | Brentwood, CA (East Bay) |
| Contact | info@ccbizcon.com |

---

## How it was created

### Approach

The homepage was built as **one self-contained HTML file** (~1,929 lines). There is no build step, bundler, or framework — open the file in a browser to preview.

| Layer | Location in `index.html` | Notes |
|-------|--------------------------|-------|
| Structure | `<body>` (~lines 1163–1891) | Semantic sections with HTML comments |
| Styles | `<style>` in `<head>` (~lines 9–1161) | All CSS inline; no external stylesheet |
| Behavior | `<script>` before `</body>` (~lines 1893–1926) | Vanilla JS only |

**External dependencies (CDN only):**

- [Google Fonts](https://fonts.googleapis.com): Bebas Neue (display), Barlow Condensed (labels/UI), Barlow (body)

No npm packages, React, or asset pipeline.

### Design direction

A dark, tech-forward visual system was defined with CSS custom properties:

```css
--cyan: #00F5FF;
--magenta: #C840E9;
--dark-bg: #0A0A12;
--card-bg: #0F0F1E;
```

**Visual motifs:**

- Fixed 60px grid overlay on `body::before`
- Radial glow blobs in the hero
- Scanline overlay on `.hero::after`
- Angled “cut” buttons via `clip-path: polygon(...)`
- Scroll-triggered `.fade-up` reveals

### Hero: animated neural-network SVG

The hero includes a custom inline SVG (~lines 1185–1365) — a 5-layer network graphic with:

- Static dim connection lines between layers
- Animated gradient “signal” paths (`lineFlow1`–`lineFlow3` with SMIL `<animate>`)
- Glowing node halos, rings, and cores in cyan/magenta
- Layer labels: INPUT → LAYER 1 → CORE → LAYER 3 → OUTPUT

This was authored directly in SVG inside the HTML (no image files).

### Content sections (top to bottom)

| Section | `id` / class | Purpose |
|---------|--------------|---------|
| Nav | fixed `<nav>` | Anchor links + “Register Now” CTA |
| Hero | `.hero` | Title, subtitle, CTAs, event stats bar |
| Stats strip | `.stats-strip` | 4+ hours, 10+ speakers, 6 frameworks, Bay Area |
| About | `#about` | Three topic pillars + “Who Should Attend” |
| Frameworks | `.frameworks` | PCI, NIST, GLBA, CMMC, HIPAA, SOC 2, ISO 27001, AI Act |
| Agenda | `#agenda` | 1:00–4:30 PM schedule (6 blocks) |
| Speakers | `#speakers` | Four placeholder speaker cards |
| Register | `#register` | Client-side form (no backend) |
| Location | `#location` | Date/time/venue + map placeholder |
| Sponsors | `#sponsors` | Gold / Silver / Bronze placeholder slots |
| FAQ | `#faq` | 8 accordion items |
| Footer | `<footer>` | Links + © 2025 |

### JavaScript (minimal)

Three behaviors at the bottom of the file:

1. **`IntersectionObserver`** — adds `.visible` to `.fade-up` elements on scroll
2. **`toggleFaq(item)`** — accordion; only one FAQ open at a time
3. **`handleRegister()`** — validates required fields; on success opens `https://ccbizcon.com` in a new tab (form is not submitted to a server)

### Placeholder content to replace later

These areas use template/placeholder copy and should be updated when real assets exist:

- **Speakers** — fictional names (Jordan Chen, Aisha Morales, etc.)
- **Sponsors** — “Your Logo” cards in Gold/Silver/Bronze tiers
- **Map** — `.map-placeholder` instead of an embedded map
- **Registration** — collects input locally then redirects to ccbizcon.com

---

## How to view and edit

**Preview:** Double-click `index.html` or run from the project root:

```bash
# Optional: local server (avoids some file:// quirks)
npx serve .
```

**Edit workflow:**

1. **Copy** — search the file for event names, dates, emails, and agenda text
2. **Styles** — change tokens in `:root` at the top of `<style>` for global theme updates
3. **Sections** — each block is marked with `<!-- NAV -->`, `<!-- HERO -->`, etc.
4. **New section** — copy an existing `<section>`, add a nav link, and reuse `.section-tag` / `.section-title` / `.fade-up` patterns

**Responsive:** Breakpoint at `768px` hides nav links and stacks grids to a single column.

---

## Project layout

```
Seana Bizcon/
├── index.html          # Full homepage (this file)
└── docs/
    └── homepage.docs.md
```

---

## Summary

`index.html` was created as a **zero-dependency, single-file landing page**: embedded CSS design system, inline animated SVG hero, anchor-based single-page navigation, and light vanilla JS for scroll animation, FAQ accordion, and registration redirect. No separate assets folder — everything ships in one file for easy hosting (static file server, S3, Netlify, or email attachment).
