# Deployment

Two free hosting options for this portfolio (no build step required — just `portfolio.html`).

---

## Option 1 — GitHub Pages (Recommended)

**Free, zero-config, served from your GitHub repo. Custom domain support included.**

### Steps

1. Push this repository to GitHub (create a repo at github.com/new if you haven't):

   ```powershell
   git remote add origin https://github.com/bbalouki/bbalouki.github.io.git
   git push -u origin main
   ```

2. Rename `portfolio.html` to `index.html` (GitHub Pages serves `index.html` as the root):

   ```powershell
   git mv portfolio.html index.html
   git commit -m "rename portfolio.html to index.html for GitHub Pages"
   git push
   ```

3. In your GitHub repo go to **Settings → Pages → Source** and select `main` branch, `/ (root)`.

4. Your site will be live at `https://bbalouki.github.io` within ~60 seconds.

### Custom domain (optional)

Add a `CNAME` file at the repo root containing your domain (e.g. `bbs-trading.com`), then point your DNS `A` record to GitHub's IPs or add a `CNAME` DNS record to `bbalouki.github.io`.

---

## Option 2 — Netlify

**Free tier, instant deploys via drag-and-drop or Git. Automatic HTTPS, CDN, form handling.**

### Option A — Drag & Drop (fastest, no CLI needed)

1. Go to [app.netlify.com](https://app.netlify.com) and sign in (GitHub login works).
2. Drag the project folder (containing `portfolio.html`) onto the Netlify dashboard.
3. Netlify assigns a random URL like `https://random-name.netlify.app` immediately.
4. Rename the site under **Site settings → Site name** to get `https://bbalouki.netlify.app`.

### Option B — Git-connected deploy (auto-deploys on push)

1. Push this repo to GitHub (see Option 1, step 1).
2. In Netlify: **Add new site → Import an existing project → GitHub**.
3. Select the repo. Set:
   - **Base directory**: _(leave blank)_
   - **Build command**: _(leave blank)_
   - **Publish directory**: `.` (a single dot — the repo root)
4. Click **Deploy**. Every `git push` to `main` will trigger a new deploy automatically.

### Custom domain (optional)

In Netlify go to **Site settings → Domain management → Add a domain**. Netlify walks you through the DNS changes.

---

## Comparison

|                       | GitHub Pages          | Netlify              |
| --------------------- | --------------------- | -------------------- |
| Free tier             | Yes                   | Yes                  |
| Auto-deploy on push   | Yes (after setup)     | Yes                  |
| CDN                   | Yes                   | Yes (global edge)    |
| Custom domain + HTTPS | Yes                   | Yes                  |
| Drag-and-drop deploy  | No                    | Yes                  |
| Build minutes         | N/A                   | 300 min/month free   |
| Best for              | Simplest Git workflow | Fastest first deploy |
