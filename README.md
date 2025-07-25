## 📘 Facebook Top Pages Dashboard - Power BI Project

---

## 📌 Overview

**The Facebook Top Pages Dashboard** is a comprehensive Power BI project designed to track, analyze, and visualize the performance of popular Facebook Pages. The project leverages live API data, processes it using Power Query, and displays it through interactive and dynamic visuals. The goal is to provide actionable insights for social media managers, marketers, and content creators.

---

## 🔗 Data Source - API Integration

The dataset is retrieved directly from the Facebook Insights API (a third-party wrapper).

### 🔧 How the API Integration Works:

- A custom Power BI web connector is used to fetch JSON data.
- Parameters include the Page ID, metrics (likes, posts, engagement), and access tokens. - API authentication is performed using a token passed in the header or query string.
- Data is refreshed on request or scheduled via the Power BI service (with a gateway, if necessary).

--

## 🧼 Data Cleansing - Power Query (M Language)

Once the API response is loaded, it is cleaned and structured using the **Power Query Editor**.

### ⚙️ Key Cleansing Steps:

| Step | Description |
|------|-----------|
| Column Rename | Cleaned names to remove special characters and make them readable |
| Record Expansion | Flatten nested JSON structures (e.g., `data`, `insights`, `paging`) |
| Row Filtering | Remove empty/null records and filter out relevant timeframes |
| Change Types | Date fields, numeric metrics, and flags are converted to appropriate data types |
| Derived Columns | Additional columns such as year, month, page category, or post type are created |
| Error Handling | Use "Try... Else" logic to detect and replace API errors or blanks |

All cleanup steps are **tagged**, allowing for dynamic updating without the need for manual modifications.

---

## 🧠 Data Model Design

The model has been optimized according to **star schema** best practices, ensuring clear relationships between fact tables and dimensions.

| Table | Type | Description |
|------|------|-----------|
| `Facebook Metrics` | Fact | Core metrics: Likes, Shares, Comments, Reach, Engagement |
| `Pages` | Dimension | Facebook Page details such as name, category, creation date |
| `Date` | Dimension | Custom date table with full calendar logic for time analysis |

--

## 🧮 DAX Metrics

DAX functions are custom-designed to support KPI and engagement calculations.

### 🧾 Key Metrics:

- Total Likes = SUM(FacebookMetrics[Likes])
- Engagement Rate = DIVIDE(SUM(FacebookMetrics[Engagement]), SUM(FacebookMetrics[Reach]))
- Average Comments per Post = AVERAGEX(FacebookMetrics, FacebookMetrics[Comments])
- Top Page = RANKX(All Pages), [Total Likes])
- Likes over Time = CALCULATE([Total Likes], DATESYTD('Date'[Date]))

Time Intelligence features (e.g., YTD, MTD) are enabled via a custom spreadsheet.

---

## 📊 Dashboard Components

The report includes several interactive elements:

| Section | Description |
|-------|-----------|
| **Key Performance Indicators** | Cards displaying total likes, engagement rate, average reach, and top posts |
| **Time Series Chart** | Engagement trends over days/weeks/months |
| **Ranking Table** | Top Facebook Pages ranked by likes, reach, or engagement |
| **Geo Map** | Regional or country performance if location data is available |
| **Post Type Analysis** | Content Type Breakdown: Video, Image, Link, etc. |
| **Dividers** | Filter by Page, Date Range, Post Type, or Category |

All visual elements are fully dynamic and connected to dividers and filters.

---

## 🎯 Project Objectives

- Enable real-time monitoring of social media performance
- Identify top-performing pages and content strategies
- Support marketing teams in content planning and analysis
- Compare historical and recent performance metrics
- Display metrics in a clear, modern dashboard

---

## 🧩 Best Practices

- ✅ Live data ingestion via API
- ✅ Clear, clearly named queries and metrics
- ✅ Enhanced data model using star schema
- ✅ Reusable DAX metrics
- ✅ Conditional formatting and tooltips for clarity
- ✅ Mobile-friendly design (optional)

---

## 🚀 How to Use

1. Open the "Top Facebook Pages Dashboard.pbix" file in **Power BI Desktop**
2. Go to **Data Transform** to examine or modify the Power Query logic
3. Refresh the data (requires valid API access token)
4. Explore the dashboard using slicing tools and Filters
5. Publish to Power BI for Auto-Update and Sharing

---

## 🛠️ Technologies Used

- Power BI Desktop
- Power Query (M)
- DAX (Data Analysis Expressions)
- Facebook Graph API or External Analytics API
- JSON Data Modeling
- Power BI (for Scheduling and Sharing)

---

## 📌 Conclusion

This project demonstrates how **Power BI** can seamlessly integrate with web APIs to provide scalable and straightforward dashboards for marketing and social media analytics. With reusable queries, an elegant template, and insightful visuals, this project is a great starting point for automating social media intelligence.
