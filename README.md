# PUBLIC SERVICE ADVISORY GENERATOR

Standalone report tool for the **DENR-EMB Central Visayas AQMS Live Tracker**.

This is a self-contained copy of the **Reports → Public Service Advisory Generator** feature.
It stays connected to the **same live Google Sheets data source** as the main application and
auto-refreshes every **5 seconds**.

## Files

| File | Purpose |
| --- | --- |
| `PUBLIC-SERVICE-ADVISORY-GENERATOR.html` | The standalone generator — open this in a browser. |
| `New Background.png` | Poster background image used by the advisory renderer. |
| `DENR LOGO.png` | Logo drawn on the generated advisory. |
| `New Bagong Pilipinas.png` | Logo drawn on the generated advisory. |

> Keep the three image files in the same folder as the HTML file so the poster renders correctly.

## Features

### 1. CONTINUOUS MONITORING ONLY
Selects the data used for the advisory from the continuous monitoring sheets.
- **Monitoring Station** — populated live from the continuous records.
- **Parameter** — PM2.5 or PM10.
- **Trend Period** — 24 Hours, 3 Days, or 7 Days.
- **AQI Graph Range** — 100 / 150 / 200 / 250 / 300 / 500, or a **Custom** value (50–500).
- **Start Date / Time** and **End Date / Time** — filter the observation window.

### 2. GENERATE PUBLIC SERVICE ADVISORY
Renders a shareable **1080 × 1350** advisory poster (canvas) from the filtered continuous
observations: station name, parameter, latest AQI value, remarks/category, AQI legend, and
an AQI trend chart with a 100-AQI safe-limit line.

### 3. PUBLIC SERVICE ADVISORY PREVIEW
Shows the generated poster image. Right-click, drag, and text selection are disabled in the
preview frame (the downloadable file is gated separately).

### 4. ADVISORY SUMMARY REPORT
Side panel that summarizes the selected advisory:
- **Report Information** — station, parameter, trend period, date range, generated timestamp.
- **Current AQI Status** — latest AQI value and category (colour-coded).
- **Observation Summary** — count of processed observations and computed AQI.
- **Data Statistics** — total records, minimum / maximum / average / latest AQI.
- **AQI Category Legend** and **Report Source** note.

### 5. DOWNLOAD PUBLIC SERVICE ADVISORY
Downloads the generated advisory as a PNG:
`DENR-EMB-CV-PUBLIC-SERVICE-ADVISORY-<STATION>-<PARAMETER>-<DATE>.png`

### 6. ADVISORY GENERATION LOG
Records each generated advisory (timestamp, station, parameter, trend period, latest AQI,
category, record count, downloaded status).
- **DOWNLOAD ADVISORY LOG 🔒** exports the log as CSV.
- **CLEAR LOG** clears the stored log.

### 7. Administrator Login
The **preview is public**, but **downloading the advisory image and the advisory log requires
the administrator session**.

- **Username:** `DENREMB7`
- **Password:** `aqmsemb7`
- Credentials are the same as the main AQMS application.
- The session is stored in `sessionStorage` under `aqms-advisory-admin-authenticated`.
- Click **LOG IN / LOG OUT** under the download buttons to manage the session.

## Data Source

Live records are read directly from the AQMS Google Spreadsheet via the `gviz` CSV endpoint:

```
https://docs.google.com/spreadsheets/d/1Fh6w15beHCAHPGJw-2nfwNryez3vwnSVCd8bsFGKvHE/gviz/tq?tqx=out:csv&sheet=<SHEET NAME>
```

Sheets used (Continuous Monitoring only):
- `Talisay City`
- `City of Toledo`

Manual LGU, TSP, and Manual PM10 observations are **excluded** by design.

## Notes

- The advisory preview and stats update automatically as the sheet data changes.
- Internet access is required to reach the Google Sheets source.
- The generator is view-only against the source; it never writes back to the spreadsheet.
