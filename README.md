# NSE Derivatives Analytics Dashboard

## Short Description / Purpose

End-to-end derivatives analytics solution developed using Power BI, SQL, and NSE Futures & Options data. The dashboard analyzes Open Interest (OI), Change in Open Interest, Long-Short Ratio, Net Contracts, and price movements to identify market positioning, sentiment shifts, and derivative trading opportunities across Index and Stock derivatives.

## Tech Stack

The dashboard was built using the following tools and technologies:

- Power BI : Data visualization and reporting
- SQL : Data extraction and transformation
- Power Query : Data transformation and cleaning
- DAX (Data Analysis Expressions) : Measures and business calculations
- Data Modeling : Relationship management and analytical structure
- Excel / CSV Files : NSE Derivatives Data Source

## Data Source

The dashboard uses NSE Derivatives (Futures & Options) data containing:

- Index Futures Data
- Index Options Data
- Stock Futures Data
- Stock Options Data
- Open Interest (OI)
- Change in Open Interest
- Long Positions
- Short Positions
- Net Contracts
- Long-Short Ratio
- Expiry Information
- Daily Price Data (OHLC)

## Features / Highlights

### Business Problem

Derivative markets generate massive volumes of Futures and Options data every trading day. However, identifying institutional positioning, tracking changes in market sentiment, analyzing Open Interest behavior, and monitoring Long-Short activity can be difficult without a centralized analytics solution.

### Goal of the Dashboard

- Monitor derivative market activity
- Analyze Open Interest trends
- Track Change in Open Interest
- Evaluate Long-Short positioning
- Identify market sentiment shifts
- Support data-driven trading decisions

### Walk Through of Key Visuals

#### Stock Futures Analytics

- Candlestick Price Analysis
- Number of Trades Analysis
- Long-Short Ratio Trend
- Stock Selection Filter
- Date Range Analysis
- Symbol-wise Performance Analysis

#### Index Futures Analytics

- NIFTY Price Trend Analysis
- Net Contracts by Date
- Index Futures Positioning
- Index Options Positioning
- Open Interest Trend Analysis
- Market Sentiment Monitoring

#### Client Position Analytics

- Long-Short Ratio Analysis
- Client-wise Position Tracking
- Future Index Long Positions
- Future Index Short Positions
- Institutional Position Monitoring
- Historical Position Trend Analysis

#### Open Interest Statistics

- Strike-wise Open Interest Analysis
- Expiry-wise Analysis
- Call vs Put Open Interest Comparison
- Open Interest Concentration Zones
- Support and Resistance Identification
- Cumulative Open Interest Analysis

#### Change in Open Interest Analytics

- Change in OI Analysis
- Long Build-Up Detection
- Short Build-Up Detection
- Long Unwinding Detection
- Short Covering Detection
- Cumulative Change in Open Interest

### Business Impact & Insights

- Identified important support and resistance zones using Open Interest concentration.
- Tracked institutional positioning through Long-Short Ratio analysis.
- Enabled monitoring of derivative market sentiment using Futures and Options activity.
- Improved understanding of market participation through Net Contracts analysis.
- Helped identify Long Build-Up, Short Build-Up, Long Unwinding, and Short Covering opportunities.
- Supported trading and market analysis through interactive derivative analytics.

## Dashboard Screenshots

### Stock Futures Analytics



### Index Futures Analytics



### Client Position Analytics



### Open Interest Statistics



### Stock Open Interest Statistics



### Change in Open Interest Statistics



### Open Interest Build-Up Analysis



## Dataset

The dashboard uses NSE Derivatives datasets containing:

- Index Futures Data
- Index Options Data
- Stock Futures Data
- Stock Options Data
- Client Position Data
- Open Interest Data
- Change in Open Interest Data

Dataset files are available in the Dataset folder of this repository.

## SQL Scripts

The project includes SQL scripts used for data preparation and analysis.

- data_preparation.sql
  - Data Cleaning
  - Data Transformation
  - Open Interest Calculations
  - Change in Open Interest Calculations
  - Long-Short Ratio Preparation

- derivatives_analysis.sql
  - Open Interest Analysis
  - Net Contracts Analysis
  - Long-Short Ratio Analysis
  - Futures Analysis
  - Options Analysis

SQL files are available in the SQL folder of this repository.

## Power BI Report

The complete Power BI dashboard file is included in this repository.

- NSE_Derivatives_Open_Interest_Analytics_Dashboard.pbix

The PBIX file can be downloaded to explore the report, data model, measures, and visualizations.
