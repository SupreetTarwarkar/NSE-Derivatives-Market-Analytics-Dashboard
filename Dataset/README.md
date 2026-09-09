# Dataset

This project uses **NSE End-of-Day (EOD) market data** downloaded from the official NSE report pages.

The dashboard is built for daily post-market analysis. After each trading day, the latest NSE files can be added to the existing source folders and the Power BI report can be refreshed with the new data.

---

## 1. NSE Files Used

The following four NSE reports are used in the project:

* **Full Bhavcopy and Security Deliverable Data**

  * Used for stock price, traded quantity, delivery quantity, and delivery percentage analysis.
  * **Official NSE Reports:** [NSE Reports](https://www.nseindia.com/all-reports)

* **F&O Participant-wise Open Interest**

  * Used to analyze participant positioning and Long / Short activity across FII, DII, Proprietary, and Client categories.
  * **Official NSE Derivatives Reports:** [NSE Derivatives Reports](https://www.nseindia.com/all-reports-derivatives)

* **F&O FII Derivatives Statistics**

  * Used for FII derivatives analysis such as Buy Contracts, Sell Contracts, Net Contracts, Buy / Sell Amount, and Open Interest.
  * **Official NSE Derivatives Reports:** [NSE Derivatives Reports](https://www.nseindia.com/all-reports-derivatives)

* **F&O UDiFF Common Bhavcopy Final**

  * Used for Futures and Options price, Open Interest, Change in Open Interest, expiry, strike price, and contract-level analysis.
  * **Official NSE Derivatives Reports:** [NSE Derivatives Reports](https://www.nseindia.com/all-reports-derivatives)

---

## 2. Data Period

* Around **one month of EOD market data from August 2026 onward** is used in this project.
* The shorter data period is only to keep the Power BI file size practical. The same setup can continue to take new NSE trading-day files as they become available.

> **Note:** New daily EOD files are added to extend the available market history. If the dataset becomes too large or report performance is affected, older source files may be archived or removed to keep the Power BI file manageable. This may reduce the historical period available in the dashboard.

---

## 3. Daily Refresh Workflow

* The required NSE EOD files are generally available around **7:00 PM IST**, although publication may occasionally be delayed.
* Once all the required files are available, they are downloaded from NSE.
* The new files are added to the relevant source folders.
* The Power BI Desktop report is refreshed.
* Power Query combines the new data with the existing historical data.
* Latest-date KPIs and visuals update automatically.
* The updated report is republished to **Power BI Service**, and the latest available trading date is verified.
* Historical data continues to grow as new trading-day files are added, subject to the data-retention approach described above.

> **Note:** If the required NSE files are delayed, they are checked again around **7:00 AM IST the next day**. The dashboard is refreshed once the required data becomes available.

> This is an **End-of-Day market analysis dashboard**, not a live or intraday dashboard.
