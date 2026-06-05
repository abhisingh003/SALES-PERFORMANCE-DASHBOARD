# 📊 Sales Performance Dashboard

## Overview

The Sales Performance Dashboard is an interactive Business Intelligence solution developed using Microsoft Power BI. The dashboard helps management monitor sales performance, profitability, regional contribution, manager effectiveness, target achievement, and operational risks through intuitive visualizations and KPI tracking.

The purpose of this dashboard is to transform raw business data into actionable insights that support strategic decision-making.

---

# Business Problem

Organizations often struggle to monitor performance across multiple regions, managers, and product categories. Without a centralized reporting solution, identifying growth opportunities and performance gaps becomes difficult.

This dashboard addresses these challenges by providing:

- Executive-level performance monitoring
- Regional and category analysis
- Manager accountability tracking
- Target achievement monitoring
- Operational risk identification

---

# Dashboard Pages

## 1️⃣ Executive Overview

Provides a high-level summary of business performance.

### Key Metrics

- Total Sales
- Total Profit
- Total Orders
- Sales Growth %
- Profit Growth %

### Visualizations

- Monthly Sales Trend
- Sales by Region
- Sales by Category
- Executive Summary
- Key Business Insights

### Business Questions Answered

- Is the business growing?
- Which regions generate the most revenue?
- Which categories contribute the most sales?
- How are sales and profits performing over time?

---

## 2️⃣ Manager Performance

Focuses on manager-level accountability and performance.

### Visualizations

- Manager Performance Table
- Sales by Manager
- Profit by Manager
- Manager vs Region Matrix

### Business Questions Answered

- Which manager generates the highest sales?
- Which manager contributes the most profit?
- How does performance vary across regions?

---

## 3️⃣ Risk & Target Analysis

Analyzes business risks and performance against targets.

### Visualizations

- Sales vs Target Comparison
- Target Achievement %
- Returns Analysis
- Delivery Delay Analysis
- Recommended Actions

### Business Questions Answered

- Are sales targets being achieved?
- Which areas require management attention?
- What operational risks impact performance?

---

# Dataset Information

The project uses four datasets:

### Orders

Contains transaction-level sales data including:

- Order ID
- Order Date
- Ship Date
- Customer Details
- Sales
- Profit
- Category
- Region
- Quantity

### People

Contains:

- Region
- Regional Manager

### Returns

Contains:

- Returned Orders

### Target

Contains:

- Category-wise Sales Targets
- Year-wise Targets

---

# Data Modeling

### Relationships

| Source Table | Column | Target Table | Column |
|-------------|---------|--------------|---------|
| Orders | Region | People | Region |
| Orders | Category | Target | Category |
| Calendar | Date | Orders | Order Date Actual |

---

# Date Conversion

Original date values were stored as Excel serial numbers.

Example:

```
42195
42336
```

Converted using DAX:

```DAX
Order Date Actual =
DATE(1899,12,30) + Orders[Order Date]
```

```DAX
Ship Date Actual =
DATE(1899,12,30) + Orders[Ship Date]
```

---

# Calendar Table

```DAX
Calendar =
CALENDAR(
MIN(Orders[Order Date Actual]),
MAX(Orders[Order Date Actual])
)
```

### Year Column

```DAX
Year =
YEAR(Calendar[Date])
```

### Month Column

```DAX
Month =
FORMAT(Calendar[Date],"MMM")
```

---

# DAX Measures

## Total Sales

```DAX
Total Sales =
SUM(Orders[Sales])
```

## Total Profit

```DAX
Total Profit =
SUM(Orders[Profit])
```

## Total Orders

```DAX
Total Orders =
DISTINCTCOUNT(Orders[Order ID])
```

## Target Sales

```DAX
Target Sales =
SUM(Target[Sales Target])
```

## Target Achievement %

```DAX
Target Achievement % =
DIVIDE(
[Total Sales],
[Target Sales]
)
```

## Sales Previous Year

```DAX
Sales PY =
CALCULATE(
[Total Sales],
SAMEPERIODLASTYEAR(Calendar[Date])
)
```

## Sales Growth %

```DAX
Sales Growth % =
DIVIDE(
[Total Sales]-[Sales PY],
[Sales PY]
)
```

## Profit Previous Year

```DAX
Profit PY =
CALCULATE(
[Total Profit],
SAMEPERIODLASTYEAR(Calendar[Date])
)
```

## Profit Growth %

```DAX
Profit Growth % =
DIVIDE(
[Total Profit]-[Profit PY],
[Profit PY]
)
```

## Delivery Days

```DAX
Delivery Days =
DATEDIFF(
Orders[Order Date Actual],
Orders[Ship Date Actual],
DAY
)
```

---

# Key Insights

- Technology is one of the highest-performing categories.
- Sales performance varies significantly across regions.
- Profitability trends differ from sales growth trends.
- Certain categories require improvement in target achievement.
- Operational metrics such as returns and delivery delays require monitoring.

---

# Recommendations

1. Improve performance in underperforming categories.
2. Monitor category-wise target achievement regularly.
3. Reduce delivery delays to improve customer satisfaction.
4. Analyze return trends to identify root causes.
5. Promote best practices from high-performing managers.

---

# Tools & Technologies

- Microsoft Power BI Desktop
- Power Query
- DAX (Data Analysis Expressions)
- Data Modeling
- Data Visualization

---

# Project Structure

```
Sales-Performance-Dashboard/
│
├── README.md
├── Sales_Performance_Dashboard.pbix
├── Dataset/
│   ├── Orders.csv
│   ├── People.csv
│   ├── Returns.csv
│   └── Target.csv
│
└── Screenshots/
    ├── Executive_Overview.png
    ├── Manager_Performance.png
    └── Risk_Analysis.png
```

---

# Author

**Abhishek Singh**

Sales Performance Dashboard using Microsoft Power BI

---

## Dashboard Objective

Transform raw sales data into meaningful business insights that help management understand performance, identify opportunities, and make data-driven decisions.
