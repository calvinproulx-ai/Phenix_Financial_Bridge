# Phenix 1929 Holdings — Monthly Board Package

Single-file, self-contained HTML dashboard, sourced from the final Phenix1929_Consolidated P&L workbook. All data is embedded directly in `index.html` as a JSON blob — no build step, no external requests, no CDN dependencies. Renders entirely with vanilla JS/SVG, with a left-hand sidebar for navigating between pages and a "Print / Save PDF" button in the masthead for assembling a board-ready PDF.

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

Four pages, selectable from the left sidebar, all "Adjusted" results unless noted:

- **EBITDA → Cash Flow**: Adjusted EBITDA → Unadjusted EBITDA → Free Cash Flow walk, including the balance-sheet-driven cash bridge (capex split into maintenance/other vs. acquisitions) and a cumulative cash-balance trend. Filterable by Entity (PCS / PSSF / GP / All companies) and, for PCS, by individual operating Company.
- **Actual v. Prior Year**: LTM / PTD / YTD sub-tabs comparing current-year Adjusted EBITDA to the same period last year.
- **Actual → Forecast**: YTD / LTM sub-tabs bridging where the business stands today to the full-year 2026 outlook.
- **Actual v. Budget**: PTD / YTD / LTM sub-tabs comparing Adjusted EBITDA to the approved plan. The YTD view also includes a full category-by-cohort breakdown table.

All three comparison pages are sourced live (by cost category, Entity, and vintage Cohort) from the workbook's **Bridge Deep-Dive** tab, replicating its 8 built-in comparison templates. Each page's Entity/Cohort filters and sub-tabs recompute the KPIs and waterfall client-side from the embedded data — no server needed.

A "Print / Save PDF" button in the masthead prints the currently open page in a clean, board-ready layout (sidebar and filters are hidden automatically).

## Data notes / known divergences from the source workbook

- **All-companies cash walk** (EBITDA → Cash Flow page): the workbook's own "All companies" cash formulas don't net every line (e.g. intercompany funding), so this figure is built by summing PCS's and PSSF's independently-validated cash walks line-by-line instead.
- **Corp/Other cohort** (Actual v. Budget → YTD page): the source tab's own Corp/Other column always computes to 0 across every named cost category because of a redundant filter condition in its formula, and dumps the true amount into a single catch-all bucket instead. This dashboard shows the true per-category split where derivable, with the remainder in an "Other / unclassified" row, so every column always reconciles exactly to that cohort's actual EBITDA change.
- **Cohort/Entity "All"**: matches the Bridge Deep-Dive tab's own behavior exactly — selecting Cohort="All" includes every cost center for that entity, including any not tagged to a named vintage cohort (so it can differ slightly from summing only the named cohort columns).
