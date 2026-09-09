Yes, bhai. Overview will be Section 1, and the main sections will continue in order. The seven dashboard pages will keep their own page numbers. I’ve also carried forward the earlier agreed neutral wording, around 7 PM refresh timing, and data-retention note. All other content and links are kept as supplied.

Edit

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

* How is Options Open Interest (OI) and Change in OI spread across strike prices and expiries?

* What does the Put-Call Ratio (PCR) indicate near key support and resistance zones?

* How does Futures Open Interest change with price, and does it indicate Long Buildup, Short Buildup, Long Unwinding, or Short Covering?

* How does security-wise delivery volume and delivery percentage move with cash equity prices?

---

## 3. Tech Stack

* **Power BI Desktop:** Dashboard design, layout, and visual interactions

* **Power Query:** Importing, cleaning, and appending daily NSE source files

* **DAX:** Calculating KPIs, Long/Short ratios, net contract changes, and latest-day filters

* **Data Modeling:** Relationships between participant files, Bhavcopy data, and contract details

* **Excel / CSV:** Raw source data from the National Stock Exchange of India

* **Custom Visuals:** Built custom `.pbiviz` visuals using TypeScript and D3.js (developed with the help of AI tools)

---

## 4. Data Sources

This dashboard uses four official End-of-Day reports published daily by the National Stock Exchange of India (NSE):

* **Full Bhavcopy and Security Deliverable Data (**`**sec_bhavdata_full**`**):** Contains trade volumes, deliverable quantities, and delivery percentages.

* **F&O Participant-wise Open Interest (**`**fao_participant_oi**`**):** Daily open contracts for Clients, DIIs, FIIs, and Pros across futures and options.

* **F&O FII Derivatives Statistics (**`**fii_stats**`**):** Daily buy/sell values and open contracts across index and stock derivatives.

* **F&O UDiFF Common Bhavcopy Final:** Contract-level strike prices, settlement prices, and open interest.

To keep the Power BI file size practical and performance smooth, this project uses around **one month of EOD market data from August 2026 onward**.

### [Dataset](Dataset/README.md)

> *Note: New daily EOD files are added to extend the available market history. If the dataset becomes too large or report performance is affected, older source files may be archived or removed to keep the Power BI file manageable. This may reduce the historical period available in the dashboard.*

---

## 5. Daily Refresh Workflow

* The required NSE EOD files are generally available around **7:00 PM IST**, although publication may occasionally be delayed.

* Once all the required files are available, they are downloaded and placed into their respective source folders.

* The report is refreshed in Power BI Desktop.

* Power Query combines the new day's rows with the existing historical data.

* All latest-date KPI cards, Long/Short ratios, and charts update automatically.

* The updated report is republished to Power BI Service, and the latest available trading date is verified.

> *Note: If the required NSE files are delayed, they are checked again around 7:00 AM IST the next day. The dashboard is refreshed once the required data becomes available.*

---

## 6. Why Custom Visuals Were Needed

Power BI does not come with a native candlestick chart that can easily display both price candles and market indicators (like volume, delivery percentage, or open interest) on the same synchronized date axis.

Third-party visuals in the store often had paid watermarks, slow performance, or could not align market dates properly across trading holidays. When stacking two standard charts, the dates on the top and bottom would often drift out of sync.

To solve this, five custom Power BI visual packages were designed and built using AI assistance (ChatGPT) to generate and troubleshoot the TypeScript code:

* **Candlestick by Supreet Tarwarkar:** Displays OHLC candlestick price movement with previous-day close change and volume.

* **Bar & Line by Supreet Tarwarkar:** A dual-axis visual with smooth Bar/Line toggles and synchronized crosshairs.

* **Options OI by Supreet Tarwarkar:** Displays Call and Put Open Interest and centers automatically around the nearest At-The-Money (ATM) strike price.

* **Futures OI by Supreet Tarwarkar:** Combines price movement with futures open interest bars, color-coded by market interpretation (Long Buildup, Short Buildup, Long Unwinding, Short Covering).

* **Single Candle by Supreet Tarwarkar:** A lightweight card widget to show the latest candle on the overview page.

The development process involved defining the exact market logic, testing each version inside Power BI, fixing visual alignment issues, and integrating the working builds into the dashboard.

---

## 7. Dashboard Pages

### 1. Home

* Filters for Index, Stock Symbol, F&O Symbol, and Expiry.

* Shows latest trading-day KPIs, FII net positions, and Long/Short ratios.

* High-level summary cards for the cash market, index, and derivatives.

---

### 2. Index Futures

* Candlestick and Line chart showing OHLC price and volume for index futures.

* Open Interest and Change in Open Interest placed with the price chart for comparison.

* Buildup classification showing whether moves are driven by fresh positions or covering.

---

### 3. FII Derivatives

* Dedicated page tracking Foreign Institutional Investor activity across Index Futures, Stock Futures, Calls, and Puts.

* View toggles between Net Amount (in Crores) and Net Contracts.

---

### 4. Long / Short Ratio

* Shows client-wise positioning (Client, DII, FII, Pro).

* Bar view shows absolute Long and Short open interest.

* Line view shows the Long-to-Short percentage ratio plotted against index price.

---

### 5. Options Open Interest

* Strike-wise Call OI and Put OI with Cumulative Open Interest.

* Separate visual for Change in Call/Put OI and Change in Cumulative OI.

* Range buttons to focus on $\pm 10$, $\pm 20$, $\pm 30$, $\pm 40$, or $\pm 50$ strikes from the spot close.

* Put-Call Ratio (PCR) indicator for the selected expiry.

---

### 6. Stock Futures

* Contract-level price action and Open Interest comparison for individual F&O stocks.

* Displays Long Buildup, Short Buildup, Long Unwinding, and Short Covering for single-stock contracts.

---

### 7. Stock & Delivery

* Filters for cash segment stocks with a search bar.

* Correlates daily stock price candles with deliverable volume and delivery percentage.

* Helps distinguish between intraday trading volume and genuine delivery-based buying or selling.

---

## 8. Key Features

* Price and market indicators displayed together for direct comparison on the same screen.

* Dynamic KPI cards that automatically reflect the latest trading date.

* Interactive filters for symbols, expiries, and date ranges.

* Candlestick / Line and Bar / Line switching for viewing data in different chart modes.

* Crosshair and hover details for reading chart values.

* Custom visual controls for adjusting the displayed strike range and chart spacing.

* Dark and Light theme options using bookmarks.

* Collapsible navigation sidebar for clean viewing.

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
