# Challenges Faced and Key Learnings

Building the NSE Market Analysis Dashboard involved more than creating visuals and DAX measures.

Several real issues came up during development related to custom financial visuals, data-source reliability, Power BI Service, Gateway configuration, bookmarks and deployment.

This section documents the important problems, how they were identified, how they were solved and the main learning from each one.

---

## 1. Power BI Did Not Have the Required Financial Candlestick Visual

- The first requirement was a proper financial Candlestick chart for analysing Open, High, Low, Close and Volume.

- Power BI does not provide a native Candlestick visual with all the features required for this project.

- Third-party visuals were also explored, but the tested options did not provide the complete combination of functionality required.

- The visual needed features such as:

  - OHLC Candles
  - Volume
  - Candle / Line switching
  - Crosshair
  - Hover values
  - Tooltips
  - Axis controls
  - Date scrolling
  - Custom formatting
  - Dynamic market fields

- Because of these limitations, a custom **Candlestick visual** was developed using ChatGPT-assisted coding.

- The financial requirement, expected behaviour, data fields and test conditions were defined first.

- ChatGPT was then used to help generate and modify the TypeScript-based custom visual code.

- Every build was compiled, imported into Power BI Desktop and tested using actual NSE market data.

### Development Flow

<div align="center">

**Requirement**

↓

**ChatGPT-assisted Code**

↓

**Compile PBIVIZ**

↓

**Import into Power BI**

↓

**Test with NSE Data**

↓

**Identify Issue**

↓

**Modify and Rebuild**

↓

**Retest**

</div>

- The Candlestick visual went through approximately **25–26 test builds**.

- Some changes solved one issue but affected another existing feature.

- For example, a fix related to hover behaviour could affect the OHLC header or another existing visual feature.

- This made regression testing necessary after important changes.

### Tools Used

- Power BI Desktop
- Power BI Custom Visual framework
- TypeScript
- PBIVIZ packaging
- ChatGPT
- NSE market data for testing

### Key Learning

- Custom visual development is not only about writing code.

- Clear requirements, repeated testing and validation are equally important.

---

## 2. Supporting Data Could Not Be Properly Aligned Below the Candlestick

- Once the Candlestick visual was working, the next requirement was to display supporting market information directly below the price chart.

Examples included:

- Price + Futures Open Interest
- Price + FII Activity
- Price + Delivery Data

- A normal Power BI Bar or Line visual could display these values, but the dates did not always align exactly with the custom Candlestick chart.

- Differences could occur because of:

  - Category spacing
  - Plot-area margins
  - Axis padding
  - Date positioning
  - Independent visual behaviour

- For financial analysis, the supporting value for a trading date needed to appear directly below the candle for the same trading date.

### Required Alignment

<div align="center">

**05 Sep Candle**

↓

**05 Sep Supporting Value**

</div>

- This requirement led to the development of the **Bar & Line custom visual**.

- The purpose of this visual was specifically to work together with the Candlestick visual.

- The Bar & Line visual went through approximately **18–20 test builds**.

- Testing included:

  - Bar mode
  - Line mode
  - Bar / Line switching
  - Date alignment
  - Axis spacing
  - Labels
  - Formatting controls
  - Scrolling behaviour

- After testing the visual inside the complete dashboard, some unnecessary features were removed.

- For example, the final Bar & Line visual did not require its own scrollbar.

### Key Learning

- A visual can work correctly by itself but still require changes after integration into the complete dashboard.

- The final behaviour should always be tested inside the actual report where the visual will be used.

---

## 3. Futures Open Interest Required Separate Market Logic

- Futures Open Interest could not be handled only as a normal Bar chart.

- The requirement was to analyse Price movement together with Open Interest movement.

- The activity also needed to be classified automatically.

| Price | OI | Interpretation |
|---|---|---|
| ↑ | ↑ | Long Buildup |
| ↓ | ↑ | Short Buildup |
| ↑ | ↓ | Short Covering |
| ↓ | ↓ | Long Unwinding |

- A separate **Futures OI custom visual** was therefore developed.

- The visual went through approximately **10–13 test builds**.

- Testing included:

  - Price + OI classification
  - Colours
  - Legends
  - Axis behaviour
  - Scrolling
  - Category completeness
  - Integration with the Candlestick visual

- Earlier versions contained additional viewing modes.

- After testing, the final visual was simplified to a Bar-based view because it worked better for OI interpretation.

### Key Learning

- A visual should not keep a feature only because it has already been developed.

- If testing shows that a feature does not improve the analysis, removing it can make the final visual better.

---

## 4. Options Open Interest Needed a Different Type of Visual

- Options analysis introduced a different requirement because the analysis is based around strike prices.

- The required visual needed to support:

  - CE Open Interest
  - PE Open Interest
  - Change in CE OI
  - Change in PE OI
  - ATM reference
  - Expiry selection
  - Cumulative OI
  - Strike-range controls

- This led to the development of the **Options OI custom visual**.

- The visual went through approximately **10–12 test builds**.

- ATM needed to remain clearly visible so that Call and Put positioning could be analysed around the current market level.

- Strike-range controls were added to allow analysis around ATM using:

  - ±10 strikes
  - ±20 strikes
  - ±30 strikes
  - ±40 strikes
  - ±50 strikes

### Key Learning

- Different financial instruments need different visual behaviour.

- One generic visual cannot always represent Candlestick, Futures OI and Options OI analysis correctly.

---

## 5. The Home Page Needed a Latest-Day Overview

- Once the detailed analysis pages were ready, the Home page required a different type of visual.

- The purpose of the Home page was to provide a quick latest-market snapshot.

- Using a full historical Candlestick chart would have repeated information already available on the detailed pages.

- Only the latest available trading-day candle was required.

- This led to the development of the **Single Candle custom visual**.

- The visual was designed to show:

  - Open
  - High
  - Low
  - Close
  - Latest trading-day candle
  - Crosshair
  - Price label
  - Hover information

- The Single Candle visual went through approximately **4–5 test builds**.

- The same visual could then be reused for different latest-market snapshots on the Home page.

### Visual Development Journey

<div align="center">

**Need Financial Price Chart**

↓

**Candlestick Visual**

<br>

**Need Supporting Data Below Price**

↓

**Bar & Line Visual**

<br>

**Need Price + OI Classification**

↓

**Futures OI Visual**

<br>

**Need Strike-wise Options Analysis**

↓

**Options OI Visual**

<br>

**Need Latest-Day Home Overview**

↓

**Single Candle Visual**

</div>

---

## 6. The Custom Visual Family Had to Be Standardised

- After the custom visuals were developed, another issue became visible.

- The visuals had been created at different stages, so similar settings were not always named or organised in exactly the same way.

- Standardisation was required across:

  - X-axis
  - Y-axis
  - Tooltip
  - Range Scroller
  - Mode selection
  - Transparency behaviour
  - Formatting order
  - Selected-state controls
  - Icons

- The Candlestick visual was used as the main reference.

- Other visuals were aligned with the same structure wherever equivalent functionality existed.

### Key Learning

- When several custom visuals belong to the same project, consistency is important.

- Users should not have to learn a completely different formatting structure for every visual.

---

## 7. Excel STOCKHISTORY Stopped Providing New Index Data

- Initially, Index price data was obtained through Excel using **STOCKHISTORY**.

- The dashboard had already been developed using this source.

- Later, even after extending the requested end date, the Index data continued to stop at **7 September 2026**.

- At first, this appeared to be a Power BI refresh issue.

- The issue was checked backwards through the data flow.

### Debugging Flow

<div align="center">

**Power BI Visual**

↓

**Data Model**

↓

**Power Query**

↓

**Excel File**

↓

**STOCKHISTORY**

</div>

- The missing dates were already absent in Excel.

- This confirmed that Power BI was not the original cause of the problem.

### Key Learning

- When a dashboard stops updating, the original source should be checked before debugging the visual or DAX.

- Power BI cannot display data that is already missing from the upstream source.

---

## 8. Index Data Had to Be Migrated to Official NSE Files

- Since STOCKHISTORY was no longer providing the required latest Index data, another reliable source was required.

- Official NSE daily Index files were selected as the replacement source.

- By this stage, the dashboard was already substantially complete.

- Rebuilding the complete report would have affected:

  - Visuals
  - Relationships
  - DAX
  - Filters
  - Custom visual field mappings
  - Other report logic

- The new NSE data was therefore transformed so that it remained compatible with the existing report structure as much as possible.

### Migration Flow

<div align="center">

**Old Excel Structure**

↓

**Identify Existing Fields Used by the Report**

↓

**Load NSE Index Files**

↓

**Clean and Transform in Power Query**

↓

**Match Required Field Structure**

↓

**Reconnect Existing Model**

↓

**Validate DAX**

↓

**Validate Visuals**

↓

**Check Latest Date**

</div>

### Key Learning

- When replacing a source in an already-developed report, keeping the downstream field structure stable can prevent unnecessary rebuilding.

- This also reduces the risk of breaking existing DAX, relationships and visuals.

---

## 9. Old Excel Dependencies Continued to Create Gateway Warnings

- After moving the main Index data to NSE files, the dashboard itself was working correctly.

- Power BI Service still showed warnings related to the old Excel source.

- Changing the visible visual source did not automatically remove every dependency on the old table.

- Remaining dependencies could exist through:

  - Power Query queries
  - Referenced queries
  - Relationships
  - Calculated columns
  - Calculated tables
  - DAX measures
  - Hidden or helper tables

### Dependency Flow

<div align="center">

**Old Excel Source**

↓

**Query / Table**

↓

**Model Dependency**

↓

**Power BI Service**

↓

**Gateway Warning**

</div>

- DAX itself does not create a Gateway connection.

- However, if a DAX expression depends on a table coming from the old Excel source, that source can still remain part of the model dependency.

### What Had to Be Checked

- Source connections
- Power Query queries
- Tables
- Relationships
- Measures
- Calculated columns
- Hidden dependencies
- Gateway source mapping

### Key Learning

- A source migration is not complete when the new visual starts working.

- The old source should also be removed from every place where it is no longer required.

---

## 10. Large Number of Bookmarks Became Difficult to Manage

- The dashboard eventually used many bookmarks.

- Bookmarks were used for:

  - Dark Theme
  - Light Theme
  - Sidebar ON
  - Sidebar OFF
  - Information popups
  - Close buttons
  - Visual states
  - Expanded and collapsed layouts

- As the number of bookmarks increased, managing them became difficult.

- Updating the wrong bookmark could unintentionally change:

  - Visual visibility
  - Layout state
  - Selection state
  - Slicer values
  - Filter values

- Bookmark Data state became especially important.

- For example, changing from Dark Theme to Light Theme should only change the appearance of the report.

- It should not change:

  - Index selection
  - Expiry
  - Date
  - Participant type
  - Other slicers

- Because of this, bookmarks were checked and updated **one by one**.

### Bookmark Testing Flow

<div align="center">

**Select Bookmark**

↓

**Check Purpose**

↓

**Check Visibility**

↓

**Check Data State**

↓

**Update**

↓

**Test**

↓

**Move to Next Bookmark**

</div>

- This took more time but reduced the chance of breaking unrelated report states.

- Clear bookmark naming also became important.

Examples:

- `Theme_Dark`
- `Theme_Light`
- `Sidebar_On`
- `Sidebar_Off`
- `Info_FuturesOI_Open`
- `Info_FuturesOI_Close`

### Key Learning

- A few bookmarks are easy to manage.

- Once bookmarks become part of the complete dashboard UI, they need proper naming, grouping and individual testing.

---

## 11. Power BI Desktop Refresh Did Not Guarantee Power BI Service Refresh

- A report could work correctly and refresh successfully in Power BI Desktop but still have issues after publishing.

- Power BI Desktop can directly access local files.

Example:

`C:\Folder\Data.xlsx`

- Power BI Service cannot directly access the same local computer path.

- Local or folder-based sources may therefore require:

  - On-premises Data Gateway
  - Correct credentials
  - Correct source mapping
  - Service refresh configuration

### Deployment Testing Flow

<div align="center">

**Desktop Refresh**

↓

**Publish**

↓

**Configure Gateway**

↓

**Service Refresh**

↓

**Validate Latest Data**

</div>

### Key Learning

- Successful Desktop refresh does not mean the report is deployment-ready.

- Power BI Service refresh should always be tested separately.

---

## 12. Desktop, Service and Publish-to-Web Did Not Always Behave the Same

- One of the information buttons worked correctly in Power BI Desktop.

- The same button also worked correctly in Power BI Service.

- However, it did not behave correctly through the Publish-to-Web public link.

- This made the issue difficult to diagnose because the PBIX itself appeared correct.

- Areas checked during troubleshooting included:

  - Visual overlap
  - Object layering
  - Bookmark target
  - Button action
  - Page size
  - Public rendering behaviour

### Final Testing Flow

<div align="center">

**Power BI Desktop**

↓

**Power BI Service**

↓

**Publish-to-Web**

</div>

### Key Learning

- The final report should always be tested in the same environment where the end user will consume it.

---

## 13. Major Changes Required Full Regression Testing

- Towards the end of the project, changing one component could affect several other areas.

- The dashboard contained:

  - Multiple data sources
  - Power Query
  - DAX
  - Custom visuals
  - Bookmarks
  - Dark / Light themes
  - Collapsible sidebar
  - Information buttons
  - Gateway
  - Power BI Service
  - Publish-to-Web

- Testing only the changed component was therefore not sufficient.

### Regression Testing Flow

<div align="center">

**Source Data**

↓

**Power Query**

↓

**Model**

↓

**DAX**

↓

**Visuals**

↓

**Filters**

↓

**Bookmarks**

↓

**Themes**

↓

**Sidebar**

↓

**Information Buttons**

↓

**Power BI Service**

↓

**Public Link**

</div>

### Key Learning

- After major source, bookmark or custom-visual changes, the complete dashboard should be tested again.

---

## 14. Financial Metrics Had to Be Explained Carefully

- Not every challenge was technical.

- Financial-market metrics can easily be over-interpreted if they are presented without proper context.

### Put-Call Ratio

- PCR above 1 means Put OI is greater than Call OI.

- It does not guarantee that the market will move upward.

### Delivery Percentage

- Higher Delivery % means a larger share of traded quantity resulted in delivery.

- It does not automatically mean buying.

### Futures Open Interest

- Price and OI combinations can help classify positioning.

- They should not be treated as guaranteed future market direction.

### Long / Short Ratio

- The dashboard calculates:

**Long ÷ (Long + Short)**

- It does not calculate:

**Long ÷ Short**

- Therefore:

  - 50% = Long and Short are equal
  - Above 50% = relatively more Long exposure
  - Below 50% = relatively more Short exposure

### Key Learning

- A dashboard should not only calculate a metric correctly.

- The explanation should also avoid giving a stronger conclusion than the underlying data supports.

---

# Overall Project Journey

<div align="center">

**Understand Market Requirement**

↓

**Build Initial Power BI Model**

↓

**Candlestick Limitation Identified**

↓

**Candlestick Visual Developed — 25–26 Builds**

↓

**Need Supporting Data Below Candles**

↓

**Bar & Line Developed — 18–20 Builds**

↓

**Need Futures Price + OI Classification**

↓

**Futures OI Developed — 10–13 Builds**

↓

**Need Options Strike-Level Analysis**

↓

**Options OI Developed — 10–12 Builds**

↓

**Need Latest-Day Home Overview**

↓

**Single Candle Developed — 4–5 Builds**

↓

**Custom Visual Family Standardised**

↓

**STOCKHISTORY Stops Updating**

↓

**Issue Traced Back to Source**

↓

**Index Data Migrated to Official NSE Files**

↓

**Existing Report Structure Preserved**

↓

**Old Excel Dependency Causes Gateway Warning**

↓

**Dependencies Cleaned**

↓

**Bookmarks Checked One by One**

↓

**Desktop Testing**

↓

**Power BI Service Testing**

↓

**Publish-to-Web Testing**

↓

**Final Regression Testing**

</div>

---

## Final Learning

The main learning from this project was that building a complete Power BI solution involves much more than creating charts.

A reliable dashboard also requires:

- Reliable source data
- Clean Power Query transformations
- Stable data-model design
- Correct DAX
- Suitable visualisation
- Careful bookmark management
- Deployment testing
- Gateway configuration
- Regression testing
- Clear interpretation of the underlying business data
