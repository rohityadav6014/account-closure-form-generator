# Account Closure Form Generator

A single-page website that fills the **Account Closure / Deactivation Form** (trading account) and
**Annexure Q** (beneficiary / demat account) as an **editable PDF** from a client data file.

Everything runs in the browser. The uploaded file is never sent to any server.

## Use

1. Open `index.html` in Chrome or Edge (double-click it, or host it with GitHub Pages).
2. Upload the client data file (`.csv`, `.xlsx` or `.xls`).
3. Search by **UCC** (mobile, email and user ID also work).
4. Check the auto-filled details. If the UCC isn't in the file, fill the details manually.
5. Click **Generate PDF**. The PDF downloads, and every field stays editable in Acrobat, Chrome or Edge.

## Field mapping

| PDF field | Source column |
|---|---|
| Application number / Trading client ID | `ucc` |
| Name / Sole-First holder | `client_name` (falls back to `itd_name` if empty) |
| Mobile | `mobile_no` |
| Email ID | `email_id` |
| Address, City, State, PIN | `current_address1-3`, `current_city`, `current_state`, `current_pincode` (falls back to `permanent_*`) |
| Client ID (page 2) | `depository` without the `IN304877` DP ID prefix |
| Date | Today's date (DD-MM-YYYY), editable |

Column names are matched case-insensitively, and spaces are treated like underscores.

## Notes

- Needs internet on first load for three libraries from cdnjs: pdf-lib, PapaParse and SheetJS.
- Large CSVs (100+ MB) load in chunks and show a progress bar.
- If a UCC appears in several rows, the first row is used.
