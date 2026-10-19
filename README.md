# 📦 PO Tracker Builder

A single-file, browser-only tool that fills PO trackers for **every channel** (FirstCry, Reliance, DMart, TATA 1MG, FirstClub, Purplle, Health & Glow) by merging a **warehouse sheet** with the **Master Tracker**.

**No install. No server. Your files never leave your computer.**

## Features

- Drag & drop the warehouse CSV and Master Tracker CSV
- Paste PO numbers, or load every PO of one, several or all channels
- Channel chips with live PO counts; KPIs, filters, copy and downloads all respect the selected channels
- Handles linked normal / `_OR1` balance re-order rows
- Animated KPI cards: POs, invoiced, dispatched, delivered, GRN done, open
- Live search and filters (open, not invoiced, not dispatched, not delivered, GRN pending)
- **Copy any single column** from its header, copy all rows, copy all columns, or copy invoice / dispatch / delivery groups, ready to paste into Google Sheets
- Row copy and double-click cell copy
- Open Balance tab with the reason each PO is open
- Download as Excel (with live qty-difference formulas) or CSV, named by channel and date, e.g. `PO_Tracker_FirstCry_2026-10-19.xlsx`
- Light / dark theme, compact density, keyboard shortcuts (`Ctrl+Enter` build, `/` search)

## Use it

1. Open `index.html` in any modern browser, or use the GitHub Pages link below.
2. Drop in the two CSVs.
3. Paste PO numbers (one per line).
4. Click **Build sheet**.

## Host free on GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Set source to **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. Your tool will be live at `https://<your-username>.github.io/<repo-name>/`.

## Notes

- Uses [PapaParse](https://www.papaparse.com/) and [SheetJS](https://sheetjs.com/) from cdnjs, so the first load needs internet.
- Expected headers: `PO Number` in the warehouse sheet and `PO NUMBER` in the Master Tracker.

## License

MIT
