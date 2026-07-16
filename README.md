# Phenix 1929 Holdings — EBITDA to FCF Bridge

Single-file, self-contained HTML dashboard. All source data (Adjusted TB / Unadjusted TB category breakdowns, PCS company-level splits, and PCS/PSSF balance-sheet cash walks) is embedded directly in `index.html` as a JSON blob — no build step, no external requests, no CDN dependencies. It renders entirely with vanilla JS/SVG.

## View it locally

Just double-click `index.html`, or open it in any browser.

## Publish as a live site (GitHub Pages)

1. Create a new repository on GitHub (public or private both work; private repos need GitHub Pro for Pages).
2. Upload `index.html` to the root of the repo (drag-and-drop on the GitHub web UI works fine, or via git):
   ```
   git init
   git add index.html
   git commit -m "Add EBITDA to FCF bridge dashboard"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
3. In the repo, go to **Settings → Pages**.
4. Under "Build and deployment," set **Source** to "Deploy from a branch," pick branch `main` and folder `/ (root)`, then Save.
5. GitHub will publish it at `https://<your-username>.github.io/<your-repo>/` within a minute or two.

Any time you want to refresh the numbers, regenerate `index.html` and push again — GitHub Pages redeploys automatically on push.

## What's in the file

- **Section 1 — Adjusted EBITDA → Unadjusted EBITDA**: live category/Co-tag breakdown from the Adjusted TB and Unadjusted TB, filterable by Entity (PCS / PSSF / GP / All companies) and, for PCS, by individual operating Company.
- **Section 2 — Unadjusted EBITDA → Free Cash Flow**: month-end balance-sheet-driven cash walk for PCS and PSSF only (not available for GP or when a single PCS company is selected, matching the source workbook's own logic).
- Entity pills, Company dropdown, and a Period selector (month or Jan–May '26 total) all recompute both charts client-side from the embedded data — no server needed.
