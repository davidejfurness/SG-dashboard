# Shelford Group NHS Trust Analytics Dashboard

A comprehensive data dashboard for monitoring performance metrics across the ten Shelford Group NHS teaching and research hospital trusts in England.

## Overview

The Shelford Group represents:
- **10 member trusts**: England's leading NHS teaching and research hospitals
- **180,000+ staff members**
- **£19 billion NHS budget**
- **20+ million annual patient contacts**
- **Two-thirds of UK's clinical research infrastructure**

## Member Trusts

| ODS Code | Trust Name |
|----------|------------|
| RGT | Cambridge University Hospitals NHS Foundation Trust |
| RJ1 | Guy's and St Thomas' NHS Foundation Trust |
| RJZ | King's College Hospital NHS Foundation Trust |
| RYJ | Imperial College Healthcare NHS Trust |
| R0A | Manchester University NHS Foundation Trust |
| RTD | The Newcastle upon Tyne Hospitals NHS Foundation Trust |
| RX1 | Nottingham University Hospitals NHS Trust |
| RTE | Oxford University Hospitals NHS Foundation Trust |
| RHQ | Sheffield Teaching Hospitals NHS Foundation Trust |
| RRV | University College London Hospitals NHS Foundation Trust |

## Features

### 📊 Performance Dashboard
- Real-time metrics across key NHS performance standards
- A&E 4-hour waiting time compliance
- RTT 18-week standard tracking
- Cancer 62-day standard monitoring
- Diagnostic 6-week standard analysis

### 🏥 Trust Comparison
- Comparative analysis across all ten trusts
- Interactive visualizations
- Trend analysis over time
- Benchmarking against national averages

### 📈 Data Visualizations
- Built with Chart.js for interactive charts
- Responsive design for all devices
- Clean, professional NHS-aligned styling
- Accessible and WCAG compliant

## Setup

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/shelford-dashboard.git
cd shelford-dashboard
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Fetch NHS Data
```bash
python fetch_data.py
```

This will:
- Create a `data/` directory
- Generate `data_sources.json` with NHS API information
- Create sample data structure in `shelford_data.json`

### 4. Deploy to GitHub Pages

#### Option A: Manual Deployment
1. Go to your repository Settings
2. Navigate to Pages section
3. Select "Deploy from a branch"
4. Choose `main` branch and `/` (root) directory
5. Save and wait for deployment

#### Option B: GitHub Actions (Automated)
The repository includes `.github/workflows/update-data.yml` which:
- Runs daily at midnight UTC
- Fetches latest NHS data
- Rebuilds the dashboard
- Commits and deploys automatically

## Data Sources

### Primary Sources
1. **NHS England Data Dashboard** (https://data.england.nhs.uk)
   - A&E waiting times
   - RTT waiting times
   - Cancer standards
   - Diagnostic waiting times

2. **NHS Digital Statistics** (https://digital.nhs.uk)
   - Monthly operational statistics
   - Workforce data
   - Trust-level performance data

3. **Organisation Data Service** (https://digital.nhs.uk/services/organisation-data-service)
   - Trust details and ODS codes
   - Organisational structure

### Data Update Frequency
- Performance metrics: Monthly (following NHS publication schedule)
- Dashboard refresh: Daily via GitHub Actions
- Manual refresh: Run `python fetch_data.py`

## Project Structure

```
shelford-dashboard/
├── index.html              # Landing page with overview cards
├── dashboard.html          # Main performance dashboard
├── trust-comparison.html   # Trust comparison page
├── ae-performance.html     # A&E detailed analysis
├── rtt-analysis.html       # RTT detailed analysis
├── cancer-standards.html   # Cancer standards tracking
├── workforce.html          # Workforce metrics
├── fetch_data.py          # Data fetching script
├── requirements.txt        # Python dependencies
├── data/
│   ├── shelford_data.json     # Current performance data
│   └── data_sources.json      # NHS data source reference
├── .github/
│   └── workflows/
│       └── update-data.yml    # Automated data refresh
└── README.md              # This file
```

## Customization

### Updating Data Sources
Edit `fetch_data.py` to implement actual NHS API calls:

```python
def fetch_nhs_data():
    # Add your API calls here
    # Example:
    response = requests.get('https://data.england.nhs.uk/api/...')
    data = response.json()
    return process_data(data)
```

### Styling
The dashboard uses CSS variables for easy theming:

```css
:root {
    --nhs-blue: #005EB8;
    --nhs-dark-blue: #003087;
    --shelford-teal: #007B7F;
    /* Modify colors here */
}
```

### Adding New Metrics
1. Update `fetch_data.py` to include new metrics
2. Add chart configuration in relevant HTML file
3. Update metric cards in dashboard

## Key Metrics Tracked

| Metric | Description | Target |
|--------|-------------|--------|
| **A&E 4-hour** | % of patients admitted/transferred/discharged within 4 hours | 95% |
| **RTT 18-week** | % of incomplete pathways within 18 weeks | 92% |
| **Cancer 62-day** | % receiving first treatment within 62 days of urgent GP referral | 85% |
| **Diagnostic 6-week** | % of patients waiting less than 6 weeks for diagnostic test | 99% |

## Technical Details

- **Frontend**: Pure HTML/CSS/JavaScript
- **Charts**: Chart.js v4.0+
- **Fonts**: DM Serif Display, Public Sans (Google Fonts)
- **Hosting**: GitHub Pages (static site)
- **Data Format**: JSON
- **Browser Support**: Modern browsers (Chrome, Firefox, Safari, Edge)

## Development

### Local Development
Simply open `index.html` in a web browser. For a local server:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`

### Testing Data Updates
```bash
python fetch_data.py
# Check data/shelford_data.json for updated values
# Refresh dashboard in browser
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-metric`)
3. Commit your changes (`git commit -am 'Add new metric tracking'`)
4. Push to the branch (`git push origin feature/new-metric`)
5. Open a Pull Request

## NHS Data Usage

This dashboard uses publicly available NHS performance data. All data remains property of NHS England and NHS Digital. Please refer to their respective data usage policies:
- [NHS England Open Data Policy](https://www.england.nhs.uk/statistics/)
- [NHS Digital Data Access Policy](https://digital.nhs.uk/data-and-information)

## License

This project is released under the MIT License. NHS data is subject to its own licensing terms.

## Support

For questions or issues:
- Open an issue on GitHub
- Contact: [your-email@example.com]
- Shelford Group website: https://shelfordgroup.org

## Acknowledgments

- NHS England for providing open data
- Shelford Group member trusts for their continued excellence
- Chart.js for visualization capabilities

---

**Last Updated**: January 2026  
**Data Source**: NHS England, NHS Digital  
**Maintained by**: [Your Name/Organisation]
