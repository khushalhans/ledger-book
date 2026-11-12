# Ledger Book — Web App

A single self-contained web page (`index.html`) that records your customers and
the products you quote them — **product name, description and quoted price** —
and saves everything **on the device itself** using the browser's `localStorage`.
No server, no account, no build step.

It is the same app as the iOS version, rewritten as one HTML file so it runs in
Safari on an iPhone (or any modern browser).

## Open it

- **On a computer:** double-click `index.html`.
- **On an iPhone:** the file must be opened from a web address (see below), then
  added to the Home Screen. Opening the file straight from the Files app is not
  reliable for saving data on iOS — use one of the hosting options.

### Getting it onto an iPhone (recommended)

Safari keeps `localStorage` per web address, so the reliable way is to host this
one file somewhere and open it as a web page.

**GitHub Pages — see [PUBLISH.md](PUBLISH.md)** for full step-by-step
instructions (no software to install). In short:

1. Create a **public** repository named `ledgerbook` on GitHub.
2. Upload `index.html` to the repository root and commit.
3. **Settings ▸ Pages ▸ Deploy from a branch ▸ `main` ▸ `/ (root)`**.
4. Your app is at `https://<your-username>.github.io/ledgerbook/`.
5. Open that in **Safari** on the iPhone → **Share ▸ Add to Home Screen**.

Open it from that icon from then on. It works offline and your records stay on
the phone.

**Any other static host works the same way** — Netlify Drop
(<https://app.netlify.com/drop>), Cloudflare Pages, a company web server, and so
on. Only the one file matters.

## What it stores

Each product quoted to a customer:

- **Product name**
- **Description**
- **Quoted price**

No quantities, no totals, no calculations. Everything can be edited later.

There is also a **Product Catalogue** (with photos) that you can reuse to fill in
the product form.

## The screens

**Dashboard → State → Customer → their products.**

- **Dashboard** — Total Customers, States, Products Supplied; customers grouped
  by state; the products you quote most; and **Backup & Restore**.
- **Customers (a state)** — the customers in that state. Toolbar: ▦ catalogue,
  ＋ add customer.
- **Customer page** — a ruled ledger page, one line per quoted product, oldest
  first. **Add Product** at the bottom. Tap a line to edit it.
- **Product Catalogue** — a photo grid. Reached from the ▦ button on the
  Customers screen.

## Backup & Restore (important)

Your data lives in this browser's `localStorage`. iOS Safari can clear a
website's storage if it is not used for a long time, so **keep a backup**:

- Dashboard ▸ **Backup & Restore** ▸ **Export backup file** — downloads a
  `.json` file (save it to iCloud Drive / Files / email).
- **Restore from a backup file** — pick that `.json` to put everything back.
- **Erase all data** — clears the device.

Adding the app to the Home Screen makes iOS treat it more like an installed app
and keeps storage around, but a periodic export is still the safe habit.

## Good to know

- **Fully offline.** No internet needed after the page loads; no data leaves the
  device.
- **Currency is INR (₹).**
- Photos are shrunk to a JPEG (max 900 px) before being saved, so they do not
  fill up storage too quickly.
- If saving ever fails (storage full), the app tells you.

## Files

```
LedgerBookWeb/
├─ index.html     the whole app — HTML, CSS and JavaScript in one file
├─ PUBLISH.md     step-by-step GitHub Pages instructions
├─ README.md      this file
├─ .nojekyll      tells GitHub Pages to serve the files as-is (optional)
└─ .gitignore     ignores OS junk files
```

The site is ready to publish as-is: upload the files to a repository root and
turn on GitHub Pages — see [PUBLISH.md](PUBLISH.md).

## Notes

- The older native SwiftUI project is in the sibling `LedgerBook/` folder. It is
  kept for reference; this web app is the one to use on the iPhone.
