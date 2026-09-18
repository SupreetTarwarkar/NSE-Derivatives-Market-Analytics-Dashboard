# Dataset

This project uses **NSE End-of-Day (EOD) market data** downloaded from the official NSE report pages.

The dashboard is built for daily post-market analysis. A custom NSE downloader and scheduled tasks are used to collect the latest market-day files into the existing source folders before the Power BI Service refresh runs through the Gateway.

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

## 3. Automated Download & Refresh Workflow

* The required NSE EOD files are generally available around **7:00 PM IST** on market days.
* The **NSE Market Data Downloader** checks the five required datasets and saves available files into their fixed source folders.
* Existing valid files are kept and are not downloaded again. Weekends and configured NSE holidays are skipped.
* Evening checks start at **7:05 PM IST**. Retry checks run at **7:15 PM, 7:45 PM, 8:15 PM, 9:45 PM, and 11:15 PM** only when required files are still missing.
* Power BI Service refreshes are scheduled at **7:30 PM, 8:00 PM, 10:00 PM, and 11:30 PM IST** so refreshes run after the corresponding evening download checks.
* Morning fallback checks run at **5:45 AM and 7:15 AM IST**, followed by Power BI refreshes at **6:00 AM and 7:30 AM IST**. A **3:00 AM** refresh is also configured as an overnight checkpoint.
* Power Query combines the new files with the existing historical data.
* Latest-date KPIs and visuals update automatically, and the refreshed report is verified in **Power BI Service**.
* Historical data continues to grow as new trading-day files are added, subject to the data-retention approach described above.

> **Note:** The retry process is dependency-based. Only missing or unavailable files are checked again; files already downloaded successfully are left unchanged.

> This is an **End-of-Day market analysis dashboard**, not a live or intraday dashboard.
