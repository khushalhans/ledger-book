# Publish Ledger Book to GitHub Pages

GitHub Pages gives this app a permanent `https://…` address, which is what the
iPhone needs in order to keep your records in `localStorage`. Once it is live,
open the address in Safari and **Add to Home Screen**.

There are two ways. **Option A needs no software installed** — use it if you are
not already a Git user.

> The repository must be **Public**. GitHub Pages is free only for public
> repositories. The *code* is public; your *data* never leaves your phone.

---

## Option A — Upload through the browser (no tools)

1. Sign in at <https://github.com> (create a free account if needed).
2. Create the repository: go to <https://github.com/new>
   - **Repository name:** `ledgerbook`
   - **Visibility:** **Public**
   - Leave *Add a README file*, *.gitignore* and *license* **unchecked** —
     we already have our own files.
   - Click **Create repository**.
3. On the new, empty repository page, click the
   **“uploading an existing file”** link.
4. Open this `LedgerBookWeb` folder on your computer and drag these files into
   the browser:
   - `index.html`  ← **the app; must be at the top level**
   - `README.md`
   - `PUBLISH.md`
   - `.nojekyll` *(optional; see the note below)*
   - `.gitignore` *(optional)*

   ⚠️ Upload the **files**, not the folder. After uploading, the repository's
   file list must show `index.html` on its own, not `LedgerBookWeb/index.html`.
5. Scroll down and click **Commit changes**.
6. Open **Settings ▸ Pages** (left sidebar).
   - Under **Build and deployment ▸ Source**, choose **Deploy from a branch**.
   - **Branch:** `main`  ·  **Folder:** `/ (root)`  → **Save**.
7. Wait about a minute, then refresh that page. GitHub shows
   **“Your site is live at …”**. The address is:

   ```
   https://<your-username>.github.io/ledgerbook/
   ```

8. On the iPhone, open that address in **Safari**, then
   **Share ▸ Add to Home Screen**. Launch it from the new icon from now on.

### Note about `.nojekyll`
`.nojekyll` is an empty file whose name starts with a dot, so it may be hidden
or refused by the uploader. It is **optional** for this app — GitHub runs Jekyll
by default, but a plain `index.html` is served correctly with or without it. If
it is a hassle, skip it.

---

## Option B — With Git (command line)

Install Git first (<https://git-scm.com/download/win>), then from inside this
`LedgerBookWeb` folder:

```bash
git init -b main
git add -A
git commit -m "Ledger Book web app"

# Create an empty PUBLIC repo named "ledgerbook" on GitHub first, then:
git remote add origin https://github.com/<your-username>/ledgerbook.git
git push -u origin main
```

Then enable Pages exactly as in **Option A, step 6** (Settings ▸ Pages ▸
Deploy from a branch ▸ `main` ▸ `/ (root)`).

### Optional: deploy with GitHub Actions instead
If you prefer Actions over branch deployment, add this file as
`.github/workflows/pages.yml`, then set **Settings ▸ Pages ▸ Source** to
**GitHub Actions**:

```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
  workflow_dispatch:
permissions:
  contents: read
  pages: write
  id-token: write
concurrency:
  group: pages
  cancel-in-progress: true
jobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: .
      - id: deployment
        uses: actions/deploy-pages@v4
```

---

## Updating the app later

Edit `index.html` on your computer, then:

- **Option A:** open the repository, click `index.html`, use the ✏️ pencil to
  edit, or use **Add file ▸ Upload files** to replace it, and commit.
- **Option B:** `git add -A && git commit -m "update" && git push`.

Pages redeploys within a minute. On the iPhone, just reopen the Home Screen icon
(the page reloads from the network when online).

## Custom domain (optional)

If you own a domain, add it under **Settings ▸ Pages ▸ Custom domain** and
follow GitHub's DNS instructions. A `CNAME` file is created automatically.

## Checklist

- [ ] Repository is **Public**
- [ ] `index.html` is at the repository **root**
- [ ] Pages source = **Deploy from a branch**, `main`, `/ (root)`
- [ ] Site opens at `https://<username>.github.io/ledgerbook/`
- [ ] Added to the iPhone Home Screen from **Safari**
- [ ] Made a first **backup** from Dashboard ▸ Backup & Restore
