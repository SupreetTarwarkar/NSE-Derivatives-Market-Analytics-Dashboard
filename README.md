# NSE Market Analysis Dashboard

## Business Questions Addressed

- How can NSE market and derivatives data be analyzed together with **candlestick price movement** instead of checking the data and price chart on separate platforms?

- What does **FII derivatives activity** indicate when compared with the movement of the underlying index?

- How are **FII, DII, Proprietary, and Client participants** positioned in terms of Long / Short activity?

- How are **Options Open Interest and Change in Open Interest** distributed across strike prices and expiries?

- What does the **Put-Call Ratio (PCR)** indicate along with the underlying price movement?

- How does **Futures Open Interest** change with price, and does the combination indicate Long Build Up, Short Build Up, Long Unwinding, or Short Covering?

- How do **stock delivery quantity and delivery percentage** behave along with stock price movement?

- Can these different NSE EOD datasets be brought into **one dashboard** for easier post-market comparison and analysis?

---

## Live Dashboard

### [View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiOGViNzk2OWMtMGRjNC00OGRlLWE5N2UtZGFiOGU5YWE5NjRjIiwidCI6ImRmODY3OWNkLWE4MGUtNDVkOC05OWFjLWM4M2VkN2ZmOTVhMCJ9)

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

For this project, I have used around **one month of EOD market data from August 2026 onward** to keep the Power BI file size practical.

Detailed information about the NSE files, official source links, data period, and refresh process is available here:

### [Dataset Documentation](Dataset/README.md)

---

## Daily Refresh Workflow

1. Download the latest EOD files from NSE after the trading day.
2. Add the new files to the relevant source folders.
3. Refresh the Power BI report.
4. Power Query combines the new data with the existing data.
5. Latest-date KPIs and visuals update automatically.
6. Previous trading-day data remains available for historical analysis.

---

## Custom Visual Development

Power BI does not include a native candlestick visual that matched the way I wanted to analyze the NSE data. In my testing, the alternatives I tried had limitations such as paid access, delayed data handling, or report performance issues.

My main requirement was simple: **show candlestick price movement together with market data so both can be analyzed in the same view.**

I used **AI tools, including ChatGPT, to generate, modify, and refine the custom Power BI visual code based on my requirements**.

I did not write the custom visual code from scratch myself. My role was to define what the visuals should do, test each version inside Power BI, identify problems, refine the requirements, and integrate the working visuals into the dashboard.

### Custom Power BI Visuals Used

- **Candlestick by Supreet Tarwarkar**
- **Bar & Line by Supreet Tarwarkar**
- **Single Candle by Supreet Tarwarkar**
- **Options OI by Supreet Tarwarkar**
- **Futures OI by Supreet Tarwarkar**

These visuals help bring price movement and market data such as Open Interest, FII activity, volume, and derivatives positioning into the same analytical view.

I also plan to make these visuals available **free of cost** for traders who may find them useful.

---

## Dashboard Pages

### 1. Home

The Home page provides a quick latest-date market overview.

It includes:

- Buy Contracts
- Buy Amount
- Sell Contracts
- Sell Amount
- Net Contracts
- Net Amount
- EOD Open Interest Contracts
- EOD Open Interest Amount
- Latest Long / Short Ratio
- Index snapshot
- Stock and delivery snapshot
- Futures & Options snapshot
- Last updated date

![Home](Images/1.%20Home.png)

---

### 2. Index Charts

Used to review price movement across major NSE indices using OHLC candlestick charts and volume.

It includes:

- NIFTY
- BANKNIFTY
- FINNIFTY
- Candlestick / Line switching
- OHLC values
- Volume
- Date filtering

![Index Charts](Images/2.%20Index%20Charts.png)

---

### 3. FII Derivatives

Used to analyze FII derivatives activity together with index price movement.

It includes:

- Index selection
- Instrument selection
- Buy Contracts
- Sell Contracts
- Net Contracts
- Buy / Sell Amount
- Net Amount
- Historical FII activity
- Index price context
- Candlestick / Line switching
- Bar / Line switching

![FII Derivatives](Images/3.%20FII%20Derivatives.png)

---

### 4. Long / Short Ratio

Used to compare participant positioning together with index price movement.

It includes:

- FII
- DII
- Proprietary
- Client
- Long / Short Ratio
- Future Index Long positions
- Future Index Short positions
- Index price movement
- Date filtering

![Long Short Ratio](Images/4.%20LS%20Ratio.png)

---

### 5. Options Open Interest

Used for strike-wise and expiry-wise Options Open Interest analysis.

It includes:

- Call Open Interest
- Put Open Interest
- Change in Call Open Interest
- Change in Put Open Interest
- Put-Call Ratio (PCR)
- Underlying price
- ATM reference
- Strike-price analysis
- Expiry selection
- Cumulative Open Interest
- Adjustable strike range

![Options Open Interest](Images/5.%20Options%20Open%20Interest.png)

---

### 6. Futures Open Interest

Used to analyze futures price movement together with changes in Open Interest.

It includes:

- Futures Open Interest
- Change in Open Interest
- OHLC price movement
- Symbol selection
- Expiry selection
- Long Build Up
- Short Build Up
- Long Unwinding
- Short Covering

![Futures Open Interest](Images/6.%20Future%20Open%20Interest.png)

---

### 7. Stock & Delivery

Used to analyze stock price movement together with delivery activity.

It includes:

- Stock OHLC movement
- Volume
- Total Traded Quantity
- Delivery Quantity
- Delivery Percentage
- Stock search
- Symbol selection
- Date filtering
- Candlestick / Line switching
- Bar / Line switching

![Stock and Delivery](Images/7.%20Stocks%20Delivery.png)

---

## Dashboard Features

- Daily NSE EOD refresh workflow
- Dynamic latest-date KPIs
- Seven analytical report pages
- **Dark and Light theme switching using Power BI bookmarks**
- **Collapsible and expandable sidebar using bookmark navigation**
- Interactive page navigation
- Interactive slicers and filters
- Candlestick / Line switching
- Bar / Line switching
- Custom Power BI market visuals
- Historical comparison as new trading-day data is added

---

## Project Walkthrough Video

A walkthrough of the complete dashboard can be viewed here:

### [Watch Project Walkthrough](PASTE_GOOGLE_DRIVE_VIDEO_LINK_HERE)

The walkthrough covers:

- Dashboard navigation
- Daily EOD data workflow
- Index analysis
- FII derivatives analysis
- Long / Short positioning
- Options Open Interest
- Futures Open Interest
- Stock & Delivery analysis
- Custom visuals
- Dark / Light theme switching
- Collapsible sidebar navigation

---

## Power BI Report

The project was developed in **Power BI Desktop** and published to **Power BI Service** for interactive viewing.

The PBIX file is larger than GitHub's browser upload limit, so the **interactive Power BI report, dashboard screenshots, dataset documentation, and project walkthrough** are provided for reviewing the project.

---

## Author

**Supreet Tarwarkar**

- [GitHub](https://github.com/SupreetTarwarkar)
- [LinkedIn](https://www.linkedin.com/in/supreettarwarkar/)
