# Phenix 1929 Holdings — Monthly Financial Review

Single-file, self-contained HTML dashboard, sourced from the final Phenix1929_Consolidated P&L workbook. All data is embedded directly in `index.html` as a JSON blob — no build step, no external requests, no CDN dependencies. Renders entirely with vanilla JS/SVG, with a left-hand sidebar for navigating between pages and a "Print / Save PDF" button in the masthead for assembling a board-ready PDF.

## View it locally

Just double-click `index.html`, or open it in any browser. The file is a few MB (it embeds full P&L detail for every PCS cost center), so allow a moment for it to load.

## Publish as a live site (GitHub Pages)

1. Create a new repository on GitHub (public or private both work; private repos need GitHub Pro for Pages).
2. Upload `index.html` to the root of the repo (drag-and-drop on the GitHub web UI works fine, or via git):
   ```
   git init
   git add index.html
   git commit -m "Phenix monthly financial review"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
3. In the repo, go to **Settings → Pages**.
4. Under "Build and deployment," set **Source** to "Deploy from a branch," pick branch `main` and folder `/ (root)`, then Save.
5. GitHub will publish it at `https://<your-username>.github.io/<your-repo>/` within a minute or two.

Any time you want to refresh the numbers, regenerate `index.html` and push again — GitHub Pages redeploys automatically on push.

## What's in the file

Six pages, selectable from the left sidebar, all "Adjusted" results unless noted:

- **EBITDA → Cash Flow**: Adjusted EBITDA → Unadjusted EBITDA → Free Cash Flow walk, including the balance-sheet-driven cash bridge (capex split into maintenance/other vs. acquisitions) and a cumulative cash-balance trend with 2026 Budget and Budget + Revised Proforma overlay lines. Filterable by Entity (PCS / PSSF / GP / All companies) and, for PCS, by individual operating Company.
- **Actual v. Prior Year**: LTM / PTD / YTD sub-tabs comparing current-year Adjusted EBITDA to the same period last year.
- **Actual → Forecast**: YTD / LTM sub-tabs bridging where the business stands today to the full-year 2026 outlook.
- **Actual v. Budget**: PTD / YTD / LTM sub-tabs comparing Adjusted EBITDA to the approved plan. The YTD view also includes a full category-by-cohort breakdown table.
- **P&L Statement (Adj.)** and **P&L Statement (Unadj.)**: full income statement — Revenue through Reported EBITDA — filterable by Entity, Company, and (for PCS) individual Cost Center. Columns cover FY2022–FY2025 annual, LTM, FY2026 Forecast, and YTD/PTD Actual-vs-Budget-vs-Prior-Year. Mirrors the workbook's "PCS Adj/Unadj P&L" and "Consolidated Adj/Unadj P&L" tabs. Cash-flow and balance-sheet detail is covered on the EBITDA → Cash Flow page rather than duplicated here.

The three comparison pages are sourced live (by cost category, Entity, and vintage Cohort) from the workbook's **Bridge Deep-Dive** tab, replicating its 8 built-in comparison templates. The two P&L Statement pages are sourced live from the **Adjusted TB** / **Unadjusted TB** at Entity/Company/Cost-Center granularity. All filters and sub-tabs recompute client-side from the embedded data — no server needed.

A "Print / Save PDF" button in the masthead prints the currently open page in a clean, board-ready layout (sidebar and filters are hidden automatically).

On the three comparison pages (Actual v. Prior Year / Actual → Forecast / Actual v. Budget), selecting a specific vintage cohort under Entity=PCS shows a chip list of the individual cost centers (locations) included in that cohort, right below the filter bar.

The Phenix Salon Suites logo is embedded in both the sidebar (inverted to white) and the masthead (original black), extracted as vector artwork straight from the uploaded `.ai` file so it stays crisp at any size.

## Data notes / known divergences from the source workbook

- **All-companies cash walk** (EBITDA → Cash Flow page): the workbook's own "All companies" cash formulas don't net every line (e.g. intercompany funding), so this figure is built by summing PCS's and PSSF's independently-validated cash walks line-by-line instead.
- **Corp/Other cohort** (Actual v. Budget → YTD page): the source tab's own Corp/Other column always computes to 0 across every named cost category because of a redundant filter condition in its formula, and dumps the true amount into a single catch-all bucket instead. This dashboard shows the true per-category split where derivable, with the remainder in an "Other / unclassified" row, so every column always reconciles exactly to that cohort's actual EBITDA change.
- **Cohort/Entity "All"**: matches the Bridge Deep-Dive tab's own behavior exactly — selecting Cohort="All" includes every cost center for that entity, including any not tagged to a named vintage cohort (so it can differ slightly from summing only the named cohort columns).
- **P&L Statement period columns**: shows the key annual/LTM/Forecast/YTD/PTD periods rather than every individual month back to 2022 (which the source tabs also offer) — this keeps the table readable for a monthly review; the underlying monthly data is available if you want it added back in.
- **Budget cash overlay**: the 2026 Budget and Budget + Revised Proforma cash lines only extend through May 2026 (the same window as actuals) since that's what the source workbook's "EBITDA to FCF Bridge" tab provides — there's no Jun–Dec budget cash trajectory yet.
