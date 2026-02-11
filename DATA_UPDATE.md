# Dashboard Update - Real NHS Data Integration

## Data Source
All performance metrics now use **real NHS data** extracted from the NHS England Acute Provider Table:
- **Source**: https://data.england.nhs.uk/providers/acute-provider-table
- **A&E Data**: November 2025 (provisional)
- **Other Metrics** (RTT, Cancer, Diagnostics): October 2025

## Shelford Group Performance Summary

### Group Averages (Latest Month)
- **A&E 4-hour Standard**: 73.1% (vs 95% target)
- **RTT 18-week Standard**: 62.1% (vs 92% target)
- **Cancer 62-day Standard**: 63.5% (vs 85% target)
- **Diagnostic <6 weeks**: 78.1% (vs 99% target)

### Trust Rankings (Out of 118 NHS Trusts)
Best performing Shelford trusts:
- **Newcastle** (RTT Rank #7, A&E Rank #34)
- **Sheffield** (RTT Rank #25, but Cancer Rank #117)
- **Guy's & St Thomas'** (A&E Rank #15, but Cancer Rank #115)

Areas of concern:
- Manchester RTT performance (Rank #110)
- Sheffield Cancer 62-day (Rank #117 - only 42.8%)
- King's diagnostic waiting times (46.8% over 6 weeks)

## Key Insights

1. **A&E Performance**: Shelford Group average (73.1%) is slightly below national average (73.5%), significantly below the 95% target

2. **RTT Performance**: Wide variation across trusts - Newcastle at 73.5% vs Manchester at 53.8%

3. **Cancer Performance**: Concerning variation - UCLH at 78.5% vs Sheffield at 42.8%

4. **Best Overall**: Newcastle Upon Tyne Hospitals shows strongest balanced performance

5. **National Context**: All Shelford trusts are ranked out of 118 acute providers nationally

## Data Quality Notes
- Sheffield Teaching Hospitals RTT data for Jul-Oct 2025 includes estimates due to reported data quality issues
- All data sourced from official NHS England publications
- Rankings reflect performance against all NHS acute trusts in England

## Future Enhancements
- Implement automated data fetching from NHS APIs
- Add historical trend analysis
- Include workforce and financial metrics
- Set up automated monthly updates via GitHub Actions

---
**Generated**: January 13, 2026
**Data Period**: October-November 2025
**Next Update**: February 2026 (following NHS monthly publication schedule)
