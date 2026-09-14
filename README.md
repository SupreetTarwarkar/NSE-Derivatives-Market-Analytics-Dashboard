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

The Home page is designed as a **latest available trading-day snapshot**, based on the **Last Updated** date shown on the report. It brings together three areas on one screen:

* **FII Derivatives KPIs:** The derivative instrument can be changed to analyse Buy, Sell, Net, and End-of-Day Open Interest activity across the latest available data.

* **Latest Long / Short Ratio:** The participant type can be switched between FII, DII, Pro, and Client to understand how each group is positioned.

* **Latest market snapshots:** Separate Single Candle visuals show the latest available Index Futures, Stock Futures, and Cash Market price action. Related values such as Futures OI, Change in OI, OI Interpretation, PCR, Delivery Quantity, and Delivery Percentage are displayed below.

The Home page is intentionally a latest-day overview; historical-date analysis is available on the detailed pages.

![Home](Images/1.%20Home.png)

---

### 2. Index Futures

This page compares **Index Futures price movement and Volume with Futures Open Interest** over a selected date range. Users can choose the Index Futures symbol and expiry, then analyse how price and OI move together.

The lower visual classifies the Price + OI combination into **Long Buildup, Short Buildup, Short Covering, and Long Unwinding**, making it easier to understand how futures positioning changes alongside price.

![Index Futures](Images/2.%20Index%20Futures.png)

---

### 3. FII Derivatives

This page analyses **FII derivatives activity alongside index price movement**. Users can select the Index, derivative instrument, date range, and independently choose **two FII metrics** for comparison.

Available metrics include Buy, Sell, Net, and End-of-Day Open Interest in both **Contracts and Amount** terms, allowing the two selected series to be compared with each other and with the index price trend over the same period.

![FII Derivatives](Images/3.%20FII%20Derivatives.png)

---

### 4. Long / Short Ratio

This page shows how **FII, DII, Client, and Pro participants are positioned across selected indices**. Users can change the participant type, index, and date range, then compare changes in positioning with index price movement.

The Bar view displays **Future Index Long and Future Index Short positions**, while the Line view displays the participant's **Long-position share of total Long + Short positions**.

The report calculates this as:

**Long Positions ÷ (Long Positions + Short Positions)**

![Long Short Ratio](Images/4.%20LS%20Ratio.png)

---

### 5. Options Open Interest

This page analyses **Call and Put Open Interest across strike prices** for the selected symbol, expiry, and date.

It includes **Open Interest, Change in Open Interest, PCR, ATM reference, cumulative OI views, and adjustable strike ranges around ATM**. The strike-range controls can be changed to **±10, ±20, ±30, ±40, or ±50 strikes**, helping users move from a focused ATM view to a broader options-market view.

![Options Open Interest](Images/5.%20Options%20Open%20Interest.png)

---

### 6. Stock Futures

This page applies **Price + Open Interest analysis to individual F&O stocks**. Users can select the Stock Futures symbol, expiry, and date range, then compare candlestick price movement and Volume with Futures Open Interest.

The OI visual classifies the selected stock's activity into **Long Buildup, Short Buildup, Short Covering, and Long Unwinding**, helping identify whether positions are being built or closed as price changes.

![Stock Futures](Images/6.%20Stock%20Futures.png)

---

### 7. Stock & Delivery

This page combines **cash-market stock price movement with Volume and Delivery data**. Users can search and select a stock and date range, then compare price action with delivery participation.

The Bar view displays **Delivery Quantity**, while the Line view displays **Delivery Percentage (%)**. This adds context to price and traded volume, while avoiding the assumption that higher delivery alone indicates buying or selling direction.

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

* Short hover tooltips on information icons help users understand what each help button explains before opening it.

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
