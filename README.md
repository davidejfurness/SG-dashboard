# Shelford Group Performance Dashboard

A data dashboard for the Shelford Group, a collaboration of ten major NHS teaching and research hospital trusts in England. The dashboard brings together published NHS performance data and internal Shelford Group data to provide a single view of trust-level performance across operational, workforce, financial and research domains.

## Access

The dashboard is password-protected. Contact info@shelfordgroup.org for the access code.

## Dashboard Pages

| Page | Content | Primary Data Sources |
|------|---------|---------------------|
| **Overview** | KPI summary, trust comparison table, NHS Oversight Framework segmentation with domain heatmap, radar chart and key metric benchmarking | NHS England monthly statistics; NHS Oversight Framework Q2 2025/26 |
| **RTT & Elective Care** | 18-week and 52-week waiting times, trends, trust comparison | NHS England RTT statistics (monthly) |
| **A&E & Urgent Care** | 4-hour and 12-hour performance, type 1 attendances, Friends & Family Test | NHS England A&E statistics (monthly); FFT data |
| **Cancer Services** | 62-day standard, Faster Diagnosis Standard (28-day), trust trends | NHS England cancer waiting times (monthly) |
| **Patient Safety & Quality** | Friends & Family Test (A&E and inpatient), response rates | NHS England FFT data (monthly) |
| **Capacity & Beds** | General & acute beds, occupancy rates, critical care | NHS England bed availability and occupancy (monthly) |
| **Workforce** | Vacancy rates, sickness absence, NHS Staff Survey results, People Promise scores | NHS Digital workforce statistics; NHS Staff Survey (annual) |
| **Research & Clinical Trials** | 90-day trial setup performance by trust | NIHR Open Data Platform |
| **Productivity & Finance** | NHS England productivity growth estimates (output vs input); in-year financial position (surplus/deficit, CIP delivery) | NHS England Productivity Growth Estimates; Shelford CFO Monthly Updates (internal) |

## Data Sources

Most data is drawn from publicly available NHS England publications, typically released around the 12th of each month. The main sources are:

- **NHS England Statistical Work Areas** — RTT, A&E, cancer, beds, diagnostics
- **NHS England Friends & Family Test** — patient experience data (xlsm files)
- **NHS Oversight Framework** — quarterly segmentation and domain scores
- **NHS England Productivity Growth Estimates** — trust-level productivity (new measure, first published February 2026)
- **NHS Staff Survey** — annual, published around March each year
- **NIHR Open Data Platform** — research and clinical trials

**Internal data (not publicly available):**

- **Shelford CFO Monthly Updates** — in-year financial position and CIP delivery, shared monthly by member trust CFOs. This data appears on the Productivity & Finance page and should be treated as confidential to the Shelford Group.

## Updating the Dashboard

The dashboard is updated manually, typically once a month after NHS England publishes new data. See `DASHBOARD-UPDATE-GUIDE.md` for the full step-by-step process, including which files to download, the prompt template for generating updates, and the property name conventions used in the JavaScript.

## Member Trusts

| Short Name | Full Name |
|------------|-----------|
| Birmingham | University Hospitals Birmingham NHS Foundation Trust |
| Cambridge | Cambridge University Hospitals NHS Foundation Trust |
| GSTT | Guy's and St Thomas' NHS Foundation Trust |
| Imperial | Imperial College Healthcare NHS Trust |
| King's | King's College Hospital NHS Foundation Trust |
| Manchester | Manchester University NHS Foundation Trust |
| Newcastle | The Newcastle upon Tyne Hospitals NHS Foundation Trust |
| Oxford | Oxford University Hospitals NHS Foundation Trust |
| Sheffield | Sheffield Teaching Hospitals NHS Foundation Trust |
| UCLH | University College London Hospitals NHS Foundation Trust |

## Technical Details

- Pure HTML, CSS and JavaScript — no build step or server required
- Charts built with Chart.js 4.x (loaded from CDN)
- Hosted on GitHub Pages
- Client-side passphrase protection (SHA-256 hashed, cookie-based, 365-day expiry)

## Project Structure

```
SG-Dashboard/
├── index.html                  # Overview page with KPIs, trust table, NOF analysis
├── rtt-detail.html             # RTT & Elective Care
├── ae-detail.html              # A&E & Urgent Care
├── cancer-detail.html          # Cancer Services
├── quality-detail.html         # Patient Safety & Quality
├── capacity-detail.html        # Capacity & Beds
├── workforce-detail.html       # Workforce
├── research-detail.html        # Research & Clinical Trials
├── productivity-detail.html    # Productivity & Finance
├── shelford-logo.jpg           # Shelford Group logo
├── DASHBOARD-UPDATE-GUIDE.md   # Monthly update instructions
└── README.md                   # This file
```

## Contact

Shelford Group — info@shelfordgroup.org — https://shelfordgroup.org

---

**Last updated:** February 2026
**Data period:** Up to October 2025 (operational); December 2025 / M9 (financial)
