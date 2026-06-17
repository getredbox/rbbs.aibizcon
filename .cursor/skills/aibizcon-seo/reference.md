# AIBIZCON SEO — reference

## Production SEO stack (current pattern)

```text
index.html <head>
├── title, description, keywords, canonical, robots, author, geo.*
├── Open Graph (og:type, url, title, description, locale, site_name)
├── Twitter Card (card, title, description)
└── JSON-LD @graph
    ├── WebSite (+ publisher → Organization)
    ├── Organization (+ sameAs: aibizcon.com, Eventbrite)
    ├── Event (AIBIZCON 2026 — dates, Place, performers, free Offer)
    └── FAQPage (mainEntity from on-page FAQ)

index.html <body>
├── skip-link → #main-content
├── <main id="main-content">
├── section ids: #about #agenda #speakers #register #location #sponsors #faq
├── H1 in hero; H2 per section; H3 in cards/agenda
├── img alt on all images
└── contextual <a href="#..."> in section-body / hero-desc (cyan link style)

Repo root
├── robots.txt
├── sitemap.xml
└── llms.txt
```

## Meta writing rules

**Title** — Brand + year + subtitle from page positioning:

```html
<title>AIBIZCON 2026 | AI, Governance, Risk &amp; Compliance — Bay Area Tech Conference</title>
```

**Description** — One sentence on what/where/when; terms that appear on the page (NIST, Brentwood, free, etc.). Companion event only if hero lists it.

**Keywords** — Comma-separated terms **already used** in body, headings, or FAQ. Do not import external audit "opportunity" lists.

### Rejected pattern (content authority)

Audit suggested targeting without developer copy:

- CISO networking event
- Compliance workshop 2026
- Cybersecurity leadership conference
- NIST framework training

Use these in meta **only after** equivalent phrasing exists in approved body content.

## JSON-LD essentials

Single `<script type="application/ld+json">` with `@graph`. Use stable `@id` URLs on `https://www.aibizcon.me/#...`.

**Event** must include when advertising a dated event:

- `startDate` / `endDate` with timezone (`-07:00` for Pacific)
- `eventAttendanceMode`, `eventStatus`
- `location` → `Place` → `PostalAddress` (include `postalCode` when known)
- `organizer` → Organization `@id`
- `offers` with registration URL; `price: "0"` and `isAccessibleForFree: true` when free
- `performer` → `Person` array from speaker cards (`name`, `jobTitle` from visible roles)
- `image` — public URL of an image on the page (or dedicated asset)

**FAQPage** — One `Question` per visible FAQ item; `acceptedAnswer.text` must match (or closely paraphrase) the on-page answer.

When developer updates FAQ, speakers, dates, or venue: update JSON-LD in the same pass.

## Internal linking pattern

Add short navigation phrases in existing `section-body` paragraphs — do not add new marketing paragraphs.

Examples used on this site:

- Hero → `#about`, `#register`
- About → `#agenda`, `#speakers`, `#register`
- Agenda → `#speakers`, `#location`, `#register`
- FAQ intro → `aibizcon.com`, `#location`

Style (in site CSS):

```css
.section-body a,
.hero-desc a {
  color: var(--cyan);
  text-decoration: none;
}
.section-body a:hover,
.hero-desc a:hover {
  text-decoration: underline;
}
```

## robots.txt template

```text
User-agent: *
Allow: /
Disallow: /docs/
Disallow: /.cursor/

Sitemap: https://www.aibizcon.me/sitemap.xml
```

## sitemap.xml scope

List only crawlable public pages:

- `https://www.aibizcon.me/` (priority 1.0)
- `https://www.aibizcon.me/llms.txt` (priority 0.5)

Do not add `/docs/`, `/.cursor/`, or maintainer paths.

## llms.txt rules

- Summarize event, dates, registration, contact
- Link to homepage, Eventbrite, aibizcon.com
- Optional: robots.txt and sitemap.xml
- **Never** link to `docs/` or `README.md`

## Post-change documentation

Minimum: append `docs/update-history.docs.md` with:

- What SEO changed and why
- Developer vs local (SEO layer vs body copy)
- Audit items applied vs rejected
- Deferred (favicon, og:image)

Also update `docs/deploy.docs.md` when crawl files or structured-data inventory changes.

## Validation (after deploy)

1. [Google Rich Results Test](https://search.google.com/test/rich-results) — Event + FAQ
2. [Google Search Console](https://search.google.com/search-console) — submit `sitemap.xml`
3. Manual: view-source for canonical, JSON-LD parse errors, broken `#` anchors
4. Confirm `/favicon.ico` — if no asset, expect 404 until added (document deferral)

## SEO + developer merge

When integrating external `index.html` deliveries:

| Preserve from production | Take from developer |
|--------------------------|---------------------|
| Full `<head>` SEO + JSON-LD (refresh facts from new body) | Body sections and copy |
| Skip link, `<main>`, nav aria | Hero tag lines, agenda, speakers, etc. |
| robots.txt, sitemap.xml, llms.txt (sync dates/URLs) | Images and section content |

After merge: re-read body → align meta and JSON-LD → do not inject audit-only keywords.
