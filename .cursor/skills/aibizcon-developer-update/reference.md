# AIBIZCON developer update — reference

## Repository layout

```text
rbbs.aibizcon/
├── index.html
├── llms.txt                # LLM site summary — keep in sync with live content
├── robots.txt
├── sitemap.xml
├── CNAME
├── images/
├── temp/                   # gitignored scratch workspace
└── docs/
    ├── deploy.docs.md      # hosting, SEO, robots, sitemap, llms.txt
    ├── homepage.docs.md    # index.html structure and event details
    └── update-history.docs.md  # changelog — append every HTML change
```

## Docs sync checklist

Run after every `index.html` change:

| Doc | Action |
|-----|--------|
| `docs/update-history.docs.md` | Append dated entry (developer vs local fixes; list docs touched) |
| `docs/homepage.docs.md` | Refresh event table, section list, line counts if page structure changed |
| `docs/deploy.docs.md` | Update if SEO tags, robots/sitemap rules, or deploy steps changed |
| `llms.txt` | Refresh summary, dates, public URLs — **never** link to `docs/` or `README.md` |
| `README.md` | Update project tree or pointers if files added/renamed |

If unsure whether a doc needs updating, update `update-history.docs.md` at minimum and note “no other docs changed” with reason.

## GitHub workflow

1. Developer edits `index.html` (and `images/`) on a branch → PR.
2. Reviewer compares diff, fixes hero/SEO if needed, **updates docs in the same PR**.
3. Merge to default branch → GitHub Pages deploys.

**Developer should edit:** `index.html`, `images/`.

**Developer should not edit without coordination:** `CNAME`, `robots.txt`, `sitemap.xml`, `docs/`, `llms.txt`, `.gitignore`.

### Reviewing a PR

```bash
gh pr checkout <number>
git diff main -- index.html docs/ llms.txt README.md
python temp/compare_update.py index.html <baseline-commit>
npx serve .
```

## temp/ — what goes here

| Artifact | Example |
|----------|---------|
| Compare scripts | `temp/compare_update.py` |
| Baseline snapshots | `temp/_old_index.html` |
| Developer HTML copies | `temp/index.YYYYMMDD-update.html` |

## Canonical hero layout

**HTML order** inside `.hero-main` > `.hero-copy`:

1. `.hero-tag` line(s)
2. `.hero-title`
3. `.hero-subtitle`
4. `.hero-ai-graphic` — SVG **under** subtitle
5. Hero description + CTAs
6. `.hero-event-bar`

**CSS essentials:**

```css
.hero { justify-content: flex-start; overflow: hidden; }
.hero-main { display: flex; flex-direction: column; align-items: center; text-align: center; }
.hero-ai-graphic { height: 180px; overflow: hidden; }
.hero-ai-graphic svg { height: 180px; overflow: hidden; }
```

Only `.hero-main` and `.hero-event-bar` need `position: relative; z-index: 1`.

## Hero gap — root cause

SVG glow filters with `overflow: visible`, SVG before text, or `.hero > * { position: relative }` inflate layout and create a large empty gap at the top.

## SEO rules

See [aibizcon-seo](../aibizcon-seo/SKILL.md) for full workflow. Summary:

- **AIBIZCON is primary** in title, meta description, OG, Twitter, and JSON-LD `Event`.
- **Describe, don't invent** — meta keywords/title must match on-page copy; reject audit-only keyword targets.
- CCBIZCON may appear in hero body copy; mention as companion in meta description only if needed.
- Fix year to **2026** in SEO and in location/footer when developer left 2025.

## Merge checklist

| Keep from production | Take from developer |
|---------------------|---------------------|
| SEO meta, OG, Twitter, JSON-LD (AIBIZCON-first) | Body sections and copy |
| Skip link + `<main id="main-content">` | Hero tag lines (including CCBIZCON line) |
| Hero CSS + element order | Speaker/sponsor content |
| `robots.txt` / `sitemap.xml` unless updating SEO | |

## Update-history entry template

```markdown
## YYYY-MM-DD HH:MM:SS — [Developer update | Local fix] (commit `<hash>` or PR #N)

**Source:** git commit / PR / `temp/index.YYYYMMDD-update.html`
**Compared to:** commit `<baseline-hash>`
**Integrated into:** `index.html` (+ docs listed below)

### From developer delivery
- ...

### Fixed locally (hero / SEO / a11y / year)
- ...

### Docs updated
- `docs/update-history.docs.md` — this entry
- `docs/homepage.docs.md` — ...
- `docs/deploy.docs.md` — ...
- `llms.txt` — ...
- (or: no other docs required — reason)

### Follow-up items
- ...
```
