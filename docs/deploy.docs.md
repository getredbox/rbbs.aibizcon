# Deployment

This site is a static single-page app (`index.html` at the repo root, no build step). We host it on **GitHub Pages** and use **Cloudflare** for DNS, TLS, and caching in front of the custom domain **`aibizcon.getredbox.com`**.

## Architecture

```
Visitor → Cloudflare (DNS, CDN, SSL) → GitHub Pages → index.html
```

GitHub Pages serves the files from the repository. Cloudflare terminates HTTPS for your domain and proxies traffic to GitHub’s Pages origin.

---

## Prerequisites

- A GitHub account and a repository for this project (e.g. `rbbs.aibizcon`)
- The `getredbox.com` zone in Cloudflare (subdomain: **`aibizcon.getredbox.com`**)
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

1. Still under **Settings** → **Pages**, enter **`aibizcon.getredbox.com`** in **Custom domain**.
2. Enable **Enforce HTTPS** once DNS has propagated and GitHub shows a valid certificate.

GitHub may prompt you to add a `CNAME` file to the repo; you can accept that or add the record only in Cloudflare (below). A subdomain `CNAME` is all that’s required for `aibizcon.getredbox.com`.

---

## 3. Configure Cloudflare DNS

In the Cloudflare dashboard for the **`getredbox.com`** zone:

| Type  | Name       | Target                    | Proxy        |
|-------|------------|---------------------------|--------------|
| CNAME | `aibizcon` | `<username>.github.io`    | Proxied (orange cloud) |

This creates **`aibizcon.getredbox.com`** → GitHub Pages.

- Use your GitHub **username or org name**, not the repo name, in the CNAME target (unless GitHub’s Pages UI shows a different target for your setup).
- Keep the record **proxied** so Cloudflare provides SSL and caching.

**SSL/TLS** (Cloudflare → **SSL/TLS**):

- Set encryption mode to **Full** (or **Full (strict)** once GitHub’s certificate is active).
- Avoid **Flexible** only pointing at GitHub Pages; it can cause redirect loops with “Enforce HTTPS” on GitHub.

**Optional:** Page Rules or Cache Rules to cache static HTML; default settings are usually fine for a small landing page.

---

## 4. Verify

1. Open the GitHub Pages URL and confirm `index.html` loads.
2. Open [https://aibizcon.getredbox.com](https://aibizcon.getredbox.com) and confirm the same content.
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
| 404 on custom domain | CNAME `aibizcon` → `<username>.github.io` in `getredbox.com`; custom domain `aibizcon.getredbox.com` set in GitHub Pages |
| Certificate / HTTPS errors | Cloudflare SSL mode is **Full**; wait for GitHub to issue cert; DNS propagated |
| Wrong path / broken assets | Project site URLs include `/repo-name/`; use a custom domain or set a `<base href>` if you must use the project URL |
| Stale content after deploy | Purge Cloudflare cache for the hostname |

---

## Alternative: Cloudflare Pages only

If you prefer not to use GitHub Pages, you can connect the same repo to **Cloudflare Pages** (build command: none; output directory: `/`). That replaces GitHub as the host while keeping DNS in Cloudflare. The steps above assume **GitHub Pages + Cloudflare DNS**, which is the default for this project.
