# NSE Market Analysis Dashboard

## 1. Overview

This is an End-of-Day (EOD) market analysis dashboard built in Power BI. It helps analyze daily National Stock Exchange (NSE) cash and derivatives data alongside candlestick price charts on a single screen, rather than checking market numbers and technical charts on separate websites or software.

The main objective of the project is to bring **candlestick price action and supporting market data together in one analytical workflow**, making it easier to compare price movement with Open Interest, FII activity, participant positioning, PCR, and delivery data.

This report is designed for post-market analysis using official daily closing files. It is not an intraday or real-time streaming dashboard.

### [View Interactive Power BI Dashboard](PBIX/README.md)

---

## 2. Business Questions Addressed

* How can daily NSE cash and derivatives figures be read alongside actual price candles without switching platforms?

* What does Foreign Institutional Investor (FII) derivatives activity suggest when compared with index price direction?

* How are Clients, DIIs, FIIs, and Proprietary desks positioned in terms of Long vs. Short exposure?

* How is Options Open Interest (OI) and Change in OI distributed across strike prices and expiries?

* What does the Put-Call Ratio (PCR) indicate alongside Call and Put Open Interest?

* How does Futures Open Interest change with price, and does it indicate Long Buildup, Short Buildup, Long Unwinding, or Short Covering?

* How do security-wise delivery quantity and delivery percentage move with cash equity prices?

---

## 3. Tech Stack

* **Power BI Desktop:** Dashboard design, layout, visual interactions, bookmarks, and report development

* **Power Query:** Importing, cleaning, transforming, and appending daily NSE source files

* **DAX:** Calculating KPIs, Long/Short positioning, PCR, Open Interest metrics, and latest-date calculations

* **Data Modeling:** Relationships between participant data, Bhavcopy data, index data, and date tables

* **CSV:** Official NSE End-of-Day source files used for the report data

* **Windows Task Scheduler:** Runs the NSE downloader at scheduled evening and morning checkpoints

* **Power BI Gateway:** Connects the local source folders to scheduled refresh in Power BI Service

* **Custom Visuals:** Custom `.pbiviz` visuals developed with TypeScript-based Power BI visual development and AI assistance

---

## 4. Data Sources

This dashboard uses five official End-of-Day reports/data files published by the National Stock Exchange of India (NSE):

* **Full Bhavcopy and Security Deliverable Data (`sec_bhavdata_full`):** Contains stock price, traded quantity, deliverable quantity, and delivery percentage data.

* **F&O Participant-wise Open Interest (`fao_participant_oi`):** Contains participant-wise Open Interest for Client, DII, FII, and Proprietary categories.

* **F&O FII Derivatives Statistics (`fii_stats`):** Contains FII Buy Contracts, Sell Contracts, Net Contracts, Buy / Sell Amount, and Open Interest data across derivative instruments.

* **F&O UDiFF Common Bhavcopy Final:** Contains contract-level Futures and Options price, Open Interest, Change in Open Interest, expiry, strike price, and related derivatives data.

* **NSE Daily Index Close (`ind_close_all`):** Used for index OHLC and related daily index data for NIFTY 50, NIFTY BANK, and NIFTY FINANCIAL SERVICES.

To keep the Power BI file size practical and performance smooth, this project uses around **one month of EOD market data from August 2026 onward**.

### [Dataset](Dataset/README.md)

> *Note: New daily EOD files are added to extend the available market history. If the dataset becomes too large or report performance is affected, older source files may be archived or removed to keep the Power BI file manageable. This may reduce the historical period available in the dashboard.*

---

## 5. Automated Download & Refresh Workflow

* The required NSE EOD files are generally available around **7:00 PM IST** on market days.

* A custom **NSE Market Data Downloader** checks the five required files and saves them into their fixed source folders. Existing valid files are not downloaded again, and weekends/configured NSE holidays are skipped.

* **Windows Task Scheduler** starts the evening download checks at **7:05 PM IST**, with retry checks at **7:15 PM, 7:45 PM, 8:15 PM, 9:45 PM, and 11:15 PM** when required files are still unavailable.

* **Power BI Service** refreshes are aligned after the download checks through the On-premises Data Gateway. The main evening refreshes run at **7:30 PM, 8:00 PM, 10:00 PM, and 11:30 PM IST**.

* Morning fallback download checks run at **5:45 AM and 7:15 AM IST**, followed by Power BI refreshes at **6:00 AM and 7:30 AM IST**. An additional **3:00 AM** service refresh is also configured as an overnight refresh checkpoint.

* Power Query combines the newly downloaded files with the existing historical data, and latest-date KPIs and visuals update automatically.

* The refreshed report is verified in Power BI Service against the latest available trading date.

> *Note: The retry workflow is dependency-based. Files that already exist and pass validation are kept; only missing or unavailable files are checked again.*

---

## 6. Why Custom Visuals Were Needed

Power BI does not include a native candlestick visual suitable for the requirements of this dashboard, especially where price movement needs to be compared directly with Volume, Open Interest, delivery data, and other market indicators.

Third-party alternatives were also tested, but some had limitations such as paid access, performance issues, or difficulty maintaining consistent date alignment between stacked market visuals.

The main requirement was to display **candlestick price movement and related market data together in the same analytical view**.

Five custom Power BI visual packages were developed with AI assistance, including ChatGPT, to generate, modify, and troubleshoot the visual code.

* **Candlestick by Supreet Tarwarkar:** Displays OHLC Candlestick / Line price movement with Volume and additional market metrics.

* **Bar & Line by Supreet Tarwarkar:** Displays market metrics using Bar / Line modes for direct comparison with price charts.

* **Options OI by Supreet Tarwarkar:** Displays Call and Put Open Interest, Change in Open Interest, ATM reference, strike-range controls, and related Options data.

* **Futures OI by Supreet Tarwarkar:** Displays Futures Open Interest and Change in Open Interest with Long Buildup, Short Buildup, Long Unwinding, and Short Covering classification.

* **Single Candle by Supreet Tarwarkar:** Displays the latest trading-day OHLC candle used on the Home page.

The development process involved defining the market requirements, testing each version inside Power BI, identifying visual and alignment issues, refining the requirements, and integrating the working builds into the dashboard.

---

## 7. Dashboard Pages

### 1. Home

* Shows the **latest available trading-day snapshot** based on the **Last Updated** date shown on the page.

* The **FII Derivatives KPI section** allows the derivative instrument to be changed and shows Buy, Sell, Net, and End-of-Day Open Interest activity.

* The **Latest Long / Short Ratio** can be viewed for FII, DII, Pro, and Client participants.

* Separate **Single Candle** visuals show the latest available Index Futures, Stock Futures, and Cash Market price snapshots.

* Related values such as Futures OI, Change in OI, OI Interpretation, PCR, Delivery Quantity, and Delivery Percentage are displayed below the respective market snapshots.

* Historical-date analysis is available on the detailed pages; the Home page is intentionally kept as a latest-day overview.

![Home](Images/1.%20Home.png)

---

### 2. Index Futures

* Select the **Index Futures symbol, Expiry, and Date Range**.

* The top visual shows **Candlestick / Line price movement with Volume**.

* The lower visual shows **Futures Open Interest and Change in Open Interest** for the same period.

* Price and OI movement are classified into **Long Buildup, Short Buildup, Short Covering, and Long Unwinding**.

* This page is mainly used to compare **index price action with futures positioning**.

![Index Futures](Images/2.%20Index%20Futures.png)

---

### 3. FII Derivatives

* Select the **Index, Derivative Instrument, Date Range, and two FII Metrics**.

* The top visual shows the selected **Index price movement**.

* Two separate Bar / Line visuals allow **any two FII metrics to be selected independently**.

* Available metrics include **Buy, Sell, Net, and End-of-Day Open Interest** in both Contracts and Amount terms.

* This page helps show **where FII derivatives activity is concentrated and how it changes alongside index price movement**.

![FII Derivatives](Images/3.%20FII%20Derivatives.png)

---

### 4. Long / Short Ratio

* Select the **Client Type, Index, and Date Range**.

* Participant types include **FII, DII, Client, and Pro**.

* The top visual shows the selected **Index price movement**.

* The Bar view shows **Future Index Long and Future Index Short positions**.

* The Line view shows the participant's **Long-position share of total Long + Short positions**.

* The report calculates this as **Long Positions ÷ (Long Positions + Short Positions)**.

* This page helps compare **participant positioning with index movement over time**.

![Long Short Ratio](Images/4.%20LS%20Ratio.png)

---

### 5. Options Open Interest

* Select the **F&O Symbol, Expiry, and Date**.

* The upper visual shows **Call and Put Open Interest across strike prices**.

* The lower visual shows **Change in Call OI and Change in Put OI**.

* **ATM** is marked on both visuals for quick reference.

* **PCR** is displayed for the selected data.

* Cumulative OI and cumulative Change in OI are shown alongside the main strike-wise visuals.

* Strike-range controls allow the view to be adjusted to **±10, ±20, ±30, ±40, or ±50 strikes around ATM**.

![Options Open Interest](Images/5.%20Options%20Open%20Interest.png)

---

### 6. Stock Futures

* Select the **Stock Futures symbol, Expiry, and Date Range**.

* The top visual shows **Candlestick / Line price movement with Volume** for the selected stock.

* The lower visual shows **Futures Open Interest and Change in Open Interest**.

* OI activity is classified into **Long Buildup, Short Buildup, Short Covering, and Long Unwinding**.

* This page applies the same **Price + OI analysis used for indices to individual F&O stocks**.

![Stock Futures](Images/6.%20Stock%20Futures.png)

---

### 7. Stock & Delivery

* Search and select the **Stock Symbol and Date Range**.

* The top visual shows **cash-market Candlestick / Line price movement with Volume**.

* The lower visual can be viewed as **Delivery Quantity** or **Delivery Percentage (%)**.

* Delivery data can be compared directly with price and traded volume.

* This page adds **delivery participation context to cash-market price movement**.

* Higher delivery alone is not treated as a direct buying or selling signal.

![Stock and Delivery](Images/7.%20Stocks%20Delivery.png)

---

## 8. Key Features

* Price and market indicators displayed together for direct comparison on the same screen.

* Dynamic KPI cards that automatically reflect the latest available trading date.

* Interactive filters for symbols, expiries, participant categories, instruments, metrics, and date ranges.

* Candlestick / Line and Bar / Line switching for viewing data in different chart modes.

* Crosshair and hover details for reading chart values.

* ATM reference and adjustable strike-range controls for Options Open Interest analysis.

* Futures Open Interest interpretation using Long Buildup, Short Buildup, Long Unwinding, and Short Covering.

* Dark and Light theme switching using Power BI bookmarks.

* Collapsible and expandable navigation sidebar using bookmarks.

* Contextual information buttons are provided wherever additional explanation is required, with metric definitions and **How to Read It** guidance across the dashboard.

* Short hover tooltips on information icons help users understand what each help button explains before opening it.

* Automated NSE file download, dependency-based retries, and scheduled Power BI Gateway refresh workflow.

* The downloader checks all five required NSE files, skips configured non-trading days, and avoids re-downloading files that already exist.

* Historical market data is extended as new daily EOD files are added.

---

## 9. Challenges & Learnings

The main development problems, debugging process, source migration, custom visual iterations, Gateway issues, bookmark management, and deployment learnings are documented separately.

### [Challenges Faced and Key Learnings](Challenges-and-Learnings/README.md)

---

## 10. Project Walkthrough Video

A full video walkthrough explaining how to read the data, navigate the pages, and use the dashboard is available here:

[Link to Walkthrough Video](https://drive.google.com/file/d/1b5joltMGyvu1zLb04pjtTNFVJI_DRRML/view)

---

## 11. Author

**Supreet Jayant Tarwarkar**

* LinkedIn: [Supreet Jayant Tarwarkar](https://www.linkedin.com/in/supreettarwarkar/)

* GitHub: [SupreetTarwarkar](https://github.com/SupreetTarwarkar)
