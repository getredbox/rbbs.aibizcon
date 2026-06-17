---
name: aibizcon-seo
description: Builds and maintains SEO for the AIBIZCON static site while content is created or integrated — meta tags, JSON-LD, crawl files, internal links, and accessibility. Use when adding or editing index.html, running SEO audits, updating robots.txt/sitemap.xml/llms.txt, or when third-party content must not be rewritten for keyword stuffing.
---

# AIBIZCON SEO while building content

SEO is part of every content change, not a post-launch patch. Apply this skill whenever `index.html` or public discoverability files change.

**Related:** Developer deliveries use [aibizcon-developer-update](../aibizcon-developer-update/SKILL.md) for merge workflow; this skill owns SEO rules and checklists.

## Core rules

1. **Describe, don't invent** — `<title>`, meta description, and keywords must reflect **on-page copy** (developer or approved text). Never add audit-suggested keyword phrases that are not in the body (e.g. "CISO networking event", "compliance workshop 2026") unless the developer adds them first.
2. **AIBIZCON is primary** — Title, description, OG/Twitter, and JSON-LD `Event` lead with AIBIZCON. CCBIZCON may appear in hero or as a companion line in meta only when the page says so.
3. **Layer, don't rewrite** — Keep developer body copy intact. SEO lives in `<head>`, JSON-LD, nav/footer links, and minimal in-section anchor links (navigation only).
4. **Schema mirrors the page** — JSON-LD facts (dates, venue, FAQ answers, speakers) must match visible HTML. Update schema when sections change.
5. **Ship docs with HTML** — Append `docs/update-history.docs.md`; update `docs/deploy.docs.md`, `llms.txt`, or `docs/homepage.docs.md` when relevant.

## Workflow (every content change)

```
Task progress:
- [ ] Read visible content (what changed?)
- [ ] Update <head> meta to match (title, description, canonical, OG, Twitter)
- [ ] Update JSON-LD @graph if facts/sections changed
- [ ] Verify heading hierarchy (one H1, logical H2/H3)
- [ ] Verify images have descriptive alt text
- [ ] Add or refresh contextual internal links between sections
- [ ] Sync robots.txt / sitemap.xml / llms.txt if URLs or crawl rules changed
- [ ] Document in docs/update-history.docs.md
- [ ] Note deferred items (favicon, og:image) — do not fake assets
```

## What to implement in index.html

| Layer | Required |
|-------|----------|
| **Meta** | `title`, `description`, `keywords` (from page terms only), `canonical`, `robots`, geo tags for local event |
| **Social** | Open Graph + Twitter Card (`og:title`, `og:description`, `og:url`, `twitter:card`) |
| **Structured data** | JSON-LD `@graph`: `WebSite`, `Organization`, `Event`, `FAQPage` when FAQ exists; `Person` performers when speakers listed |
| **Accessibility** | `lang="en"`, skip link, `<main id="main-content">`, nav `aria-label`, semantic sections with `id` anchors |
| **Internal links** | Nav + footer + short contextual links in section intros (e.g. about → agenda, register → location) |
| **Images** | Meaningful `alt` on every `<img>` |

## Crawl and LLM files (repo root)

| File | Purpose |
|------|---------|
| `robots.txt` | Allow `/`; disallow `/docs/`, `/.cursor/`; sitemap URL |
| `sitemap.xml` | Public URLs only (homepage + `llms.txt`) |
| `llms.txt` | LLM-readable summary; public registration/contact links only — **never** link to `docs/` or `README.md` |

Domain: `https://www.aibizcon.me/`

## Audit recommendations — how to apply

| Audit item | Apply when | Skip or defer when |
|------------|------------|-------------------|
| Event / FAQ schema | FAQ and event details on page | — |
| Internal links | Improves navigation; no new marketing copy | — |
| Title / keyword tweaks | Wording already in body or brand name | Phrases only in audit, not on page |
| Social links in footer | Real URLs exist (Eventbrite, aibizcon.com) | Placeholder LinkedIn/Twitter |
| `favicon.ico` | Asset provided | No icon file yet |
| `og:image` | 1200×630 image hosted at stable URL | No image asset yet |

When rejecting audit keywords, note it in `docs/update-history.docs.md`.

## Do not

- Stuff meta keywords or titles with positioning the content author did not write
- Change developer section copy to chase rankings
- List maintainer paths in `llms.txt` or `sitemap.xml`
- Remove production SEO/a11y markup during developer merges
- Add `favicon` or `og:image` links without real files

## Additional resources

- JSON-LD shape, meta templates, validation URLs: [reference.md](reference.md)
