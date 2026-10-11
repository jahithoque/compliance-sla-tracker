# Compliance SLA Tracker

A single-page, offline web app for tracking configuration-compliance findings against remediation SLAs.
No server, no install: open `index.html` in Edge, Chrome or Firefox. Uploaded data stays in your browser
(IndexedDB) and is never sent anywhere.

## Use

1. Download this repository (Code → Download ZIP) and unzip it. Keep `lib/` next to `index.html`.
2. Open `index.html` and drop in a compliance export (`.xlsx`, `.xls` or `.csv`).
3. Map the columns. Names don't have to match exactly; unmapped columns (e.g. Country) are ignored.
   - Required: Asset, Severity, Last Scanned Date, Last Compliant Date
   - Optional: #, Network, Test Category, Setting, First Detected
4. Click **Download report (.xlsx)** for the dashboard report.

## SLA policy (editable under SLA settings)

| Network | High / Critical | Medium / Low |
|---|---|---|
| DMZ | 60 days | 120 days |
| DRN | 110 days | 180 days |

`-` and `Unknown Status in QIP` use the DMZ rules by default.

- **Compliant**: Last Compliant Date is on or after Last Scanned Date.
- **SLA clock start**: Last Compliant Date, or First Detected if later. Never-compliant findings use the earliest of
  First Detected, the date the tracker first saw them failing, or Last Scanned Date.
- **Exceptions**: custom SLA days, custom due date, or risk accepted — per finding or in bulk, with reason and approver.

## Back up

Exceptions, first-seen dates and trend history live only in the browser. Use
**SLA settings → Back up tracker data (.json)** regularly, and restore from it on another machine.

## Third-party libraries (bundled in `lib/`)

- [SheetJS Community Edition](https://sheetjs.com) 0.20.3 — Apache License 2.0 (reading spreadsheets)
- [ExcelJS](https://github.com/exceljs/exceljs) 4.4.0 — MIT License (writing the report)
