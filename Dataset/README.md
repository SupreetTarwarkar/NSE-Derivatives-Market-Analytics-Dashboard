# Dataset

This project uses **NSE End-of-Day (EOD) market data** downloaded from the official NSE report pages.

The dashboard is built for daily post-market analysis. After each trading day, the latest NSE files can be added to the existing source folders and the Power BI report can be refreshed with the new data.

---

## 1. NSE Files Used

The following five NSE reports/data files are used in the project:

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

* **NSE Daily Index Close (`ind_close_all`)**

  * Used for daily Index OHLC and related Index data for NIFTY 50, NIFTY BANK, and NIFTY FINANCIAL SERVICES.
  * This replaced the earlier Excel STOCKHISTORY-based Index source after it stopped returning the latest trading-day data.
  * **Official NSE Reports:** [NSE Reports](https://www.nseindia.com/all-reports)

---

## 2. Data Period

* Around **one month of EOD market data from August 2026 onward** is used in this project.
* The shorter data period is only to keep the Power BI file size practical. The same setup can continue to take new NSE trading-day files as they become available.

> **Note:** New daily EOD files are added to extend the available market history. If the dataset becomes too large or report performance is affected, older source files may be archived or removed to keep the Power BI file manageable. This may reduce the historical period available in the dashboard.

---

## 3. Daily Refresh Workflow

* The required NSE EOD files are generally available around **7:00 PM IST**.
* Once the required files are available, they are downloaded from NSE and added to the relevant source folders.
* The dashboard refresh is scheduled around **8:00 PM IST** after the evening NSE files are available.
* Power Query combines the new data with the existing historical data.
* Latest-date KPIs and visuals update automatically.
* The refreshed report is verified in **Power BI Service** against the latest available trading date.
* Historical data continues to grow as new trading-day files are added, subject to the data-retention approach described above.

> **Note:** If any required NSE file is delayed in the evening, the data is checked again around **7:00 AM IST the next morning** and the dashboard is refreshed once the missing file becomes available.

> This is an **End-of-Day market analysis dashboard**, not a live or intraday dashboard.
