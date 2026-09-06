# Dataset

This project uses **NSE End-of-Day (EOD) market data** downloaded from the official NSE report pages.

The dashboard is designed as a **daily refresh-based market analysis project**. On each NSE trading day, the latest EOD files can be downloaded and added to the existing source folders before refreshing the Power BI report.

For the GitHub portfolio version, the dataset has been limited to approximately **one month of trading data starting from August 2026** to keep the project and Power BI file size manageable.

## NSE Files Used

The following four NSE reports are used in the project:

### 1. Full Bhavcopy and Security Deliverable Data

Used for stock price, traded quantity, delivery quantity, and delivery percentage analysis.

Official NSE Reports:  
https://www.nseindia.com/all-reports

### 2. F&O Participant-wise Open Interest

Used to analyze participant positioning and Long / Short activity across categories such as FII, DII, Proprietary, and Client.

Official NSE Derivatives Reports:  
https://www.nseindia.com/all-reports-derivatives

### 3. F&O FII Derivatives Statistics

Used for FII derivatives analysis including Buy Contracts, Sell Contracts, Net Contracts, Buy / Sell Amount, and Open Interest statistics.

Official NSE Derivatives Reports:  
https://www.nseindia.com/all-reports-derivatives

### 4. F&O UDiFF Common Bhavcopy Final

Used for Futures and Options price, Open Interest, Change in Open Interest, expiry, strike price, and contract-level analysis.

Official NSE Derivatives Reports:  
https://www.nseindia.com/all-reports-derivatives

## Data Period

The GitHub portfolio version uses approximately **one month of EOD market data from August 2026 onward**.

This limited period is used only to keep the repository and Power BI file size manageable. The dashboard architecture supports adding new NSE trading-day files over time.

## Daily Refresh Workflow

1. Download the latest EOD files from the official NSE report pages.
2. Add the new files to the relevant source folders.
3. Refresh the Power BI report.
4. Power Query combines the latest files with the existing historical data.
5. Latest-date KPIs and visuals update automatically.
6. Historical analysis expands as new trading-day data is added.

> This is an **End-of-Day market analysis dashboard**, not a live or intraday streaming dashboard.
