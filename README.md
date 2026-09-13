# NSE Market Analysis Dashboard

## 1. Overview

This is an End-of-Day (EOD) market analysis dashboard built in Power BI. It helps analyze daily National Stock Exchange (NSE) cash and derivatives data alongside candlestick price charts on a single screen, rather than checking market numbers and technical charts on separate websites or software.

This report is designed for post-market analysis using official daily closing files. It is not an intraday or real-time streaming dashboard.

### [View Interactive Power BI Dashboard](PBIX/README.md)

---

## 2. Business Questions Addressed

* How can daily NSE cash and derivatives figures be read alongside actual price candles without switching platforms?

* What does Foreign Institutional Investor (FII) derivatives activity suggest when compared with index price direction?

* How are Clients, DIIs, FIIs, and Proprietary desks positioned in terms of Long vs. Short contracts?

* How is Options Open Interest (OI) and Change in OI distributed across strike prices and expiries?

* What does the Put-Call Ratio (PCR) indicate alongside Call and Put Open Interest?

* How does Futures Open Interest change with price, and does it indicate Long Buildup, Short Buildup, Long Unwinding, or Short Covering?

* How do security-wise delivery quantity and delivery percentage move with cash equity prices?

---

## 3. Tech Stack

* **Power BI Desktop:** Dashboard design, layout, visual interactions, bookmarks, and report development

* **Power Query:** Importing, cleaning, transforming, and appending daily NSE source files

* **DAX:** Calculating KPIs, Long/Short ratios, PCR, Open Interest metrics, and latest-date calculations

* **Data Modeling:** Relationships between participant data, Bhavcopy data, index data, and date tables

* **Excel / CSV:** Raw End-of-Day source data from the National Stock Exchange of India

* **Custom Visuals:** Custom `.pbiviz` visuals developed with TypeScript-based Power BI visual development and AI assistance

---

## 4. Data Sources

This dashboard uses four official End-of-Day reports published daily by the National Stock Exchange of India (NSE):

* **Full Bhavcopy and Security Deliverable Data (`sec_bhavdata_full`):** Contains stock price, traded quantity, deliverable quantity, and delivery percentage data.

* **F&O Participant-wise Open Interest (`fao_participant_oi`):** Contains participant-wise Open Interest for Client, DII, FII, and Proprietary categories.

* **F&O FII Derivatives Statistics (`fii_stats`):** Contains FII Buy Contracts, Sell Contracts, Net Contracts, Buy / Sell Amount, and Open Interest data across derivative instruments.

* **F&O UDiFF Common Bhavcopy Final:** Contains contract-level Futures and Options price, Open Interest, Change in Open Interest, expiry, strike price, and related derivatives data.

To keep the Power BI file size practical and performance smooth, this project uses around **one month of EOD market data from August 2026 onward**.

### [Dataset](Dataset/README.md)

> *Note: New daily EOD files are added to extend the available market history. If the dataset becomes too large or report performance is affected, older source files may be archived or removed to keep the Power BI file manageable. This may reduce the historical period available in the dashboard.*

---

## 5. Daily Refresh Workflow

* The required NSE EOD files are generally available around **7:00 PM IST**, although publication may occasionally be delayed.

* Once all the required files are available, they are downloaded and placed into their respective source folders.

* The report is refreshed in Power BI Desktop.

* Power Query combines the new data with the existing historical data.

* Latest-date KPI cards and visuals update with the newly added trading-day data.

* The updated report is republished to Power BI Service, and the latest available trading date is verified.

> *Note: If the required NSE files are delayed, they are checked again around **7:00 AM IST the next day**. The dashboard is refreshed once the required data becomes available.*

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

* **Single Candle by Supreet Tarwarkar:** Displays the latest trading-day OHLC candle used on the Overview page.

The development process involved defining the market requirements, testing each version inside Power BI, identifying visual and alignment issues, refining the requirements, and integrating the working builds into the dashboard.

---

## 7. Dashboard Pages

### 1. Home

* Filters for **Index Futures, Index Expiry, Stock Futures, Stock Expiry, Cash Market Symbol, FII Derivative Instrument, and Participant Type**.

* Displays the latest available trading-day FII KPIs including Buy Contracts, Buy Amount, Sell Contracts, Sell Amount, Net Contracts, Net Amount, EOD OI Contracts, and EOD OI Amount.

* Displays the latest Long / Short Ratio for the selected participant type.

* Displays latest Index Futures, Stock Futures, and Cash Market price snapshots using Single Candle visuals.

* Displays related Futures Open Interest, Change in Futures Open Interest, OI Interpretation, PCR, Delivery Quantity, and Delivery Percentage values.

![Home](Images/1.%20Home.png)

---

### 2. Index Futures

* Filters for **Index Futures Symbol, Expiry, and Date Range**.

* Candlestick / Line chart displays OHLC price movement and Volume for the selected index futures contract.

* Futures Open Interest and Change in Open Interest are displayed together with the price chart for direct comparison.

* OI Interpretation classifies the selected futures movement as **Long Buildup, Short Buildup, Long Unwinding, or Short Covering**.

![Index Futures](Images/2.%20Index%20Futures.png)

---

### 3. FII Derivatives

* Filters for **Index, FII Derivative Instrument, Metrics, and Date Range**.

* Displays the selected Index Candlestick / Line price chart.

* Two Bar / Line analytical visuals allow different FII metrics to be compared with the selected index price movement.

* Available FII analysis includes Buy, Sell, Net, and End-of-Day Open Interest data across Contracts and Amount-based metrics.

![FII Derivatives](Images/3.%20FII%20Derivatives.png)

---

### 4. Long / Short Ratio

* Filters for **Client Type, Index, and Date Range**.

* Displays the selected Index Candlestick / Line price chart.

* Bar view displays **Future Index Long and Future Index Short positions**.

* Line view displays the **Long / Short Ratio in percentage (%)** for the selected participant category.

* Participant categories include **Client, DII, FII, and Proprietary**.

![Long Short Ratio](Images/4.%20LS%20Ratio.png)

---

### 5. Options Open Interest

* Filters for **F&O Symbol, Expiry, and Date**.

* Displays **Call Open Interest and Put Open Interest** across strike prices.

* Displays separate **Change in Call Open Interest and Change in Put Open Interest** analysis.

* Cumulative Call and Put Open Interest are displayed alongside the strike-wise charts.

* ATM reference is displayed on both Open Interest visuals.

* Strike-range controls allow the displayed range to be adjusted to **±10, ±20, ±30, ±40, or ±50 strikes around ATM**.

* Put-Call Ratio (PCR) is displayed for the selected data.

![Options Open Interest](Images/5.%20Options%20Open%20Interest.png)

---

### 6. Stock Futures

* Filters for **Stock Futures Symbol, Expiry, and Date Range**.

* Displays the selected Stock Futures Candlestick / Line price chart with Volume.

* Futures Open Interest and Change in Open Interest are displayed with the selected stock futures price for comparison.

* OI Interpretation classifies the selected stock futures movement as **Long Buildup, Short Buildup, Long Unwinding, or Short Covering**.

* This page is dedicated to **individual F&O stock futures**, while index futures are analyzed separately on the Index Futures page.

![Stock Futures](Images/6.%20Stock%20Futures.png)

---

### 7. Stock & Delivery

* Filters for **Stock Symbol and Date Range**, with stock search available.

* Displays the selected cash-market Stock Candlestick / Line chart with Volume.

* Delivery data is displayed below the price chart for direct comparison with price movement.

* Bar view displays **Delivery Quantity**.

* Line view displays **Delivery Percentage (%)**.

* Delivery data helps evaluate the level of delivery-based participation alongside price and traded volume; it does not by itself indicate buying or selling direction.

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

* Contextual information buttons with metric definitions and **How to Read It** guidance across the dashboard.

* Historical market data is extended as new daily EOD files are added.

---

## 9. Project Walkthrough Video

A full video walkthrough explaining how to read the data, navigate the pages, and use the dashboard is available here:

[Link to Walkthrough Video](PASTE_GOOGLE_DRIVE_VIDEO_LINK_HERE)

---

## 10. Author

**Supreet Jayant Tarwarkar**

* LinkedIn: [Supreet Jayant Tarwarkar](https://www.linkedin.com/in/supreettarwarkar/)

* GitHub: [SupreetTarwarkar](https://github.com/SupreetTarwarkar)
