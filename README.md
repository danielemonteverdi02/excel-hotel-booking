# 🏨 Hotel Booking Analysis with Microsoft Excel

## 📌 Project Overview

This project focuses on the complete analysis of a hotel booking dataset using **Microsoft Excel**. The objective was to simulate a real Business Intelligence workflow, starting from raw data cleaning, continuing with exploratory data analysis, and ending with the development of interactive dashboards.

Unlike a simple visualization project, the entire process includes **data cleaning, feature engineering, data quality assessment, Pivot Table analysis and dashboard creation**, reproducing the typical activities performed by a Junior Data Analyst.

---

The complete Excel file containing:
- Data Quality Check
- Pivot Analysis
- Overview Dashboard
- Customer Analysis Dashboard
- Market & Geography Dashboard

is available here:

[📊 Download Excel Dashboard](https://drive.google.com/uc?export=download&id=1siMbL324IhNcKjkrEukAnT761hXNJp38)

**Note:** The complete Excel workbook is relatively large (~120 MB)

---

# 🎯 Objectives

The project was developed to:

- Clean and standardize inconsistent data
- Detect and monitor data quality issues
- Create new analytical variables
- Perform exploratory analysis using Pivot Tables
- Build interactive dashboards using Pivot Charts and Slicers
- Extract business insights from hotel booking data

---

# 📊 Dataset

**Source:** Hotel Booking Demand Dataset (Kaggle)

The dataset contains:

- **119,390 bookings**
- More than **40 variables**

Main variables include:

- Hotel type
- Cancellation status
- Lead time
- Arrival date
- Number of guests
- Country
- Market segment
- Distribution channel
- Customer type
- Room type
- Booking modifications
- Waiting list days
- ADR (Average Daily Rate)
- Parking requests
- Special requests
- Reservation status

---

# 🛠 Tools Used

- Microsoft Excel
- Pivot Tables
- Pivot Charts
- Slicers
- Conditional Formatting

---

# 🔄 Project Workflow

```
Raw Dataset
      ↓
Data Quality Analysis
      ↓
Data Cleaning
      ↓
Feature Engineering
      ↓
Pivot Table Analysis
      ↓
Dashboard Development
      ↓
Business Insights
```

---

# 🧹 Data Cleaning

Several variables contained inconsistent values, typing mistakes and invalid observations.

A dedicated **Data Quality Check** worksheet was created to document every transformation before applying it to the cleaned dataset.

---

## 1. Hotel Standardization

Original variable:

```
hotel
```

Examples of inconsistent values:

| Dirty Value | Clean Value |
|------------|-------------|
| City  Hotel | City Hotel |
| CITY HOTEL | City Hotel |
| CityHotel | City Hotel |
| Resort  Hotel | Resort Hotel |
| RESORT HOTEL | Resort Hotel |
| ResortHotel | Resort Hotel |

New variable:

```
hotel_clean
```

Applied using a mapping table with:

```excel
=CERCA.X()
```

---

## 2. Cancellation Status

Original:

```
is_canceled
```

Mapping:

| Original | New |
|-----------|-----|
|0|No|
|1|Yes|

New variable:

```
is_canceled_recode
```

Formula:

```excel
=SE(A2=0;"No";"Yes")
```

---

## 3. Adults Cleaning

Invalid values detected:

|Original|Clean|
|---------|-----|
|-1|NA|

New variable:

```
adults_clean
```

---

## 4. Children Cleaning

Invalid values:

|Original|Clean|
|---------|-----|
|-1|NA|
|10|NA|
|20|NA|

New variable:

```
children_clean
```

---

## 5. Babies Cleaning

Invalid values:

|Original|Clean|
|---------|-----|
|9|NA|
|10|NA|

New variable:

```
babies_clean
```

---

## 6. Country Cleaning

Several country names contained typing mistakes or different abbreviations.

Examples:

| Dirty Value | Clean Value |
|-------------|-------------|
|Geramny|DEU|
|GER|DEU|
|Spian|ESP|
|ES P|ESP|
|Frnce|FRA|
|fra|FRA|
|Itlay|ITA|
|Portugl|PRT|
|GB|GBR|
|UK|GBR|
|China|CHN|
|CN|CHN|
|-|NA|
|NULL|NA|
|UNKNOWN|NA|
|MISSING|NA|
|N/A|NA|

New variable:

```
country_clean
```

Created using:

```excel
=CERCA.X()
```

---

## 7. Market Segment Cleaning

Leading/trailing spaces created duplicated categories.

Examples:

```
 Aviation
 Corporate
 Online TA
```

↓

```
Aviation
Corporate
Online TA
```

New variable:

```
market_segment_clean
```

---

## 8. Distribution Channel Cleaning

Examples:

```
Corporate
Corporate␠

Direct
Direct␠

TA/TO
TA/TO␠
```

↓

Standardized values.

New variable:

```
distribution_channel_clean
```

---

## 9. ADR Cleaning

Invalid observations identified:

|Original|Recode|
|---------|------|
|ADR < 0|NA|
|5400|NA|

New variable:

```
adr_clean
```

---

# 🏷 Feature Engineering

Several new variables were created to simplify the analysis.

## Region

Countries were grouped into macro geographical regions.

Examples:

- Western Europe
- Southern Europe
- Eastern Europe
- Northern Europe
- North America
- South America
- Asia
- Africa
- Oceania
- Missing

Created using a second mapping table and:

```excel
=CERCA.X()
```

---

## Room Match Status

Comparison between:

```
reserved_room_type
```

and

```
assigned_room_type
```

New variable:

```
room_match_status
```

Categories:

- Same
- Different

Formula:

```excel
=SE(reserved=assigned;"Same";"Different")
```

---

## Booking Changes

Numeric variable transformed into categories.

|Original|Category|
|----------|---------|
|0|No changes|
|1|One change|
|2-3|Few changes|
|≥4|Many changes|

New variable:

```
booking_changes_cat
```

Created with:

```excel
=PIÙ.SE(...)
```

---

## Waiting List

Grouped into:

- No waiting
- Short
- Medium
- Long

New variable:

```
days_wait_list_cat
```

---

## Parking

Grouped into:

- No Parking
- Parking Required

New variable:

```
car_parking_cat
```

---

## Special Requests

Grouped into:

- None
- Few
- Many

New variable:

```
special_request_cat
```

---

## Booking Modified

Binary variable indicating whether a booking had at least one modification.

Categories:

- Yes
- No

---

# ✅ Data Quality Checks

A dedicated worksheet was created to monitor anomalies rather than removing observations.

The following consistency rules were implemented:

|Condition|Category|
|----------|----------|
|Adults, Children and Babies all equal 0|Empty / Invalid|
|Presence of at least one NA|Incomplete Data|
|Adults = 0 but Children/Babies > 0|Logical Anomaly|
|Adults ≥10 and Customer Type ≠ Group|Suspicious Number of Guests|
|Otherwise|Valid|

Implemented using:

- `PIÙ.SE()`
- `SE()`
- `E()`
- `O()`

The anomaly classification was retained during the analysis to document data quality rather than discarding observations.

---

# 📈 Exploratory Data Analysis

The exploratory phase was performed through multiple Pivot Tables to investigate:

- Hotel distribution
- Cancellation rate
- ADR
- Booking trends
- Customer behaviour
- Market segments
- Geographic distribution
- Waiting list
- Booking modifications
- Room assignment consistency
- Special requests
- Parking demand

Conditional Formatting was extensively used to highlight:

- highest values
- lowest values
- heatmaps
- business patterns

---

# 📊 Dashboard Development

Three interactive dashboards were created.

---

# Dashboard 1 — Hotel Booking Overview

Purpose:

Provide a general overview of hotel performance.

### KPI

- Total Bookings
- Cancellation Rate
- Average ADR
- Repeat Guest Rate
- Room Change Rate
- Booking Modification Rate

### Charts

- Reservation Status
- Monthly Booking Trend
- ADR Trend
- Special Requests vs ADR
- Lead Time by Hotel & Cancellation
- Monthly Cancellation Trend

### Interactive Filters

- Hotel
- Year
- Market Segment
- Customer Type
- Region

---

# Dashboard 2 — Customer Analysis

Purpose:

Analyze customer behaviour.

### KPI

- Average Stay Duration
- Average Lead Time
- Cancellation Rate
- Guests with Special Requests

### Charts

- Customer Type Distribution
- Cancellation Rate by Market Segment
- Booking Changes vs ADR
- Market Segment Distribution
- Parking Demand vs ADR
- Special Requests by Customer Type

### Interactive Filters

- Hotel
- Market Segment
- Customer Type
- Deposit Type
- Repeated Guest

---

# Dashboard 3 — Market & Geography Analysis

Purpose:

Analyze bookings by geographical area and market segment.

### KPI

- Total Countries
- Top Market Region
- High Value Markets
- Top Market Segment

### Charts

- Top 10 Countries Table
- World Map (Average ADR)
- Region Cancellation Rate
- Distribution Channel
- Market Segment vs ADR
- Heatmap (Region × Market Segment)

### Interactive Filters

- Hotel
- Year
- Customer Type
- Market Segment
- Region

---

# 📌 Main Business Insights

The analysis highlighted several interesting patterns:

- Online TA is the dominant market segment.
- Southern Europe generates the highest number of bookings.
- Portugal is the largest booking market.
- Repeat guests represent only a small proportion of customers.
- Bookings with more special requests generally show higher ADR values.
- Lead Time is considerably higher among cancelled bookings.
- Customer behaviour differs substantially across customer types and market segments.

---

# 💻 Excel Features Used

- Pivot Tables
- Pivot Charts
- Combo Charts
- Line Charts
- Clustered Bar Charts
- 100% Stacked Bar Charts
- Donut Charts
- World Map Charts
- Conditional Formatting
- Slicers
- Data Validation
- Mapping Tables

Functions used:

- `CERCA.X()`
- `SE()`
- `PIÙ.SE()`
- `E()`
- `O()`
- `SE.ERRORE()`
- `SOMMA()`
- `MEDIA()`
- `CONTA.SE()`
- `INFO.DATI.TAB.PIVOT()`

---

# 🎯 Skills Demonstrated

- Data Cleaning
- Data Quality Assessment
- Data Transformation
- Feature Engineering
- Exploratory Data Analysis (EDA)
- Pivot Table Analysis
- Interactive Dashboard Design
- Business KPI Development
- Data Visualization
- Microsoft Excel Advanced Functions

---

# 📌 Conclusion

This project demonstrates a complete analytical workflow entirely developed in Microsoft Excel. Starting from a raw dataset, multiple data cleaning and transformation techniques were applied to improve data consistency and create meaningful analytical variables. The cleaned data was then explored using Pivot Tables and transformed into three interactive dashboards, allowing users to monitor hotel performance, customer behaviour, and geographical trends through dynamic KPIs, charts, slicers, and business insights.

The project highlights practical skills in **data preparation, exploratory analysis, dashboard design, and business intelligence reporting**, providing an end-to-end example of a real-world Excel Data Analyst workflow.
