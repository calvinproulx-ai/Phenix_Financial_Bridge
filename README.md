# Phenix 1929 Holdings — Driver Dashboard

Single-file, self-contained HTML dashboard, sourced from the final Phenix1929_Consolidated P&L workbook. All data is embedded directly in `index.html` as a JSON blob — no build step, no external requests, no CDN dependencies. Renders entirely with vanilla JS/SVG, with a left-hand sidebar for navigating between three pages.

## View it locally

Just double-click `index.html`, or open it in any browser.

## Publish as a live site (GitHub Pages)

1. Create a new repository on GitHub (public or private both work; private repos need GitHub Pro for Pages).
2. Upload `index.html` to the root of the repo (drag-and-drop on the GitHub web UI works fine, or via git):
   ```
   git init
   git add index.html
   git commit -m "Phenix driver dashboard"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
3. In the repo, go to **Settings → Pages**.
4. Under "Build and deployment," set **Source** to "Deploy from a branch," pick branch `main` and folder `/ (root)`, then Save.
5. GitHub will publish it at `https://<your-username>.github.io/<your-repo>/` within a minute or two.

Any time you want to refresh the numbers, regenerate `index.html` and push again — GitHub Pages redeploys automatically on push.

## What's in the file

Three pages, selectable from the left sidebar, all "Adjusted" results:

- **EBITDA → Cash Flow**: Adjusted EBITDA → Unadjusted EBITDA → Free Cash Flow walk, including the balance-sheet-driven cash bridge (capex split into maintenance/other vs. acquisitions) and a cumulative cash-balance trend. Filterable by Entity (PCS / PSSF / GP / All companies) and, for PCS, by individual operating Company.
- **Actual → Proforma**: forward- and backward-looking EBITDA bridges across all 6 comparison modes from the workbook's Bridge Deep-Dive tab (FY Budget→Forecast, LTM YoY, LTM P3→P5, Vintage Budget→Forecast, YTD Actual→FY Forecast, LTM P5→P12). Filterable by Entity, vintage Cohort, and — in Vintage mode — individual Cost Center.
- **Budget → Actual**: Jan–May 2026 actual-vs-budget EBITDA bridge with a full category-by-cohort breakdown table.

All charts/tables/filters recompute client-side from the embedded data — no server needed.

## Data notes / known divergences from the source workbook

- **All-companies cash walk** (EBITDA → Cash Flow page): the workbook's own "All companies" cash formulas don't net every line (e.g. intercompany funding), so this figure is built by summing PCS's and PSSF's independently-validated cash walks line-by-line instead.
- **Corp/Other cohort** (Budget → Actual page): the source tab's own Corp/Other column always computes to 0 across every named cost category because of a redundant filter condition in its formula, and dumps the true amount into a single catch-all bucket instead. This dashboard shows the true per-category split where derivable, with the remainder in an "Other / unclassified" row, so every column always reconciles exactly to that cohort's actual EBITDA change.
