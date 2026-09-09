# NSE Market Analysis Dashboard

## Overview

This is an End-of-Day (EOD) market analysis dashboard built in Power BI. It helps analyze daily National Stock Exchange (NSE) cash and derivatives data alongside candlestick price charts on a single screen, rather than checking market numbers and technical charts on separate websites or software.

This report is designed for post-market analysis using official daily closing files. It is not an intraday or real-time streaming dashboard.

### [View Interactive Power BI Dashboard](PBIX/README.md)

## Business Questions Addressed

• How can daily NSE cash and derivatives figures be read alongside actual price candles without switching platforms?
• What does Foreign Institutional Investor (FII) derivatives activity suggest when compared with index price direction?
• How are Clients, DIIs, FIIs, and Proprietary desks positioned in terms of Long vs. Short contracts?
• How is Options Open Interest (OI) and Change in OI spread across strike prices and expiries?
• What does the Put-Call Ratio (PCR) indicate near key support and resistance zones?
• How does Futures Open Interest change with price, and does it indicate Long Buildup, Short Buildup, Long Unwinding, or Short Covering?
• How does security-wise delivery volume and delivery percentage move with cash equity prices?

## Tech Stack

• **Power BI Desktop:** Dashboard design, layout, and visual interactions
• **Power Query:** Importing, cleaning, and appending daily NSE source files
• **DAX:** Calculating KPIs, Long/Short ratios, net contract changes, and latest-day filters
• **Data Modeling:** Relationships between participant files, Bhavcopy data, and contract details
• **Excel / CSV:** Raw source data from the National Stock Exchange of India
• **Custom Visuals:** Built custom `.pbiviz` visuals using TypeScript and D3.js (developed with the help of AI tools)

## Data Sources

This dashboard uses four official End-of-Day reports published daily by the National Stock Exchange of India (NSE):

1. **Full Bhavcopy and Security Deliverable Data (`sec_bhavdata_full`):** Contains trade volumes, deliverable quantities, and delivery percentages.
2. **F&O Participant-wise Open Interest (`fao_participant_oi`):** Daily open contracts for Clients, DIIs, FIIs, and Pros across futures and options.
3. **F&O FII Derivatives Statistics (`fii_stats`):** Daily buy/sell values and open contracts across index and stock derivatives.
4. **F&O UDiFF Common Bhavcopy Final:** Contract-level strike prices, settlement prices, and open interest.

To keep the Power BI file size practical and performance smooth, this project uses a rolling window of market data from August 2026 onward.

### [Dataset](Dataset/README.md)

## Daily Refresh Workflow

1. The required NSE files are released after market hours, usually checked between 8:00 PM and 9:00 PM IST.
2. Downloaded CSV and Excel files are placed into their respective source folders.
3. The report is refreshed in Power BI Desktop.
4. Power Query combines the new day's rows with the existing historical data.
5. All latest-date KPI cards, Long/Short ratios, and charts update automatically.
6. The updated workbook is republished to Power BI Service.

*Note: If the exchange delays file publishing in the evening, the files are checked again around 7:00 AM IST the next morning before market open, and the report is refreshed then.*

## Why Custom Visuals Were Needed

Power BI does not come with a native candlestick chart that can easily display both price candles and market indicators (like volume, delivery percentage, or open interest) on the same synchronized date axis.

Third-party visuals in the store often had paid watermarks, slow performance, or could not align market dates properly across trading holidays. When stacking two standard charts, the dates on the top and bottom would often drift out of sync.

To solve this, I designed and built five custom Power BI visual packages using AI assistance (ChatGPT) to generate and troubleshoot the TypeScript code:

• **Candlestick by Supreet Tarwarkar:** Displays OHLC candlestick price movement with previous-day close change and volume.
• **Bar & Line by Supreet Tarwarkar:** A dual-axis visual with smooth Bar/Line toggles and synchronized crosshairs.
• **Options OI by Supreet Tarwarkar:** Displays Call and Put Open Interest and centers automatically around the nearest At-The-Money (ATM) strike price.
• **Futures OI by Supreet Tarwarkar:** Combines price movement with futures open interest bars, color-coded by market interpretation (Long Buildup, Short Buildup, Long Unwinding, Short Covering).
• **Single Candle by Supreet Tarwarkar:** A lightweight card widget to show the latest candle on the overview page.

My role was defining the exact market logic, testing each version inside Power BI, fixing visual alignment issues, and integrating the working builds into the dashboard.

## Dashboard Pages

### 1. Home

• Filters for Index, Stock Symbol, F&O Symbol, and Expiry.
• Shows latest trading-day KPIs, FII net positions, and Long/Short ratios.
• High-level summary cards for the cash market, index, and derivatives.

![Home](Images/1.%20Home.png)

### 2. Index Futures

• Candlestick and Line chart showing OHLC price and volume for index futures.
• Open Interest and Change in Open Interest placed with the price chart for comparison.
• Buildup classification showing whether moves are driven by fresh positions or covering.

![Index Futures](Images/2.%20Index%20Charts.png)

### 3. FII Derivatives

• Dedicated page tracking Foreign Institutional Investor activity across Index Futures, Stock Futures, Calls, and Puts.
• View toggles between Net Amount (in Crores) and Net Contracts.

![FII Derivatives](Images/3.%20FII%20Derivatives.png)

### 4. Long / Short Ratio

• Shows client-wise positioning (Client, DII, FII, Pro).
• Bar view shows absolute Long and Short open interest.
• Line view shows the Long-to-Short percentage ratio plotted against index price.

![Long Short Ratio](Images/4.%20LS%20Ratio.png)

### 5. Options Open Interest

• Strike-wise Call OI and Put OI with Cumulative Open Interest.
• Separate visual for Change in Call/Put OI and Change in Cumulative OI.
• Range buttons to focus on $\pm 10$, $\pm 20$, $\pm 30$, $\pm 40$, or $\pm 50$ strikes from the spot close.
• Put-Call Ratio (PCR) indicator for the selected expiry.

![Options Open Interest](Images/5.%20Options%20Open%20Interest.png)

### 6. Stock Futures

• Contract-level price action and Open Interest comparison for individual F&O stocks.
• Displays Long Buildup, Short Buildup, Long Unwinding, and Short Covering for single-stock contracts.

![Stock Futures](Images/6.%20Future%20Open%20Interest.png)

### 7. Stock & Delivery

• Filters for cash segment stocks with a search bar.
• Correlates daily stock price candles with deliverable volume and delivery percentage.
• Helps distinguish between intraday trading volume and genuine delivery-based buying or selling.

![Stock and Delivery](Images/7.%20Stocks%20Delivery.png)

## Key Features

• Dynamic KPI cards that automatically reflect the latest trading date.
• Dark and Light theme options using bookmarks.
• Collapsible navigation sidebar for clean viewing.
• In-visual mode switching between bars and lines.
• Custom visual controls for strike range and axis headroom.

## Project Walkthrough Video

A full video walkthrough explaining how to read the data, navigate the pages, and use the dashboard is available here:

[Link to Walkthrough Video](PASTE_GOOGLE_DRIVE_VIDEO_LINK_HERE)

## Author

**Supreet Jayant Tarwarkar**

• LinkedIn: [Supreet Jayant Tarwarkar](https://www.linkedin.com/in/supreettarwarkar/)
• GitHub: [SupreetTarwarkar](https://github.com/SupreetTarwarkar)
