# Wood, Water & Waves — one-page site

A self-contained static website. No build step, no framework install — just
static files you upload as-is.

## What's in this folder

```
index.html        The page itself
support.js        Runtime that renders index.html (must stay next to it)
image-slot.js     Photo component used by the page
uploads/          All photos, the press PDFs, and article thumbnails
README.md         This file
```

Keep the files together exactly as they are — `index.html` loads
`support.js`, `image-slot.js`, and everything in `uploads/` by relative
path, so the folder structure must be preserved.

> It must be served over **http/https** (a web server or GitHub Pages).
> Opening `index.html` directly from your hard drive with `file://` will
> not load the scripts. GitHub Pages serves it correctly.

---

## Publish with GitHub Pages

### Option A — GitHub website (no command line)

1. Sign in at <https://github.com> and click **New** to create a repository.
   Name it e.g. `wood-water-waves`. Leave it **Public**. Click
   **Create repository**.
2. On the new repo page, click **uploading an existing file**
   (under "Quick setup").
3. Drag **the contents of this folder** — `index.html`, `support.js`,
   `image-slot.js`, and the whole `uploads` folder — into the upload area.
   (Drag the files/folder themselves, not the outer folder, so `index.html`
   lands at the top level of the repo.)
4. Click **Commit changes**.
5. Go to **Settings → Pages** (left sidebar).
6. Under **Build and deployment → Source**, choose **Deploy from a branch**.
   Set **Branch** to `main` and folder to `/ (root)`. Click **Save**.
7. Wait ~1 minute, then refresh. Your site is live at:
   `https://<your-username>.github.io/<repository-name>/`

### Option B — command line (git)

```bash
cd path/to/this/folder
git init
git add .
git commit -m "Wood, Water & Waves site"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

Then do steps 5–7 above to turn on GitHub Pages.

---

## Custom domain (optional)

In **Settings → Pages → Custom domain**, enter your domain (e.g.
`woodwaterwaves.com`) and follow GitHub's DNS instructions. Add a file named
`CNAME` containing just your domain if you want it committed to the repo.

## Notes

- **Photos** are the real image files in `uploads/`. To swap one, replace the
  file in `uploads/` with a new image of the same name (or edit the `src` in
  `index.html`).
- **Press PDFs** open in a new tab; they live in `uploads/` and are linked
  from the four cards.
- **The film** is embedded from YouTube and needs an internet connection to
  play (as with any YouTube embed).
- Everything else is fully self-contained and works offline once served.
