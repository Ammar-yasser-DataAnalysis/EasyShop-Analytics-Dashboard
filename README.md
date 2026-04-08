
## 📌 Project Overview

EasyShop is a multi-page Power BI dashboard designed to give business stakeholders a 360° view of an e-commerce platform's performance. The project covers the full data pipeline — from raw `.bak` restoration in SQL Server, through data cleaning and relational modeling, to advanced DAX-powered visualizations in Power BI.

---

## 🏆 Context

| | |
|---|---|
| **Event** | Orange × Instant Hackathon |
| **Partners** | Orange Telecom & Instant |
| **Tool Stack** | SQL Server · Power BI Desktop |
| **Data Source** | `.bak` backup file (SQL Server) |

---

## ⚙️ Technical Workflow

```
SQL Server (.bak restore)
        │
        ▼
Data Cleaning (SQL Server)
  - Null handling
  - Data type normalization
  - Duplicate removal
  - Standardizing categorical values
        │
        ▼
Power BI Connection (DirectQuery / Import)
        │
        ▼
Data Modeling
  - Star schema design
  - Relationships between fact & dimension tables
        │
        ▼
Advanced DAX Measures
  - Conversion Rate = DIVIDE([Purchases], [Total Views])
  - Engagement Rate = DIVIDE([Clicks + Views], [Total Sessions])
  - Drop-Off % = DIVIDE([Drop-Offs], [Total Clicks])
  - CTR, AOV, and custom time-intelligence measures
        │
        ▼
Power BI Dashboard (3 pages + landing screen)
```
## 🗃️ Data Model

The model follows a **star schema** with:

| Table | Type | Description |
|---|---|---|
| `FactEvents` | Fact | User interaction events (VIEW, CLICK, DROP-OFF, PURCHASE) |
| `DimProduct` | Dimension | Product details, category, tier, content type |
| `DimCustomer` | Dimension | Customer demographics (gender, country) |
| `DimDate` | Dimension | Date table for time-intelligence |
| `DimReviews` | Dimension | Customer ratings and review text |

---

## 📊 Key DAX Measures

```dax
Conversion Rate = 
    DIVIDE(
        CALCULATE(COUNTROWS(Events), Events[Stage] = "PURCHASE"),
        CALCULATE(COUNTROWS(Events), Events[Stage] = "VIEW")
    )

Engagement Rate = 
    DIVIDE(
        CALCULATE(COUNTROWS(Events), Events[Action] IN {"CLICK", "VIEW"}),
        COUNTROWS(Sessions)
    )

Drop Off % = 
    DIVIDE(
        CALCULATE(COUNTROWS(Events), Events[Stage] = "DROP-OFF"),
        CALCULATE(COUNTROWS(Events), Events[Stage] = "CLICK")
    )

Avg Order Value = 
    DIVIDE([Total Revenue], [Total Purchases])
```

---

## 🌍 Filters & Interactivity

All dashboard pages support dynamic filtering by:
- **Gender** (Female / Male)
- **Year** (2023 / 2024 / 2025)
- **Country** (Austria, Belgium, France, Germany, Italy, Netherlands, Spain, Sweden, Switzerland, UK)
- **Product Name** (20+ sports & lifestyle products)

---
## 🗂️ Dashboard Pages

### 1. Executive Overview
High-level KPIs for decision-makers, including:
- **9.57%** Conversion Rate
- **219.01** Average Order Value
- **25.72%** Engagement Rate
- **15.21%** Drop-Off Percentage
- Conversion rate trend over time (Jan 2023 – Jul 2025)
- Funnel breakdown: VIEW → CLICK → DROP-OFF → PURCHASE
- Session distribution: Home Page vs. Product Page vs. Total Visits

### 2. Marketing & Engagement
Product-level marketing performance analysis:
- **8M** Total Views · **43.36K** Total Revenue · **198** Purchases
- CTR comparison across all products (top performers: Baseball Glove 22.37%, Yoga Mat 22.12%)
- Conversion Rate Efficiency scatter plot (Views vs. Conversion Rate by product)
- Products Attractiveness: side-by-side revenue vs. engagement bar chart
- Detailed table: ProductName · ContentType · Likes · CTR · Score

### 3. Product Quality & Customer Voice
Customer sentiment and product quality metrics:
- Rating matrix by product tier (Budget · Mid-Range · Premium)
- Customer review table with ratings and review text
- Rating distribution donut chart (ratings 1–5)
- Geographic distribution map across European markets
- Sankey-style cross-filter: Country × ProductName × Gender

---
## Dashboard Screenshots (Click to enlarge) :
<img src="https://github.com/Ammar-yasser-DataAnalysis/EasyShop-Analytics-Dashboard/blob/main/Executive%20Overview.png">
<img src="https://github.com/Ammar-yasser-DataAnalysis/EasyShop-Analytics-Dashboard/blob/main/Marketing%20%26%20Engagement.png">
<img src="https://github.com/Ammar-yasser-DataAnalysis/EasyShop-Analytics-Dashboard/blob/main/Product%20Quality%20%26%20Customer%20Voice.png">
<img src="https://github.com/Ammar-yasser-DataAnalysis/EasyShop-Analytics-Dashboard/blob/main/Model.png">
```

## 📁 Repository Structure

```
EasyShop-Analytics-Dashboard/
│
├── README.md
├── EasyShop.pbix                  # Power BI dashboard file
├── SQL/
│   ├── 01_restore_backup.sql      # Restore .bak file script
│   ├── 02_data_cleaning.sql       # Full cleaning pipeline
│   └── 03_views_for_powerbi.sql   # Optimized views for PBI connection
├── Screenshots/
│   ├── 00_landing.png
│   ├── 01_executive_overview.png
│   ├── 02_marketing_engagement.png
│   └── 03_product_quality.png
└── Docs/
    └── data_dictionary.md         # Column definitions and business logic
```

---
## 🔎 Project Insights

* **Funnel Optimization Opportunities:** The analysis reveals a **15.21% Drop-Off rate** occurring between the "Click" and "Purchase" stages, suggesting potential friction in the checkout process or shipping cost concerns that need addressing to capitalize on existing traffic.
* **High-Performing Assets:** Sports and lifestyle products like the **Baseball Glove (22.37% CTR)** and **Yoga Mat (22.12% CTR)** have emerged as top performers, identifying them as primary candidates for featured marketing campaigns and inventory prioritization.
* **Product Tier Satisfaction:** By analyzing the rating matrix, it's evident that while budget products drive high volume, the **Mid-Range and Premium tiers** maintain the most stable customer satisfaction scores, providing a clear roadmap for long-term customer retention strategies.
* **Geographic Trends:** Real-time mapping across European markets shows distinct purchasing patterns by country and gender, allowing for highly localized and personalized marketing spend.

---

## ⭐ Final Conclusion

The **EasyShop Analytics Dashboard** provides a holistic bridge between raw e-commerce logs and strategic business growth. By centralizing marketing, sales, and customer feedback into a single **Star Schema** relational model, the project demonstrates how data-driven decisions—such as focusing on high-CTR products or fixing funnel leaks—can directly impact the bottom line. 

This solution is fully scalable, utilizing optimized DAX measures and a clean data pipeline, making it ready to incorporate real-time data streams for ongoing business monitoring and performance tracking.

---

## 👥 Team

Built with ❤️ during the **Orange × Instant Hackathon**.
