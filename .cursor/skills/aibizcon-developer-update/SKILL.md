---
name: aibizcon-developer-update
description: Integrates web developer changes to the AIBIZCON static site, syncs docs/ and llms.txt with index.html changes, documents in update-history, repairs hero layout, and preserves SEO/accessibility. Use when the user mentions a developer update, GitHub push or PR, index.html edits, hero fixes, SEO, or www.aibizcon.me site updates.
---

# AIBIZCON developer update integration

## Project context

- **Production file:** `index.html` at repo root — single-page static site (HTML/CSS/JS, no build step).
- **Domain:** `www.aibizcon.me` (GitHub Pages + Cloudflare; see `docs/deploy.docs.md`).
- **Events:** **AIBIZCON** (Sept 17, 2026, 1PM–5PM) primary; **CCBIZCON** (Sept 18, 2026) in hero only unless developer expands it.
- **Registration:** `https://ccbizcon2026.eventbrite.com`
- **Scratch workspace:** `temp/` (gitignored) — all temporary files and scripts

The web developer pushes updates **directly to this GitHub repo** (branch or PR).

Read `docs/update-history.docs.md` before integrating a new delivery.

## Integration principle

**Do not rewrite developer body content.** When merging a developer delivery, change only what the site owner expects locally:

1. **Hero layout** — centered stack; graphic under subtitle (see [reference.md](reference.md))
2. **SEO / accessibility** — follow [aibizcon-seo](../aibizcon-seo/SKILL.md): `<head>` meta, OG, Twitter, JSON-LD; skip link; `<main id="main-content">`
3. **Year fixes** — align location/footer dates with hero when developer left 2025 behind

Keep nav, agenda, speakers, sponsors, FAQ, register, and hero copy as delivered unless the user asks otherwise.

## temp/ rules (mandatory)

**Every** temporary artifact belongs in `temp/` — never at repo root, never under `.cursor/`.

`temp/` is in `.gitignore` — nothing inside it is committed.

## Workflow

```
Task progress:
- [ ] Identify the change (git log, git diff, or file in temp/)
- [ ] Run comparison; save scripts/output under temp/
- [ ] Integrate into index.html (developer body + hero/SEO/a11y/year fixes)
- [ ] Repair hero layout if regressed
- [ ] Update docs/ and related files (see below) — same commit as index.html
- [ ] Append entry to docs/update-history.docs.md
- [ ] Confirm no scratch files left outside temp/
```

### Compare

```bash
git diff <baseline>..<commit> -- index.html
python temp/compare_update.py temp/index.YYYYMMDD-update.html [baseline-commit]
```

## Docs must stay in sync

**Any change to `index.html` (or SEO/deploy files) requires updating the relevant docs in the same work session.** Do not ship HTML without documenting it.

| File | Update when |
|------|-------------|
| `docs/update-history.docs.md` | **Always** — dated entry for every integration or local fix |
| `docs/homepage.docs.md` | Sections, event details, structure, or design notes change |
| `docs/deploy.docs.md` | SEO, robots.txt, sitemap.xml, llms.txt, or deploy steps change |
| `llms.txt` | Event dates, branding, or public URLs — do not link to `docs/` or `README.md` |
| `README.md` | Repo layout or run/deploy pointers change |

`docs/` is blocked from crawlers (`robots.txt`) but is the **source of truth** for maintainers. `update-history.docs.md` is the changelog; the other docs reflect current state.

### update-history entry (required)

Append to `docs/update-history.docs.md` every time:

- Timestamp and source (commit, PR, or `temp/` file)
- What came from the **developer** vs what was **fixed locally** (hero, SEO, year)
- Which **docs files** were updated in the same pass
- Follow-up items

Template: [reference.md](reference.md#update-history-entry-template)

## Integrating into index.html

**Take from developer:** body content — nav, hero copy, sections, speakers, sponsors, FAQ, location, footer.

**Keep from production:**

- SEO `<head>` (AIBIZCON-first; see reference.md)
- Accessibility markup
- Canonical hero CSS and HTML order

After integration: `npx serve .` and verify no hero gap.

## Do not

- Create temporary files outside `temp/`
- Change developer body copy beyond hero layout, SEO, a11y, and agreed year fixes
- Commit `index.html` changes without updating `docs/update-history.docs.md`
- Drop production SEO or accessibility markup
- Use blanket `.hero > * { position: relative }`

## Additional resources

- Hero layout, docs sync detail, merge checklist: [reference.md](reference.md)
- SEO rules, schema, crawl files, audit handling: [aibizcon-seo](../aibizcon-seo/SKILL.md)
