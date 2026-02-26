# Shelford Group Dashboard – Monthly Update Guide

## Overview

This document provides instructions for updating the Shelford Group Performance Dashboard on a monthly basis. It maps each dashboard page to its NHS data source(s), sets out the publication calendar, and includes a ready-made prompt for Claude.

---

## Dashboard Structure (9 pages)

| Page | File | Primary Data Sources |
|------|------|---------------------|
| Overview | `index.html` | NHS England Acute Provider Table; NHS Oversight Framework |
| RTT & Elective Care | `rtt-detail.html` | NHS England RTT/Acute Provider Table |
| A&E & Urgent Care | `ae-detail.html` | NHS England A&E Attendances and Emergency Admissions |
| Cancer Services | `cancer-detail.html` | NHS England Cancer Waiting Times |
| Patient Safety & Quality | `quality-detail.html` | NHS England HCAI Data; Friends & Family Test |
| Capacity & Beds | `capacity-detail.html` | NHS England Bed Availability and Occupancy Data |
| Workforce | `workforce-detail.html` | NHS Digital Workforce Statistics; NHS Staff Survey |
| Research & Clinical Trials | `research-detail.html` | NIHR Open Data Platform |
| Productivity & Finance | `productivity-detail.html` | NHS England Productivity Growth Estimates; Shelford CFO Monthly Updates (internal) |

---

## Data Sources and Publication Schedule

### Monthly publications (update every month)

| Source | What it covers | Published | URL |
|--------|---------------|-----------|-----|
| **NHS England Acute Provider Table** | RTT, A&E 4hr, cancer 62-day, diagnostics – trust-level | ~12th of each month (for previous month) | [england.nhs.uk/statistics](https://www.england.nhs.uk/statistics/statistical-work-areas/) |
| **A&E Attendances and Emergency Admissions** | Total attendances, 12hr waits, ambulance handovers – trust-level | ~12th of each month | Same statistics page |
| **Cancer Waiting Times** | 2-week wait, 28-day FDS, 62-day – trust-level | ~12th of each month | Same statistics page |
| **Friends & Family Test** | A&E and Inpatient recommend % – trust-level | ~12th of each month | Same statistics page |

**Note on FFT files:** The trust-level FFT data is published as macro-enabled Excel files (.xlsm), not CSV. You need two files: `FFT_AE_MacroWebfile` and `FFT_IP_MacroWebfile`. The headline FFT file only contains national-level figures.

### Internal data (update when received)

| Source | What it covers | Frequency |
|--------|---------------|-----------|
| **Shelford CFO Monthly Updates** | Provider surplus/deficit (plan vs actual), CIP delivery – trust-level | Monthly (received from CFO group) |
| **NIHR Open Data Platform / Shelford data collection** | 90-day trial setup performance – trust-level | Periodically |

**Note on CFO data:** This is confidential to the Shelford Group. The spreadsheet uses £000s for most trusts but Oxford sometimes reports in £millions — check and normalise before updating. Manchester data is often incomplete. Finance data appears on the Productivity & Finance page only.

### Weekly publications (update as needed)

| Source | What it covers | Published | URL |
|--------|---------------|-----------|-----|
| **Bed Availability and Occupancy** | G&A occupancy, critical care – trust-level | Weekly (usually Thursdays) | [england.nhs.uk/statistics/bed-availability](https://www.england.nhs.uk/statistics/statistical-work-areas/bed-availability-and-occupancy/) |

### Quarterly publications (update when available)

| Source | What it covers | Published | URL |
|--------|---------------|-----------|-----|
| **HCAI Data** | C. difficile rates, MRSA, E. coli – trust-level | Quarterly (~2 months after quarter end) | [england.nhs.uk/statistics/hcai](https://www.england.nhs.uk/statistics/statistical-work-areas/hcai/) |
| **NHS Digital Workforce Statistics** | Vacancy rates, sickness absence – trust-level | Quarterly | [digital.nhs.uk/workforce](https://digital.nhs.uk/data-and-information/publications/statistical/nhs-workforce-statistics) |
| **NHS Oversight Framework** | Trust segmentation and domain scores | ~Twice yearly | [england.nhs.uk/nhs-oversight-framework](https://www.england.nhs.uk/nhs-oversight-framework/) |
| **NHS England Productivity Growth Estimates** | Trust-level productivity (output vs input growth) | Published with monthly stats (new measure from Feb 2026) | [england.nhs.uk/statistics](https://www.england.nhs.uk/statistics/statistical-work-areas/) |

### Annual publications (update once per year)

| Source | What it covers | Published | URL |
|--------|---------------|-----------|-----|
| **NHS Staff Survey** | Staff engagement, People Promise scores, recommend % – trust-level | March (for previous autumn's survey) | [nhsstaffsurveys.com/results](https://www.nhsstaffsurveys.com/results/) |

---

## Critical: index.html Data Format

The trust comparison table on the overview page is powered by a JavaScript array called `trustData`. The property names **must** match exactly or the table will show `undefined%`. The correct format is:

```javascript
const trustData = [
    { name: 'Birmingham', rtt: 61.5, ae: 61.1, cancer: 68.6, fds: 83.4, diagnostic: 42.1 },
    // ... etc
];
```

**Property names that the table rendering code expects:**
- `name` — trust short name
- `ae` — A&E 4-hour performance (NOT `ae4hr`)
- `rtt` — RTT 18-week performance
- `cancer` — Cancer 62-day performance (NOT `cancer62`)
- `fds` — Cancer Faster Diagnosis Standard
- `diagnostic` — Diagnostics 6-week breach rate (NOT `diag`)

If these are renamed to anything else, the table will break and show `undefined%`.

---

## How to Prepare the Monthly Update

### What to provide

Download the relevant NHS England Excel/CSV files and put them in a zip folder. For a standard monthly update, you need:

1. **Acute Provider Table** (Excel) – covers RTT, A&E, cancer, diagnostics for all trusts
2. **A&E Attendances** (Excel/CSV) – trust-level attendances, 12hr waits, ambulance handovers
3. **Cancer Waiting Times** (Excel) – if month aligns with cancer publication
4. **Friends & Family Test** (xlsm) – Two files: `FFT_AE_MacroWebfile` and `FFT_IP_MacroWebfile`
5. **Bed Availability and Occupancy** (Excel) – latest week's data
6. **Shelford CFO Monthly Updates** (xlsx) – when received from CFO group
7. **Research/trials data** (xlsx) – when new NIHR data available

For quarterly updates, also include:
8. **HCAI Data** (Excel)
9. **Workforce Statistics** (Excel)
10. **Productivity Growth Estimates** (xlsx) – when new publication available

### File naming convention (suggested)

```
dashboard-update-[month]-[year]/
├── acute-provider-table.xlsx
├── ae-attendances.xlsx
├── cancer-waiting-times.xlsx
├── FFT_AE_MacroWebfile.xlsm
├── FFT_IP_MacroWebfile.xlsm
├── bed-occupancy.xlsx
├── cfo-monthly-update.xlsx       (when received)
├── productivity-estimates.xlsx   (when published)
├── research-trials.xlsx          (when new data available)
├── hcai-data.xlsx                (quarterly only)
├── workforce-stats.xlsx          (quarterly only)
├── staff-survey-2025.xlsx        (annual only)
└── notes.txt                     (any context or corrections)
```

Zip this folder and upload it to the conversation.

---

## Update Prompt Template

Copy and paste the following prompt when you're ready to update:

---

**PROMPT:**

> Please update the Shelford Group Performance Dashboard with the latest data. I've uploaded a zip file containing the source data.
>
> **Month/period being updated:** [e.g. December 2025 data, published January 2026]
>
> **Files included:**
> - Acute Provider Table (covers RTT, A&E, cancer, diagnostics)
> - A&E Attendances and Emergency Admissions
> - Friends & Family Test – two xlsm files: AE MacroWebfile and IP MacroWebfile
> - Bed Availability and Occupancy (week ending [date])
> - [Shelford CFO Monthly Updates – M[X] (if included)]
> - [Research trials data (if included)]
> - [Add any quarterly/annual sources if included]
>
> **Specific notes:**
> - [Any known data issues, e.g. "Cambridge RTT figures look unusually low"]
> - [Any trusts with missing CFO data this month]
> - [Any structural changes needed]
>
> Please update all 9 dashboard pages with the new figures. Extract the data for the 10 Shelford trusts only:
> - University Hospitals Birmingham (RRK)
> - Cambridge University Hospitals (RGT)
> - Guy's and St Thomas' (RJ1)
> - Imperial College Healthcare (RYJ)
> - King's College Hospital (RJZ)
> - Manchester University NHS Foundation Trust (R0A)
> - Newcastle Upon Tyne Hospitals (RTD)
> - Oxford University Hospitals (RTH)
> - Sheffield Teaching Hospitals (RHQ)
> - University College London Hospitals (RRV)
>
> Update all KPI boxes, trust comparison tables, bar charts, and trend lines. Keep the existing page structure and styling unchanged unless I've noted a structural change above. Output all 9 updated HTML files.

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
- The research page now shows period-on-period comparison. When updating, move the current "latest" data to "previous" and add the new data as "latest".
- If a data source changes format or URL, note this in the `notes.txt` file in the zip upload.
