# FUTURE_DS_01
Repository for Task 1 of the Data Science &amp; Analytics Internship at Future Interns
# Superstore Sales Analysis Dashboard

<img width="1473" height="824" alt="Dashboard 1" src="https://github.com/user-attachments/assets/854393c9-48d8-4572-83b7-cdca3ffc062b" />

<img width="1472" height="828" alt="Dashboard 2" src="https://github.com/user-attachments/assets/abfda3e8-0235-495c-8798-c4c119ab88d2" />

<img width="1468" height="828" alt="Dashboard 3" src="https://github.com/user-attachments/assets/ca3ee748-5141-4b62-bceb-c4e0e21a4298" />

# Overview

## Business Objective

The objective of this analysis was to evaluate Superstore’s sales performance across products, categories, regions, and time periods. The dashboard was designed to help stakeholders identify bestselling products, understand seasonal sales and profit trends, and determine which categories and regions contribute most to overall revenue and profitability.

## Data Overview

The analysis is based on historical Superstore order-level sales data from 2011 to 2014, including information on sales, profit, quantity, discounts, product categories, customer segments, regions, and order dates. The data was cleaned and transformed to support accurate time-based and performance analysis.

## Tools Used

* Microsoft Excel: Data Source.
* Microsoft Power BI: Data Cleaning, Transformation & Visualisation.

## Key Performance Indicators (KPIs) & DAX Formulas Used for Each

* Total Sales: $ 2,297K
```DAX
Total Sales = SUM(Orders[Sales])
```
* Total Profit: $ 286K
```DAX
Total Profit = SUM(Orders[Profit])
``` 
* Profit Margin: 12%
```DAX
Profit Margin % = DIVIDE(Orders[Total Profit],Orders[Total Sales],0)
```
* Total Quantity Ordered: 38K
```DAX
Total Quantity = SUM(Orders[Quantity])
```
* Total Orders: 5K
```DAX
Total Orders = DISTINCTCOUNT(Orders[Order ID])
```
* Average Order Value: $ 0.46K
```DAX
Average Order Value = DIVIDE(Orders[Total Sales],Orders[Total Orders],0)
```
* Average Discount: 15.62%
```DAX
Average Discount = AVERAGE(Orders[Discount])
```
* Most Selling Region: West
```DAX
Most Selling Region = 
VAR RegionTable =
    SUMMARIZE (
        Orders,
        Orders[Region],
        "RegionSales", [Total Sales]
    )
RETURN
    MAXX (
        TOPN ( 1, RegionTable, [RegionSales], DESC ),
        Orders[Region]
    )
```
* Worst Profitable Region: Central
```DAX
Worst Profitable Region = 
VAR RegionTable =
    SUMMARIZE (
        Orders,
        Orders[Region],
        "RegionProfit", [Total Profit]
    )
RETURN
    CONCATENATEX (
        TOPN ( 1, RegionTable, [RegionProfit], ASC ),
        Orders[Region]
    )
```

## Other DAX Formulas Used for Calculated Columns

### 1. Order Year
```DAX
Order Year = YEAR(Orders[Order Date])
```

### 2. Month Year
```DAX
Month Year = FORMAT(Orders[Order Date], "MMM YYYY")
```

### 3. Order Month
```DAX
Order Month = FORMAT(Orders[Order Date], "MMM")
```

### 4. Order Month No.
```DAX
Order Month No. = MONTH(Orders[Order Date])
```

## Key Insights

* Sales show strong seasonality, with a clear upward trend toward the end of the year. November 
and December are the highest-performing months, indicating peak demand during the holiday 
season.
* The Consumer segment dominates sales, contributing over 50% of total revenue, while 
Corporate and Home Office segments together account for the remaining share.
* Technology is the highest revenue-generating category ($ 836K) and also delivers the highest 
profit ($ 145K), making it the strongest overall performer.
* Furniture generates high sales but significantly lower profit, contributing only $ 18K in profit 
despite substantial revenue, indicating margin pressure within this category.
* Sub-category analysis reveals concentrated revenue drivers: 
➢ Phones lead all sub-categories with approximately $ 330K in sales, making them the 
single most important revenue contributor. 
➢ Chairs follow closely with around $ 328K in sales, highlighting strong demand within the 
Furniture category despite lower overall profitability. 
➢ Storage ($ 224K) and Binders ($ 203K) are the top-performing Office Supplies sub
categories, indicating consistent demand for operational essentials. 
➢ Accessories and Copiers are notable Technology sub-categories, contributing 
significant sales while supporting the category’s strong profit performance. 
