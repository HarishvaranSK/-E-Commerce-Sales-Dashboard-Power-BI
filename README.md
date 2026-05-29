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

## # 🧠 DAX Measures — E-Commerce Sales Dashboard

All DAX measures used in this Power BI project, organized by category.

---

## 📅 Calendar Table

```dax
-- Dynamic Calendar Table (start to end from order data)
Calendar = CALENDAR(
    MIN('E-Commerce Data'[Order Date]),
    MAX('E-Commerce Data'[Order Date])
)

-- Year Column
Year = YEAR('Calendar'[Calendar Date])

-- Month Name Column
Month = FORMAT('Calendar'[Calendar Date], "MMMM")

-- Month Number Column (for sorting)
Month Number = MONTH('Calendar'[Calendar Date])
```

---

## 💰 Sales Measures

```dax
-- Year to Date Sales
YTD Sales = 
TOTALYTD(
    SUM('E-Commerce Data'[Sales Per Order]),
    'Calendar'[Calendar Date]
)

-- Previous Year to Date Sales
Previous YTD Sales = 
CALCULATE(
    SUM('E-Commerce Data'[Sales Per Order]),
    DATESYTD(
        SAMEPERIODLASTYEAR('Calendar'[Calendar Date])
    )
)

-- Year on Year Sales Growth %
YoY Sales = 
DIVIDE(
    [YTD Sales] - [Previous YTD Sales],
    [Previous YTD Sales]
)
```

---

## 💵 Profit Measures

```dax
-- Year to Date Profit
YTD Profit = 
TOTALYTD(
    SUM('E-Commerce Data'[Profit Per Order]),
    'Calendar'[Calendar Date]
)

-- Previous Year to Date Profit
Previous YTD Profit = 
CALCULATE(
    SUM('E-Commerce Data'[Profit Per Order]),
    DATESYTD(
        SAMEPERIODLASTYEAR('Calendar'[Calendar Date])
    )
)

-- Year on Year Profit Growth %
YoY Profit = 
DIVIDE(
    [YTD Profit] - [Previous YTD Profit],
    [Previous YTD Profit]
)
```

---

## 📦 Quantity Measures

```dax
-- Year to Date Quantity
YTD Quantity = 
TOTALYTD(
    SUM('E-Commerce Data'[Order Quantity]),
    'Calendar'[Calendar Date]
)

-- YTD Quantity with # symbol (custom format)
YTD Concatenated Quantity = 
CONCATENATE(
    "#",
    FORMAT(
        DIVIDE([YTD Quantity], 1000),
        "0.0"
    ) & "K"
)

-- Previous Year to Date Quantity
Previous YTD Quantity = 
CALCULATE(
    SUM('E-Commerce Data'[Order Quantity]),
    DATESYTD(
        SAMEPERIODLASTYEAR('Calendar'[Calendar Date])
    )
)

-- Year on Year Quantity Growth %
YoY Quantity = 
DIVIDE(
    [YTD Quantity] - [Previous YTD Quantity],
    [Previous YTD Quantity]
)
```

---

## 📊 Profit Margin Measures

```dax
-- Profit Margin %
Profit Margin = 
DIVIDE(
    SUM('E-Commerce Data'[Profit Per Order]),
    SUM('E-Commerce Data'[Sales Per Order])
)

-- Year to Date Profit Margin
YTD Profit Margin = 
TOTALYTD(
    [Profit Margin],
    'Calendar'[Calendar Date]
)

-- Previous Year to Date Profit Margin
Previous YTD Profit Margin = 
CALCULATE(
    [Profit Margin],
    DATESYTD(
        SAMEPERIODLASTYEAR('Calendar'[Calendar Date])
    )
)

-- Year on Year Profit Margin Growth %
YoY Profit Margin = 
DIVIDE(
    [YTD Profit Margin] - [Previous YTD Profit Margin],
    [Previous YTD Profit Margin]
)
```

---

## 🔺 Dynamic Icons (Trend Arrows)

```dax
-- Sales Trend Icon
Sales Icon = 
VAR positive_icon = UNICHAR(9650)   -- ▲ Up Arrow
VAR negative_icon = UNICHAR(9660)   -- ▼ Down Arrow
VAR result = IF([YoY Sales] > 0, positive_icon, negative_icon)
RETURN result

-- Profit Trend Icon
Profit Icon = 
VAR positive_icon = UNICHAR(9650)
VAR negative_icon = UNICHAR(9660)
VAR result = IF([YoY Profit] > 0, positive_icon, negative_icon)
RETURN result

-- Quantity Trend Icon
Quantity Icon = 
VAR positive_icon = UNICHAR(9650)
VAR negative_icon = UNICHAR(9660)
VAR result = IF([YoY Quantity] > 0, positive_icon, negative_icon)
RETURN result

-- Profit Margin Trend Icon
Profit Margin Icon = 
VAR positive_icon = UNICHAR(9650)
VAR negative_icon = UNICHAR(9660)
VAR result = IF([YoY Profit Margin] > 0, positive_icon, negative_icon)
RETURN result
```

---

## 🎨 Dynamic Background Colors (Conditional Formatting)

```dax
-- Sales Background Color
Sales Color = 
IF([YoY Sales] > 0, "Green", "Red")

-- Profit Background Color
Profit Color = 
IF([YoY Profit] > 0, "Green", "Red")

-- Quantity Background Color
Quantity Color = 
IF([YoY Quantity] > 0, "Green", "Red")

-- Profit Margin Background Color
Profit Margin Color = 
IF([YoY Profit Margin] > 0, "Green", "Red")
```

---

## 📌 Key DAX Functions Used

| Function | Purpose |
|---|---|
| `TOTALYTD` | Calculates year-to-date value |
| `SAMEPERIODLASTYEAR` | Returns same period from previous year |
| `DATESYTD` | Returns year-to-date dates |
| `CALCULATE` | Modifies filter context |
| `DIVIDE` | Safe division (avoids divide by zero) |
| `UNICHAR` | Adds special characters (arrows) |
| `FORMAT` | Custom number formatting |
| `CONCATENATE` | Combines text values |
| `IF` | Conditional logic |
| `VAR / RETURN` | Variables for cleaner DAX |
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
