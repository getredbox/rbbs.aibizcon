# Deployment

This site is a static single-page app (`index.html` at the repo root, no build step). We host it on **GitHub Pages** and use **Cloudflare** for DNS, TLS, and caching in front of the custom domain **`www.aibizcon.me`**.

## Architecture

```
Visitor → Cloudflare (DNS, CDN, SSL) → GitHub Pages → index.html
```

GitHub Pages serves the files from the repository. Cloudflare terminates HTTPS for your domain and proxies traffic to GitHub’s Pages origin.

---

## Prerequisites

- A GitHub account and a repository for this project (e.g. `rbbs.aibizcon`)
- The **`aibizcon.me`** zone in Cloudflare
- `index.html` at the **root** of the default branch (already true in this repo)

---

## 1. Publish on GitHub Pages

1. Push the repo to GitHub (default branch: `main` or `master`).
2. Open the repo → **Settings** → **Pages**.
3. Under **Build and deployment** → **Source**, choose **Deploy from a branch**.
4. Set **Branch** to `main` (or your default branch) and **Folder** to `/ (root)`.
5. Save. After a minute or two, the site is available at:
   - `https://<username>.github.io/<repo-name>/` (project site), or
   - `https://<username>.github.io/` (user/org site if the repo is named `<username>.github.io`)

No build command or GitHub Action is required for this project.

---

## 2. Add a custom domain in GitHub

1. Still under **Settings** → **Pages**, enter **`www.aibizcon.me`** in **Custom domain**.
2. Enable **Enforce HTTPS** once DNS has propagated and GitHub shows a valid certificate.

The repo includes a root **`CNAME`** file set to `www.aibizcon.me` so GitHub Pages serves the custom domain. A subdomain `CNAME` in Cloudflare is all that’s required (below).

---

## 3. Configure Cloudflare DNS

In the Cloudflare dashboard for the **`aibizcon.me`** zone:

| Type  | Name  | Target                    | Proxy        |
|-------|-------|---------------------------|--------------|
| CNAME | `www` | `<username>.github.io`    | Proxied (orange cloud) |

This creates **`www.aibizcon.me`** → GitHub Pages.

**Optional — apex redirect:** To send `aibizcon.me` to `www`, add a redirect rule in Cloudflare (Redirect Rules: `aibizcon.me/*` → `https://www.aibizcon.me/$1`).

- Use your GitHub **username or org name**, not the repo name, in the CNAME target (unless GitHub’s Pages UI shows a different target for your setup).
- Keep the record **proxied** so Cloudflare provides SSL and caching.

**SSL/TLS** (Cloudflare → **SSL/TLS**):

- Set encryption mode to **Full** (or **Full (strict)** once GitHub’s certificate is active).
- Avoid **Flexible** only pointing at GitHub Pages; it can cause redirect loops with “Enforce HTTPS” on GitHub.

**Optional:** Page Rules or Cache Rules to cache static HTML; default settings are usually fine for a small landing page.

---

## 4. Verify

1. Open the GitHub Pages URL and confirm `index.html` loads.
2. Open [https://www.aibizcon.me](https://www.aibizcon.me) and confirm the same content.
3. Check **Settings** → **Pages** in GitHub for “DNS check successful” and a valid certificate.
4. Spot-check fonts (Google Fonts CDN) and outbound links (e.g. ccbizcon.com) over HTTPS.

DNS can take up to 24–48 hours to propagate globally; often it is much faster.

---

## 5. Ship updates

1. Edit `index.html` locally.
2. Commit and push to the branch GitHub Pages uses (usually `main`).
3. GitHub redeploys automatically; Cloudflare may serve a cached copy briefly—purge cache in Cloudflare if you need an immediate refresh.

---

## Troubleshooting

| Symptom | What to check |
|---------|----------------|
| 404 on GitHub URL | Pages source is `/ (root)` and `index.html` is on that branch |
| 404 on custom domain | CNAME `www` → `<username>.github.io` in `aibizcon.me`; custom domain `www.aibizcon.me` set in GitHub Pages |
| Certificate / HTTPS errors | Cloudflare SSL mode is **Full**; wait for GitHub to issue cert; DNS propagated |
| Wrong path / broken assets | Project site URLs include `/repo-name/`; use a custom domain or set a `<base href>` if you must use the project URL |
| Stale content after deploy | Purge Cloudflare cache for the hostname |

---

## 6. SEO and LLM discoverability after launch

The site ships with:

- Meta description, canonical URL, and Open Graph / Twitter tags in `index.html`
- JSON-LD structured data (`Event`, `Organization`, `WebSite`, `FAQPage`)
- `robots.txt` and `sitemap.xml` at the repo root (`/docs/` and `/.cursor/` disallowed for crawlers)
- `llms.txt` at the repo root — a curated, LLM-readable overview per the [llms.txt specification](https://llmstxt.org/)

### Search engines

After deploy, submit the sitemap in [Google Search Console](https://search.google.com/search-console):

1. Add property: `https://www.aibizcon.me`
2. Verify ownership (DNS TXT record in Cloudflare is easiest)
3. Submit sitemap URL: `https://www.aibizcon.me/sitemap.xml`

The sitemap lists the homepage and `llms.txt` only. Internal paths under `docs/` and `.cursor/` are blocked in `robots.txt` and excluded from the sitemap.

Optional: add an `og:image` (1200×630) hosted at a public URL for richer social previews.

### LLMs and agents

`llms.txt` lives at **`https://www.aibizcon.me/llms.txt`** after deploy. It summarizes the public site and points to registration and contact details for LLM inference-time use — not for search indexing. Do **not** link to `docs/` or `README.md` in `llms.txt`; those are maintainer-only (`docs/` is blocked in `robots.txt`).

When updating the site, keep `llms.txt` in sync with event dates and public URLs. Maintainer docs under `docs/` are updated separately (see `docs/update-history.docs.md`).

---

## Alternative: Cloudflare Pages only

If you prefer not to use GitHub Pages, you can connect the same repo to **Cloudflare Pages** (build command: none; output directory: `/`). That replaces GitHub as the host while keeping DNS in Cloudflare. The steps above assume **GitHub Pages + Cloudflare DNS**, which is the default for this project.
