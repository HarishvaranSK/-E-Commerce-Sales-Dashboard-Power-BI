# -E-Commerce-Sales-Dashboard-Power-BI
Power BI Dashboard analyzing E-Commerce sales, profit &amp; regional performance using DAX &amp; Power Query
# 🛒 E-Commerce Sales Dashboard | Power BI

![Dashboard]("C:\Users\PHOENIX\Videos\Screen Recordings\Screen Recording 2025-06-16 110132.mp4")

## 📌 Project Overview

This project is an end-to-end **E-Commerce Sales Analytics Dashboard** built in Power BI.
The goal was to analyze sales performance, profitability, and customer behavior for an e-commerce retail store — and turn raw data into actionable business insights.

---

## Business Problem

The management team needed answers to these key questions:
- How are we performing this year compared to last year?
- Which product categories and regions are driving profit?
- Which products are our top performers and which are underperforming?
- How do different customer segments (Consumer, Corporate, Home Office) behave?

---

## Dashboard Features

| Feature | Description |
|---|---|
| **YTD KPI Cards** | Year-to-date Sales, Profit, Quantity & Profit Margin |
| **YoY Comparison** | Year-over-Year growth tracking with trend indicators |
| **Sales by Category** | Furniture, Office Supplies, Technology breakdown |
| **Top 5 Products** | Highest revenue generating products |
| **Bottom 5 Products** | Lowest performing products for business review |
| **Sales by Region** | Regional breakdown — East, West, Central, South |
| **Map Visual** | State-level sales distribution across the US |
| **Segment Filter** | Dynamic filtering by Consumer / Corporate / Home Office |

---

## Tools & Technologies

- **Power BI Desktop** — Dashboard building & visualization
- **Power Query** — Data cleaning & transformation
- **DAX** — Calculated measures & KPIs
- **Data Modeling** — Star schema with Fact & Dimension tables

---

## DAX Measures Used

```dax
Total Sales = SUM(Orders[Sales])

Total Profit = SUM(Orders[Profit])

Profit Margin % = DIVIDE([Total Profit], [Total Sales])

Total Orders = COUNTROWS(Orders)

YoY Sales Growth = 
DIVIDE(
    [Total Sales] - CALCULATE([Total Sales], SAMEPERIODLASTYEAR(Dates[Date])),
    CALCULATE([Total Sales], SAMEPERIODLASTYEAR(Dates[Date]))
)
```

---

## 💡 Key Insights

- 📈 **YTD Sales grew 1%** compared to previous year
- 💰 **Profit increased by 13%** YoY showing improved margins
- 📦 **Office Supplies** is the highest revenue category at $1.21M
- ⚠️ **Quantity sold dropped by 9%** — needs further investigation
- 🗺️ **East and West regions** contribute equally at 6% each
- 🏆 **Easy-staple paper** is the top performing product at $19K

---

## 📂 Dataset

- **Source:** Superstore Sales Dataset
- **Link:** [Kaggle - Superstore Dataset](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)
- **Records:** 9,994 orders
- **Period:** 2019 - 2022

---

## 🚀 How to Open This Project

1. Download and install [Power BI Desktop](https://powerbi.microsoft.com/en-us/downloads/) (Free)
2. Clone or download this repository
3. Open the `.pbix` file in Power BI Desktop
4. Explore the dashboard and interact with filters!

---

## 📁 Repository Structure

```
E-Commerce-Sales-Dashboard/
│
├── README.md
├── E-Commerce-Sales-Dashboard.pbix
├── Dataset/
│   └── superstore_data.csv
├── Screenshots/
│   └── dashboard.png
└── DAX-Measures/
    └── measures.md
```

---

## 👨‍💻 About Me

**Harishvaran S K** — Aspiring Data Analyst

Passionate about turning raw data into meaningful business insights.
Currently building my Data Analytics portfolio with Power BI, Tableau, SQL & Python.

---

## 📜 License

This project is open source and available for learning purposes.

---

⭐ If you found this project helpful, please give it a star!
```
