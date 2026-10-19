<div align="center">

# PO Tracker Builder

**Fill every PO tracker from two sheets, right in your browser.**

Merge your warehouse sheet with the Master Tracker and get a completed, cross-checked tracker for
FirstCry, Reliance, DMart, TATA 1MG, FirstClub, Purplle and Health & Glow.

![Single file](https://img.shields.io/badge/single%20file-index.html-2340f0)
![No server](https://img.shields.io/badge/server-none-ffc933?labelColor=0d1330)
![Privacy](https://img.shields.io/badge/your%20files-never%20leave%20your%20browser-16a34a)
![License](https://img.shields.io/badge/license-MIT-0d1330)

</div>

---

## Why this exists

Updating a PO tracker by hand means looking up every PO in two different sheets, copying invoice numbers,
dispatch dates, AWBs and delivery status, and hoping nothing was missed. PO Tracker Builder does that lookup
for you, flags anything that looks wrong, and gives you a result you can paste straight into Google Sheets.

- **No install, no server, no account.** Open `index.html` and work.
- **Private by design.** Files are read and processed locally in your browser. Nothing is uploaded anywhere.
- **Built to be checked.** An accuracy banner and an Audit tab show exactly what was matched, what was linked and what needs a look.

## Quick start

1. Open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari), or use your GitHub Pages link.
2. Drop in the **Warehouse sheet** CSV.
3. Drop in the **Master Tracker** CSV.
4. Paste your PO numbers, or switch on **Load all POs of selected channels**.
5. Click **Build sheet** (or press `Ctrl` + `Enter`).

## Features

### Matching that handles real-world POs

| You paste | Warehouse sheet has | Result |
|---|---|---|
| `4200054047_OR1` | `4200054047_OR1` | Exact match |
| `4200054047` | `4200054047_OR1` | Finds the `_OR1` row and fills it from the Master Tracker |
| `4200054056-` or `4300125069_` | `4200054056_OR1`, `4300125069__OR1` | Trailing `-`, `_` and `.` are ignored |
| `7777` | `7777` and `7777_OR1` | Pulls every version of that PO |
| `8888_OR2` | only `8888_OR1` | Not swapped. Reported as not found |

- Warehouse-style and Master-style POs both work, so you can paste from either sheet.
- Linked normal / `_OR1` balance re-order rows are handled, with a toggle to use the linked master row when the exact one is empty.
- No duplicate rows when you paste the same PO in two styles.
- POs can be separated by new lines, commas, spaces or tabs. Quotes are ignored.

### Reads messy Master Trackers

- Headers that wrap across lines inside one cell (for example `DISPATCH` + `DATE`) are read correctly.
- Emoji and hidden characters in headers are ignored.
- Several tables stacked in one sheet are supported. Each table is read with its own headers.
- Alternate header spellings are recognised, and `Dispatch Date` also accepts names like "Dispatched On Date" or "Date of Handover".
- If a PO appears on two Master rows, blank dispatch, AWB and transporter fields are filled from the other row of the same PO.
- Dates in many formats (`15-Oct-2026`, `2026-10-15`, `15/10/2026`, Excel serials) are normalised to `DD-Mon-YYYY`.

### Results you can trust

- **Accuracy banner:** how many built POs are clean, how many need a check, and how many were not found, with an **Open Audit** shortcut.
- **KPI rings:** POs, Invoiced, Dispatched, Delivered, GRN done and Open, each with its percentage.
- **Channel mix bar:** the split of your POs by channel.
- **Audit tab:** every decision the tool made, including which master row was linked and which dates could not be read.
- **Open Balance tab:** each open PO with the reason it is open (no invoice, not dispatched, not delivered, GRN pending, short invoiced quantity).
- Warning markers on any PO that needs a quick check.

### Work faster

- **Channel chips with logos and live counts.** KPIs, filters, copy and downloads all respect the selected channels.
- **Search** across PO, location, invoice and AWB. Press `/` to jump to it.
- **Filters:** open, not invoiced, not dispatched, not delivered, GRN pending.
- **Copy any single column** from its header, copy all rows, all columns, or the invoice, dispatch and delivery groups. All paste cleanly into Google Sheets.
- Row copy and double-click cell copy.
- **Download Excel** (with live quantity-difference formulas) or **CSV**, named by channel and date, for example `PO_Tracker_FirstCry_2026-10-19.xlsx`.
- Your pasted PO list is remembered in the browser so a refresh does not lose it.
- Light and dark themes, comfortable and compact density.

## Expected sheet headers

Header names are matched ignoring case, dots, extra spaces and line breaks.

**Warehouse sheet** (header on the first row)

| Required | Used when present |
|---|---|
| `PO Number` | `Marketplace`, `PO Value`, `PO Qty`, `PO Date`, `Delivery Location`, `Processing Date`, `Dispatch Date`, `Dispatch Status`, `Slot Date`, `Slot Confirmed`, `Invoice Number`, `Invoice Date`, `Invoice Qty`, `Invoice Value`, `Delivered`, `GRN Status`, `Delivery Partner`, `Invoice AWB`, `No of boxes` and the TAT and remarks columns |

**Master Tracker** (header row is found automatically)

| Required | Used when present |
|---|---|
| `PO NUMBER` | `CHANNEL`, `INVOICE NO`, `INVOICE DATE`, `BOXES`, `DISPATCH QTY`, `AWB NUMBER`, `TRANSPORTER`, `DISPATCHED`, `DISPATCH DATE`, `APPOINTMENT DATE`, `APPOINTMENT STATUS`, `DELIVERED`, `DELIVERY DATE`, `GRN DONE`, `PO<>INVOICE TAT`, `INVOICE<>DELIVERY TAT`, `PO<>DELIVERY TAT`, `TOTAL DEDUCTIONS`, `DEDUCTION REASON`, `REMARKS`, `POD STATUS` |

Export each Google Sheet tab as **File → Download → Comma-separated values (.csv)**.

## Troubleshooting

| Problem | What to do |
|---|---|
| A column such as Dispatch Date comes out blank | Open the **Audit** tab. It says whether the column was found under another name or not recognised at all. If not, rename the Master header to `Dispatch Date`. |
| "PO(s) not found in the warehouse sheet" | The PO is not in the warehouse CSV you uploaded. Check you exported the correct tab and that any filter was cleared before exporting. |
| Warning marker next to a PO | Hover it or open the Audit tab. Typical causes: dispatch date missing, invoice number without an invoice date, or two Master rows for one PO. |
| Fonts or download buttons do not work | The tool loads fonts and two libraries from the internet on first load. Check your connection and refresh. |
| Old version still showing | Hard refresh with `Ctrl` + `Shift` + `R`. |

## Keyboard shortcuts

| Keys | Action |
|---|---|
| `Ctrl` + `Enter` | Build sheet |
| `/` | Focus search |

## Host it free on GitHub Pages

1. Create a repository and upload `index.html` and `README.md` to the root.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. Your tool goes live at `https://<your-username>.github.io/<repo-name>/`.

## Project structure

```
.
├── index.html   # the whole app: markup, styles and logic
├── README.md
└── LICENSE      # MIT
```

## Tech notes

- Plain HTML, CSS and JavaScript in one file. No build step.
- [PapaParse](https://www.papaparse.com/) 5.4.1 for CSV and [SheetJS](https://sheetjs.com/) 0.18.5 for Excel export, loaded from cdnjs.
- Fonts: Bricolage Grotesque and Figtree from Google Fonts, with system-font fallbacks.
- The matching logic lives in a single `buildCore` function so it can be tested on its own.
- Channel badges are simple colour monograms, not official brand logos.

## Contributing

Issues and pull requests are welcome. If a Master Tracker layout is not read correctly, open an issue with the header row (no PO or customer data needed) and what you expected.

## License

MIT. See `LICENSE`.

<div align="center">

Built for supply chain ops by [vishnumohanesv-wq](https://github.com/vishnumohanesv-wq)

</div>
