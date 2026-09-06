# Dataset

This project uses **NSE End-of-Day (EOD) market data** that is updated on each trading day.

The dataset is not treated as a fixed historical snapshot. New daily market files are downloaded, added to the existing source folders, and the Power BI report is refreshed so the latest KPIs update while the historical dataset continues to grow.

## Official NSE Data Sources

The project uses data downloaded from the following official NSE report pages:

- **NSE Derivatives Reports**  
  https://www.nseindia.com/all-reports-derivatives

- **NSE All Reports**  
  https://www.nseindia.com/all-reports

## Data Categories Used

The Power BI model uses market data covering:

- Index spot prices
- FII derivatives statistics
- Participant-wise Open Interest
- Stock delivery data
- NSE derivatives Bhavcopy
- Futures and Options expiry information
- OHLC price data
- Open Interest
- Change in Open Interest

## Daily Refresh Workflow

For each NSE trading day:

1. Download the latest EOD market files from the NSE report pages.
2. Add the new files to the relevant source folders.
3. Refresh the Power BI report.
4. Power Query combines the new files with the existing historical data.
5. Latest-date KPIs update automatically.
6. Historical analysis expands as new trading-day data is added.

> This dashboard is designed for **post-market EOD analysis** and is not a live or intraday streaming dashboard.
