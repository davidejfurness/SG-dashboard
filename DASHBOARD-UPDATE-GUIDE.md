# Shelford Group Dashboard – Monthly Update Guide

## ⚠️ CRITICAL: Data Integrity Rules

**Every figure on this dashboard must come from a verifiable source file.** This is the single most important rule for maintaining the dashboard.

### The Golden Rules

1. **Never fabricate data.** If a source file is not available for a metric, that metric must be removed from the dashboard — not populated with estimates, illustrative figures, or AI-generated values.

2. **Every number must be traceable.** Each data point should be extractable from a specific cell, row, or record in a named source file. If you cannot point to where a number came from, it should not be on the dashboard.

3. **Cross-check averages.** Shelford averages must be computed from verified trust-level figures, not stated independently. Weighted averages (e.g. bed occupancy) must use verified numerators and denominators.

4. **National averages must come from the same source** as the trust-level data, not from memory or different publications.

5. **Trend data requires a time series source.** Monthly or quarterly trends must come from a file that contains the full time series — never extrapolated or smoothly interpolated between two known points. A telltale sign of fabricated trends is monotonic smooth curves with no seasonal variation.

6. **When in doubt, leave it out.** A dashboard with fewer verified metrics is far more valuable than one padded with plausible-looking but fabricated figures.

### How fabrication was caught (February 2026 audit)

In February 2026, a comprehensive audit found fabricated data across every dashboard page. Warning signs included:

- People Promise scores with perfect 0.2 increments across all trusts (identical rank order for every theme)
- Monthly A&E attendance figures that were smooth sequences for every trust with no seasonal variation
- Trend lines that declined monotonically — real NHS data shows winter peaks and summer troughs
- Values that were close to but consistently different from verified source data (e.g. bed occupancy errors of up to 10 percentage points)
- Critical care occupancy and MFFD figures with no available source file
- NOF segment scores wrong for every trust (20 segment errors, 43 domain score errors)
- Sickness absence and vacancy rates that were plausible but entirely invented

**If updating with AI assistance, always upload source files and instruct the AI to extract data only from those files.** Do not ask for "illustrative" or "placeholder" data.

---

## Dashboard Structure (9 pages)

| Page | File | Primary Data Sources | Last verified |
|------|------|---------------------|---------------|
| Overview | `index.html` | Multiple (see detail pages); NHS Oversight Framework | Feb 2026 |
| RTT & Elective Care | `rtt-detail.html` | NHS England RTT Data; Acute Provider Time Series | Feb 2026 |
| A&E & Urgent Care | `ae-detail.html` | NHS England A&E Attendances; Acute Provider Time Series | Feb 2026 |
| Cancer Services | `cancer-detail.html` | NHS England Cancer Waiting Times; Acute Provider Time Series | Feb 2026 |
| Patient Safety & Quality | `quality-detail.html` | Friends & Family Test MacroWebfiles; Patient Safety Events Quarterly | Feb 2026 |
| Capacity & Beds | `capacity-detail.html` | NHS England KH03 Beds Open Overnight | Feb 2026 |
| Workforce | `workforce-detail.html` | NHS Staff Survey Benchmark Report; NHS Sickness Absence Rates (ESR) | Feb 2026 |
| Research & Clinical Trials | `research-detail.html` | NIHR Open Data Platform / Shelford data collection | Previously verified |
| Productivity & Finance | `productivity-detail.html` | NHS England Productivity Growth Estimates; Shelford CFO Updates | Previously verified |

---

## Verified Data Sources — Current Dashboard

This section records exactly which source files were used for the data currently on the dashboard, verified during the February 2026 audit. When updating, replace these references with the new source files used.

### RTT & Elective Care (`rtt-detail.html`)

| Data element | Source file | Key details |
|---|---|---|
| Trust-level RTT % (Nov 2025) | `Full-CSV-data-file-Dec25.csv` (NHS England RTT Data) | Column: Total incomplete pathways % within 18 weeks |
| RTT trend (Feb–Dec 2025) | `acute-provider-timeseries-feb-2026.csv` | Metric: "Percentage waiting within 18 weeks for elective treatment" |
| 52-week+ waiters | Same RTT CSV | Total incomplete pathways 52+ weeks |
| England averages | Same time series CSV | Provider.Name = "England" |

**Known issue:** Sheffield RTT frozen at 66.0% from June 2025 onwards in time series (data submission issue at trust).

### A&E & Urgent Care (`ae-detail.html`)

| Data element | Source file | Key details |
|---|---|---|
| Trust-level 4hr %, attendances, 12hr DTA (Jan 2026) | `January-2026-AE-by-provider-mj588-1.xls` | "All types" columns for 4hr performance; "Acute" rows for 12hr DTA waits |
| 4hr trend (Feb 2025–Jan 2026) | `acute-provider-timeseries-feb-2026.csv` (Feb–Dec 2025) + A&E file (Jan 2026) | Metric: "A&E 4 hour performance" |
| 12hr % trend (Feb–Dec 2025) | Same time series CSV | Metric: "A&E 12 hour performance" (% >12hrs arrival-to-departure, all patients — different from DTA waits for admitted patients only) |
| England averages | A&E file (Jan 2026 snapshot) + time series (trends) | |

**Note:** Ambulance handover data was removed — not in A&E file, requires separate ambulance quality indicators source. Stacked monthly attendances replaced with Jan 2026 snapshot bar chart (time series does not contain monthly attendances).

### Cancer Services (`cancer-detail.html`)

| Data element | Source file | Key details |
|---|---|---|
| Trust-level 62-day, FDS, 2WW, 31-day (Nov 2025) | `CRS-Cancer-Provider-Data-November-2025.xlsx` | "Provider_level" sheet, filter by Shelford ODS codes |
| Cancer trends (Dec 2024–Dec 2025) | `acute-provider-timeseries-feb-2026.csv` | Metrics: "Cancer 62 Day Combined Performance", "Cancer Faster Diagnostic Standard" |
| England averages | Same time series CSV | Provider.Name = "England" |

### Patient Safety & Quality (`quality-detail.html`)

| Data element | Source file | Key details |
|---|---|---|
| FFT A&E recommend % (Dec 2025) | `FFT_AE_MacroWebfile_Dec-25.xlsm` | "Trusts" sheet; Col 2 = ODS code, Col 6 = % positive; England in rows 12–13 |
| FFT Inpatient recommend % (Dec 2025) | `FFT_IP_MacroWebfile_Dec-25-1.xlsm` | Same structure as A&E MacroWebfile; England incl. IS = 94.8% |
| Patient safety event rate, incidents, bed days (Q2 2025/26) | `Patient-Safety-Event-Data-Quarterly-Publication-Recording-Rates-and-Median-Lag-by-NHS-Trusts-2025_26_Q2.csv` | Columns: Recording Rate, Number of Incidents, Activity Denominator |

**Note:** Infection control data (C. difficile, MRSA, E. coli) was removed — no HCAI source file was available at the time of the audit. When HCAI data is obtained, this section can be reinstated. FFT files are macro-enabled (.xlsm); use `openpyxl` with `data_only=True` to read computed values.

### Capacity & Beds (`capacity-detail.html`)

| Data element | Source file | Key details |
|---|---|---|
| G&A bed occupancy, available/occupied beds (Q3 2025/26) | `Beds-Open-Overnight-Web_File-Q3-2025-26.xlsx` | "NHS Trust by Sector" sheet; Col 5 = ODS code, Col 8 = G&A available, Col 14 = G&A occupied, Col 20 = G&A % occupied |
| England averages | Same file, row where Col 6 name contains "England" | |

**Note:** This is quarterly KH03 data (Oct–Dec 2025), not weekly. Critical care occupancy and MFFD were removed — not in KH03 file, would require separate sources. The previous dashboard incorrectly cited "January 2026" as the data period.

### Workforce (`workforce-detail.html`)

| Data element | Source file | Key details |
|---|---|---|
| Staff Survey 2024 — all metrics | `Benchmark-report-Excel-data-for-2020-2024.xlsx` | "Acute&Acute Community Trusts" sheet; 122 trusts |
| Staff engagement (theme_engagement_2024) | Same file, Col 29 | Score out of 10 |
| Morale (theme_morale_2024) | Same file, Col 33 | Score out of 10 |
| Recommend as place to work (q25c_2024) | Same file, Col 119 | % agree/strongly agree |
| Happy with standard of care (q25d_2024) | Same file, Col 120 | % agree/strongly agree |
| People Promise PP1–PP7 | Same file, Cols 7, 12, 13, 16, 20, 23, 26 | Scores out of 10 |
| Acute trust averages | Computed as mean across all 122 trusts in the sheet | |
| Sickness absence (Nov 2025) | `NHS_Sickness_Absence_rates__November_2025.xlsx` | "Table 4" sheet; Col 6 = ODS code, Col 158 = November 2025 |
| Sickness absence — England | Same file, "Table 1" sheet | Col 2 = England rate |
| Sickness trend (Dec 2024–Nov 2025) | Same file, Table 4 Cols 147–158; Table 1 for England | 12 months of monthly rates |

**Note:** Vacancy rates are not currently included. The NHS Vacancy Statistics file (`nhs-vac-stats-apr15-dec25-eng-tables.xlsx`) contains regional/sector-level data only, not trust-level. Trust-level vacancy data would require a different source.

### Overview / Index (`index.html`)

| Data element | Source | Notes |
|---|---|---|
| KPI cards (A&E, RTT, Cancer) | Computed from verified detail page data | A&E from Jan 2026, RTT and Cancer from Nov 2025 |
| National averages in KPI cards | Time series CSV + A&E file | England: A&E 72.5%, RTT 61.8%, Cancer 70.2% |
| Trust comparison table | Same as detail pages | 3 columns: A&E 4hr, RTT 18wk, Cancer 62d |
| NOF segments and domain scores | `nhs-oversight-framework-acute-trust-data-q2.csv` | OF5000 = adjusted segment; OF4000/4002/4003/4004/4005 = domain scores; OF4100–4105 = domain segments; OF5002 = average metric score |
| National Ranking: RTT, A&E, Cancer, FDS | Same NOF CSV | OF0023, OF0013, OF0014, OF0011, OF0010 (with median/LQ/UQ from same file) |
| National Ranking: Staff engagement | Same NOF CSV (OF0084) | Median/LQ/UQ from same file |
| National Ranking: Sickness absence | `NHS_Sickness_Absence_rates__November_2025.xlsx` | Trust-level Nov 2025 values; NOF sickness (OF0082) uses an earlier period |

**Removed during Feb 2026 audit:** Diagnostic 6-week KPI (no DM01 source), C. difficile rate (no HCAI source), discharge delay days (available in NOF but not independently verified).

---

## Data Sources and Publication Schedule

### Monthly publications (update every month)

| Source | What it covers | Published | URL |
|--------|---------------|-----------|-----|
| **NHS England A&E Attendances and Emergency Admissions** | Total attendances, 4hr performance, 12hr DTA waits – trust-level | ~12th of each month | [england.nhs.uk/statistics](https://www.england.nhs.uk/statistics/statistical-work-areas/) |
| **NHS England RTT Data** | RTT incomplete pathways, 18-week and 52-week performance – trust-level | ~12th of each month | Same statistics page |
| **NHS England Cancer Waiting Times** | 2-week wait, 28-day FDS, 62-day, 31-day – trust-level | ~12th of each month | Same statistics page |
| **Friends & Family Test** | A&E and Inpatient recommend % – trust-level | ~12th of each month | Same statistics page |
| **Acute Provider Time Series** | Monthly trends for RTT, A&E, cancer, diagnostics – all providers | Published alongside monthly stats | Same statistics page |
| **NHS Sickness Absence Rates** | Sickness absence % from ESR – trust-level monthly time series | Monthly (~2 months lag) | [digital.nhs.uk](https://digital.nhs.uk/data-and-information/publications/statistical/nhs-sickness-absence-rates) |

**Note on FFT files:** You need the two MacroWebfiles (.xlsm): `FFT_AE_MacroWebfile` and `FFT_IP_MacroWebfile`. The headline FFT file only contains national-level figures. Read with `openpyxl` using `data_only=True`.

**Note on the Acute Provider Time Series:** This CSV contains data as proportions (0–1) in Column E. Multiply by 100 for percentages. It is the single best source for trend charts across A&E, RTT, and cancer as it contains all providers and all months in one file.

### Quarterly publications

| Source | What it covers | Published | URL |
|--------|---------------|-----------|-----|
| **KH03 Beds Open Overnight** | G&A and total bed occupancy – trust-level quarterly average | ~2 months after quarter end | [england.nhs.uk/statistics/bed-availability](https://www.england.nhs.uk/statistics/statistical-work-areas/bed-availability-and-occupancy/) |
| **Patient Safety Events Quarterly** | Recording rates, incidents, bed days – trust-level | Quarterly | [england.nhs.uk](https://www.england.nhs.uk/patient-safety/learning-from-patient-safety-events/) |
| **HCAI Data** | C. difficile, MRSA, E. coli rates – trust-level | Quarterly (~2 months after quarter end) | [england.nhs.uk/statistics/hcai](https://www.england.nhs.uk/statistics/statistical-work-areas/hcai/) |
| **NHS Oversight Framework** | Trust segmentation and domain scores | ~Twice yearly | [england.nhs.uk/nhs-oversight-framework](https://www.england.nhs.uk/nhs-oversight-framework/) |
| **NHS England Productivity Growth Estimates** | Trust-level productivity (output vs input growth) | Published with monthly stats (new measure from Feb 2026) | [england.nhs.uk/statistics](https://www.england.nhs.uk/statistics/statistical-work-areas/) |

### Annual publications

| Source | What it covers | Published | URL |
|--------|---------------|-----------|-----|
| **NHS Staff Survey Benchmark Report** | Staff engagement, People Promise scores, recommend %, morale – trust-level | March (for previous autumn's survey) | [nhsstaffsurveys.com/results](https://www.nhsstaffsurveys.com/results/) |

### Internal data (update when received)

| Source | What it covers | Frequency |
|--------|---------------|-----------|
| **Shelford CFO Monthly Updates** | Provider surplus/deficit (plan vs actual), CIP delivery – trust-level | Monthly (received from CFO group) |
| **NIHR Open Data Platform / Shelford data collection** | 90-day trial setup performance – trust-level | Periodically |

**Note on CFO data:** This is confidential to the Shelford Group. The spreadsheet uses £000s for most trusts but Oxford sometimes reports in £millions — check and normalise before updating. Manchester data is often incomplete. Finance data appears on the Productivity & Finance page only.

---

## The 10 Shelford Group Trusts

| Short name (dashboard) | Full trust name | ODS code |
|------------------------|----------------|----------|
| Birmingham | University Hospitals Birmingham NHS Foundation Trust | RRK |
| Cambridge | Cambridge University Hospitals NHS Foundation Trust | RGT |
| GSTT | Guy's and St Thomas' NHS Foundation Trust | RJ1 |
| Imperial | Imperial College Healthcare NHS Trust | RYJ |
| King's | King's College Hospital NHS Foundation Trust | RJZ |
| Manchester | Manchester University NHS Foundation Trust | R0A |
| Newcastle | The Newcastle Upon Tyne Hospitals NHS Foundation Trust | RTD |
| Oxford | Oxford University Hospitals NHS Foundation Trust | RTH |
| Sheffield | Sheffield Teaching Hospitals NHS Foundation Trust | RHQ |
| UCLH | University College London Hospitals NHS Foundation Trust | RRV |

---

## How to Prepare the Monthly Update

### What to provide

Download the relevant NHS England Excel/CSV files. For a standard monthly update, you need:

1. **RTT Data** (Full CSV data file) – trust-level RTT performance
2. **A&E Attendances and Emergency Admissions** (Excel) – trust-level attendances, 4hr, 12hr DTA
3. **Cancer Waiting Times** (Excel) – trust-level cancer performance
4. **Acute Provider Time Series** (CSV) – single file covering RTT, A&E, cancer trends
5. **Friends & Family Test** (xlsm) – Two files: `FFT_AE_MacroWebfile` and `FFT_IP_MacroWebfile`
6. **Shelford CFO Monthly Updates** (xlsx) – when received from CFO group

For quarterly updates, also include:

7. **KH03 Beds Open Overnight** (xlsx)
8. **Patient Safety Events Quarterly** (CSV)
9. **HCAI Data** (xlsx) – when available
10. **NHS Sickness Absence Rates** (xlsx)

For annual updates:

11. **NHS Staff Survey Benchmark Report** (xlsx) – published March each year
12. **NHS Oversight Framework** (CSV) – when new segmentation published

---

## Update Prompt Template

Copy and paste the following prompt when you're ready to update:

---

**PROMPT:**

> Please update the Shelford Group Performance Dashboard with the latest data. I've uploaded the source files.
>
> **CRITICAL: Extract data ONLY from the uploaded source files. Do not use any values from memory, estimates, or illustrative figures. If a source file is missing for a metric, tell me rather than populating with fabricated data. Every number on the dashboard must be traceable to a specific cell in a specific uploaded file.**
>
> **Month/period being updated:** [e.g. December 2025 data, published January 2026]
>
> **Files uploaded:**
> - [List each file you're uploading]
>
> **Specific notes:**
> - [Any known data issues, e.g. "Cambridge RTT figures look unusually low"]
> - [Any trusts with missing CFO data this month]
> - [Any structural changes needed]
>
> Please update the relevant dashboard pages with the new figures. Extract the data for the 10 Shelford trusts only (RRK, RGT, RJ1, RYJ, RJZ, R0A, RTD, RTH, RHQ, RRV).
>
> For each page updated, confirm:
> 1. Which source file each data point came from
> 2. The exact values extracted for each trust
> 3. Any metrics that could not be updated due to missing source data
>
> Output all updated HTML files.

---

## Critical: index.html Data Format

The trust comparison table on the overview page is powered by a JavaScript array called `trustData`. The property names **must** match exactly or the table will show `undefined%`. The current format is:

```javascript
const trustData = [
    { name: 'Birmingham', rtt: 61.5, ae: 61.1, cancer: 68.6 },
    // ... etc
];
```

**Property names that the table rendering code expects:**
- `name` — trust short name
- `ae` — A&E 4-hour performance
- `rtt` — RTT 18-week performance
- `cancer` — Cancer 62-day performance

If these are renamed, the table will break and show `undefined%`.

---

## Access Control

The dashboard uses client-side passphrase protection. The current passphrase is **shelford2026** (case-insensitive). It is SHA-256 hashed in the source code. The cookie expires after 365 days.

To change the passphrase: provide the new passphrase to Claude and ask it to regenerate the hash across all 9 HTML pages.

Contact email shown on the login screen: info@shelfordgroup.org

---

## Notes

- The elective recovery plan benchmarks (65% by March 2026, 70% by March 2027, 92% by March 2029) are static policy targets. Update only if the government revises them.
- The NOF segmentation data changes infrequently. Update only when a new segmentation is published by NHS England.
- Oxford CFO data sometimes switches between £000s and £millions mid-spreadsheet. Always check and normalise to £000s.
- Manchester CFO data is often incomplete. Leave gaps rather than estimating.
- The research page shows period-on-period comparison. When updating, move the current "latest" data to "previous" and add the new data as "latest".
- Sheffield RTT data appears frozen at 66.0% from June 2025 in the time series — this is a known data submission issue at the trust level.
- If a data source changes format or URL, note this in the update conversation.
