# rbbs.aibizcon

Static marketing site for AIBIZCON/CCBIZCON, built as a single HTML page with no build step.

## What this repo contains

- `index.html` - the complete landing page (HTML, CSS, and JavaScript in one file)
- `llms.txt` - LLM-friendly site summary and doc links ([llms.txt spec](https://llmstxt.org/))
- `robots.txt` and `sitemap.xml` - search engine crawlers
- `docs/homepage.docs.md` - structure and implementation notes for the homepage
- `docs/deploy.docs.md` - deployment guide for GitHub Pages + Cloudflare
- `docs/update-history.docs.md` - changelog of web developer deliveries
- `CNAME` - GitHub Pages custom domain (`www.aibizcon.me`)

## Tech stack

- Plain HTML/CSS/JavaScript
- Google Fonts loaded via CDN
- No framework, bundler, or package dependencies required

## Run locally

You can open `index.html` directly in a browser, or use a local static server.

### Option 1: Open directly

Double-click `index.html`.

### Option 2: Serve locally (recommended)

```bash
npx serve .
```

Then open the local URL shown in your terminal.

## Deployment

Production hosting is documented for:

- GitHub Pages (origin hosting)
- Cloudflare (DNS, SSL, and caching)

See `docs/deploy.docs.md` for the full step-by-step guide and domain setup for `www.aibizcon.me`.

## Project structure

```text
rbbs.aibizcon/
├── CNAME
├── index.html
├── llms.txt
├── README.md
├── robots.txt
├── sitemap.xml
└── docs/
    ├── deploy.docs.md
    ├── homepage.docs.md
    └── update-history.docs.md
```
