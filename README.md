# NSE Market Analysis Dashboard

## Business Questions Addressed

- How can NSE market and derivatives data be analyzed together with **candlestick price movement** instead of checking the data and price chart on separate platforms?

- What does **FII derivatives activity** indicate when compared with the movement of the underlying index?

- How are **FII, DII, Proprietary, and Client participants** positioned in terms of Long / Short activity?

- How are **Options Open Interest and Change in Open Interest** distributed across strike prices and expiries?

- What does the **Put-Call Ratio (PCR)** indicate along with the underlying price movement?

- How does **Futures Open Interest** change with price, and does the combination indicate Long Build Up, Short Build Up, Long Unwinding, or Short Covering?

- How do **stock delivery quantity and delivery percentage** behave along with stock price movement?

---

## Dashboard

### [View Interactive Power BI Dashboard](PBIX/README.md)

> This is an **End-of-Day (EOD) market analysis dashboard**, not a live or intraday streaming dashboard.

---

## Tech Stack

- **Power BI** - Dashboard development and interactive reporting
- **Power Query** - Cleaning, transforming, and combining daily NSE files
- **DAX** - KPIs, ratios, latest-date calculations, and analytical measures
- **Data Modeling** - Connecting market datasets through a common analytical model
- **Excel / CSV Files** - NSE End-of-Day source data

---

## Data Source

This project uses official **NSE End-of-Day (EOD) market reports**.

The four main NSE files used are:

1. **Full Bhavcopy and Security Deliverable Data**
2. **F&O Participant-wise Open Interest**
3. **F&O FII Derivatives Statistics**
4. **F&O UDiFF Common Bhavcopy Final**

This project uses around **one month of EOD market data from August 2026 onward** to keep the Power BI file size practical.

Detailed information about the NSE files, official source links, data period, and refresh process is available here:

### [Dataset](Dataset/README.md)

---

## Daily Refresh Workflow

1. The required NSE EOD files generally start becoming available after the trading day.
2. The latest files are usually checked between **8:00 PM and 9:00 PM IST**.
3. Once all the required files are available, they are added to the relevant source folders.
4. The Power BI report is refreshed.
5. Power Query combines the new data with the existing historical data.
6. Latest-date KPIs and visuals update automatically.

> **Note:** If the required NSE files are delayed, the dashboard is refreshed by around **7:00 AM IST the next day**, once the data becomes available.

---

## Custom Visual Development

Power BI does not include a native candlestick visual suitable for the requirements of this dashboard. Some available alternatives also had limitations such as paid access, delayed data handling, or report performance issues.

The main requirement was to **display candlestick price movement together with market data in the same analytical view**.

**AI tools, including ChatGPT, were used to generate, modify, and refine the custom Power BI visual code.** The visual code was not written manually from scratch.

The development process focused on defining the visual requirements, testing each version inside Power BI, identifying issues, refining the requirements, and integrating the working visuals into the dashboard.

### Custom Power BI Visuals Used

- **Candlestick by Supreet Tarwarkar**
- **Bar & Line by Supreet Tarwarkar**
- **Single Candle by Supreet Tarwarkar**
- **Options OI by Supreet Tarwarkar**
- **Futures OI by Supreet Tarwarkar**

These visuals are used to display price movement, Open Interest, FII activity, volume, and derivatives data within the dashboard.

The custom visuals are also planned to be made available **free of cost** for traders and Power BI users.

---

## Dashboard Pages

### 1. Home

- Selection for **Index, Stock Symbol, F&O Symbol, and Expiry**.
- Displays only the **latest available trading-day KPIs**, including FII activity and Long / Short Ratio.
- Displays the latest Index, Stock & Delivery, and Futures & Options snapshots.

![Home](Images/1.%20Home.png)

---

### 2. Index Charts

- Date range selection for the available EOD data.
- Candlestick / Line charts for **NIFTY, BANKNIFTY, and FINNIFTY**.
- Each chart displays **OHLC price data and Volume**.

![Index Charts](Images/2.%20Index%20Charts.png)

---

### 3. FII Derivatives

- Selection for **Index, FII Derivative Instrument, OI Metrics, and Date Range**.
- First visual displays the selected **Index Candlestick / Line chart**.
- **Net Amount and Net Contracts** are displayed in separate Bar / Line visuals based on the selected FII derivative instrument.

![FII Derivatives](Images/3.%20FII%20Derivatives.png)

---

### 4. Long / Short Ratio

- Selection for **Client Type, Index, and Date Range**.
- First visual displays the selected **Index Candlestick / Line chart**.
- Bar view displays **Future Index Long and Short positions**.
- Line view displays the **Long / Short Ratio in percentage (%)**.

![Long Short Ratio](Images/4.%20LS%20Ratio.png)

---

### 5. Options Open Interest

- Selection for **F&O Symbol, Expiry, and Date**, with PCR displayed for the selected data.
- First visual displays **Call and Put Open Interest** across strike prices, along with **Cumulative Open Interest**.
- Second visual displays **Change in Call and Put Open Interest**, along with **Change in Cumulative Open Interest**.
- Strike range controls are available for adjusting the displayed strike prices.

![Options Open Interest](Images/5.%20Options%20Open%20Interest.png)

---

### 6. Futures Open Interest

- Selection for **F&O Symbol, Expiry, and Date Range**.
- **Futures Open Interest and Change in Open Interest are displayed together with the selected symbol's Candlestick / Line price chart for comparison**.
- The Open Interest visual displays:
  - Long Build Up
  - Short Build Up
  - Long Unwinding
  - Short Covering

![Futures Open Interest](Images/6.%20Future%20Open%20Interest.png)

---

### 7. Stock & Delivery

- Selection for **Stock Symbol and Date Range**, with stock search available.
- First visual displays the selected **Stock Candlestick / Line chart with Volume**.
- Delivery data is displayed below the price chart for comparison with the selected stock's price movement.
- Bar view displays **Delivery Quantity**.
- Line view displays **Delivery Percentage (%)**.

![Stock and Delivery](Images/7.%20Stocks%20Delivery.png)

---

## Dashboard Features

- Dynamic latest-date KPIs
- **Dark and Light theme switching using Power BI bookmarks**
- **Collapsible and expandable sidebar using bookmark navigation**
- **Custom Candlestick / Line switching**
- **Custom Bar / Line switching**
- Historical comparison for traders as new trading-day data is added

---

## Project Walkthrough Video

A walkthrough of the complete dashboard can be viewed here:

### [Watch Project Walkthrough](PASTE_GOOGLE_DRIVE_VIDEO_LINK_HERE)

---

## Author

**Supreet Jayant Tarwarkar**

- [GitHub](https://github.com/SupreetTarwarkar)
- [LinkedIn](https://www.linkedin.com/in/supreettarwarkar/)
