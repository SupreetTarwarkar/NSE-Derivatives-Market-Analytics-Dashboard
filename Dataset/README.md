# Dataset

This project uses **NSE End-of-Day (EOD) market data** downloaded from the official NSE report pages.

The dashboard is built for daily post-market analysis. After each trading day, the latest NSE files can be added to the existing source folders and the Power BI report can be refreshed with the new data.

## NSE Files Used

The following four NSE reports are used in the project:

### 1. Full Bhavcopy and Security Deliverable Data

Used for stock price, traded quantity, delivery quantity, and delivery percentage analysis.

Official NSE Reports:  
https://www.nseindia.com/all-reports

### 2. F&O Participant-wise Open Interest

Used to analyze participant positioning and Long / Short activity across FII, DII, Proprietary, and Client categories.

Official NSE Derivatives Reports:  
https://www.nseindia.com/all-reports-derivatives

### 3. F&O FII Derivatives Statistics

Used for FII derivatives analysis such as Buy Contracts, Sell Contracts, Net Contracts, Buy / Sell Amount, and Open Interest.

Official NSE Derivatives Reports:  
https://www.nseindia.com/all-reports-derivatives

### 4. F&O UDiFF Common Bhavcopy Final

Used for Futures and Options price, Open Interest, Change in Open Interest, expiry, strike price, and contract-level analysis.

Official NSE Derivatives Reports:  
https://www.nseindia.com/all-reports-derivatives

## Data Period

For this project, I have used around **one month of EOD market data from August 2026 onward**.

The shorter data period is only to keep the Power BI file size practical. The same setup can continue to take new NSE trading-day files as they become available.

## Daily Refresh Workflow

1. Download the latest EOD files from NSE after the trading day.
2. Add the new files to the relevant source folders.
3. Refresh the Power BI report.
4. Power Query combines the new data with the existing data.
5. Latest-date KPIs and visuals update automatically.
6. Historical data continues to grow with each new trading day.

> This is an **End-of-Day market analysis dashboard**, not a live or intraday dashboard.
