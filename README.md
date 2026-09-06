# NSE Market Analysis Dashboard

## Why I Built This Project

- As a trader, I found that market data such as Open Interest, FII activity, Long / Short Ratio, and delivery data was often viewed separately from price charts.

- This meant checking the data in one place and then using another platform to compare it with candlestick price movement.

- The main purpose of this project was to bring **market data and candlestick charts together on the same screen**, making it easier to understand how changes in positioning, Open Interest, or delivery activity were reflected in price movement.

- I also wanted one place to analyze **FII derivatives activity, participant-wise positioning, Options OI, Futures OI, Long / Short Ratio, and stock delivery data** instead of checking them separately.

- Some platforms provide processed views of metrics such as Long / Short Ratio, Open Interest, and delivery data as paid features, while the underlying EOD reports used in this project are available directly from NSE.

I later developed this idea into a Data Analytics project using **Power BI, Power Query, DAX, data modeling, interactive visuals, and custom Power BI visuals**.

The dashboard follows a daily EOD workflow. After each NSE trading day, the latest files can be added to the existing source folders and the Power BI report refreshed. The latest-date KPIs and visuals update with the new data, while previous trading-day data remains available for historical comparison.

[View Interactive Power BI Dashboard](PASTE_POWER_BI_LINK_HERE)

---

# Tech Stack

- **Power BI** - Dashboard development and interactive reporting
- **Power Query** - Cleaning, transforming, and combining daily NSE files
- **DAX** - KPIs, ratios, latest-date calculations, and analytical measures
- **Data Modeling** - Connecting market datasets through a common analytical model
- **Excel / CSV Files** - NSE EOD source data
- **Custom Power BI Visuals** - Custom visuals developed for market and Open Interest analysis

---

# Data Source

The project uses official **NSE End-of-Day market reports**.

The four main NSE files used are:

1. **Full Bhavcopy and Security Deliverable Data**
2. **F&O Participant-wise Open Interest**
3. **F&O FII Derivatives Statistics**
4. **F&O UDiFF Common Bhavcopy Final**

For this project, I have used around **one month of EOD market data from August 2026 onward** to keep the Power BI file size practical.

Detailed source information and the refresh process are available in the:

[Dataset Documentation](Dataset/README.md)

---

# Daily Refresh Workflow

1. Download the latest EOD files from NSE after the trading day.
2. Add the new files to the relevant source folders.
3. Refresh the Power BI report.
4. Power Query combines the new data with the existing data.
5. Latest-date KPIs and visuals update automatically.
6. Previous trading-day data remains available for historical analysis.

---

# Dashboard Pages

## 1. Home

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

## 2. Index Charts

Used to review price movement across major NSE indices using OHLC candlestick charts and volume.

The page includes:

- NIFTY
- BANKNIFTY
- FINNIFTY
- Candlestick / Line switching
- OHLC values
- Volume
- Date filtering

![Index Charts](Images/2.%20Index%20Charts.png)

---

## 3. FII Derivatives

Used to analyze FII activity across derivative instruments.

The page includes:

- Index selection
- Instrument selection
- Net Amount
- Net Contracts
- Historical FII activity
- Index price context
- Candlestick / Line switching
- Bar / Line switching

![FII Derivatives](Images/3.%20FII%20Derivatives.png)

---

## 4. Long / Short Ratio

Used to compare participant positioning in the derivatives market.

The page includes:

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

## 5. Options Open Interest

Used for strike-wise and expiry-wise Options Open Interest analysis.

The page includes:

- Call Open Interest
- Put Open Interest
- Change in Call Open Interest
- Change in Put Open Interest
- Put-Call Ratio (PCR)
- ATM reference
- Strike-price analysis
- Expiry selection
- Cumulative Open Interest
- Adjustable strike range

![Options Open Interest](Images/5.%20Options%20Open%20Interest.png)

---

## 6. Futures Open Interest

Used to review futures price movement together with Open Interest activity.

The page includes:

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

## 7. Stock & Delivery

Used to analyze cash-market stock activity together with delivery data.

The page includes:

- Stock OHLC movement
- Volume
- Delivery Quantity
- Delivery Percentage
- Stock search
- Symbol selection
- Date filtering
- Candlestick / Line switching
- Bar / Line switching

![Stock and Delivery](Images/7.%20Stocks%20Delivery.png)

---

# Custom Power BI Visuals

This report also uses custom Power BI visuals developed specifically for this market-analysis project:

- **Candlestick by Supreet Tarwarkar**
- **Bar & Line by Supreet Tarwarkar**
- **Single Candle by Supreet Tarwarkar**
- **Options OI by Supreet Tarwarkar**
- **Futures OI by Supreet Tarwarkar**

The visuals are used for OHLC price charts, market trends, Futures Open Interest, and Options Open Interest analysis.

---

# Dashboard Features

- Daily EOD refresh workflow
- Dynamic latest-date KPIs
- Seven analytical report pages
- Dark and Light theme switching
- Collapsible sidebar navigation
- Interactive slicers and filters
- Candlestick / Line switching
- Bar / Line switching
- Custom Power BI market visuals
- Historical analysis that grows as new trading-day files are added

---

# Project Walkthrough Video

A complete walkthrough of the dashboard can be viewed here:

[Watch Project Walkthrough](PASTE_GOOGLE_DRIVE_VIDEO_LINK_HERE)

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
- Dashboard interactions

---

# Power BI Report

The project was developed in **Power BI Desktop** and published to **Power BI Service** for interactive viewing.

The PBIX file is currently larger than GitHub's browser upload limit, so the interactive Power BI report and dashboard screenshots are provided for reviewing the project.

---

# Author

**Supreet Tarwarkar**

- [GitHub](https://github.com/SupreetTarwarkar)
- [LinkedIn](https://www.linkedin.com/in/supreettarwarkar/)
