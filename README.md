# Supply Chain Analytics Dashboard (Power BI)

## Project Overview
Interactive Power BI dashboard built on the DataCo Global Supply Chain dataset (180,519 orders).
Transforms a single flat CSV into a structured star schema model with actionable insights
on delivery risk and profitability across shipping modes, regions, and product categories.

---

## Business Questions
1. Which shipping modes carry the highest late delivery risk — and is premium shipping worth it?
2. How does profit margin vary across product categories and regions?
3. Where should supply chain managers focus to reduce delivery failures without sacrificing margin?

---

## Key Findings
- **First Class shipping has a 95% late delivery rate** despite being a premium option —
  the tightest delivery windows are the hardest to meet
- **Standard Class is the most reliable mode at 38% late rate**, outperforming even Same Day (46%)
- **Overall profit margin is 11%**, ranging from 17% (Golf Bags & Carts) to 0.6%
  (Strength Training) across 40+ categories
- **Regional late delivery rates are consistently high (49–58%)** with minimal variation,
  suggesting a systemic operational issue rather than a regional one

---

## Data Model (Star Schema)
Built in Power Query before loading into Power BI:

| Table | Key Columns |
|---|---|
| Fact_Orders | Order Id, Item Id, Customer Id, Product Id, Dates, Sales, Profit, Late_delivery_risk |
| Dim_Customer | Customer Id, Segment, City, Country |
| Dim_Product | Product Card Id, Product Name, Category Name |
| Dim_Date | Date, Month, Quarter, Year (DAX calendar table) |

Relationships: all many-to-one from Fact_Orders to dimension tables.
Cross-filter direction: single throughout.

---

## DAX Measures
```dax
Total Orders = COUNTROWS(Fact_Orders)
Late Orders = CALCULATE(COUNTROWS(Fact_Orders), Fact_Orders[Late_delivery_risk] = 1)
Late Delivery Rate = DIVIDE([Late Orders], [Total Orders])
Total Profit = SUM(Fact_Orders[Benefit per order])
Total Sales = SUM(Fact_Orders[Sales])
Profit Margin % = DIVIDE([Total Profit], [Total Sales])
```

---

## Dashboard Pages

### 1. Executive Summary
Static overview page — no slicers. KPI cards (Total Orders, Sales, Profit, Late Rate),
top-line charts, and 3 written business insights for decision-maker consumption.

### 2. Late Delivery Risk
Late delivery rate by shipping mode and order region. Slicers: Shipping Mode,
Order Region, Delivery Status, Date range.

### 3. Profit/Margin Analysis
Profit margin by region, Top 10 and Bottom 5 product categories, customer segment breakdown.
Slicers: Shipping Mode, Order Region, Category Name, Customer Segment, Date range.

---

## Dashboard Preview

### Executive Summary
![Executive Summary](Summary.png)

### Late Delivery Risk
![Late Delivery Risk](Late_Delivery_Risk.png)

### Profit/Margin Analysis
![Profit Margin Measures](Profit_Margin_Measures.png)

---

## Tools & Technologies
- Power BI Desktop
- Power Query (ETL and table splitting)
- DAX (measures, calendar table)
- Star Schema data modeling
- Microsoft Excel

---

## Repository Contents
- `Supply_Chain_Analytics_Dashboard.pbix`
- `DataCoSupplyChainDataset.zip`
- `Summary.png`
- `Late_Delivery_Risk.png`
- `Profit_Margin_Measures.png`
- `README.md`

---

## Future Improvements
- Predictive late delivery model (Python/ML integration)
- Inventory optimization layer
- Real-time refresh via Power BI Service
- Mobile-optimized executive view

---

## Author
**Mahmoud Shiri
Supply Chain & Procurement professional with MSc degrees and expertise in
logistics, sourcing, and supply chain analytics.

LinkedIn: linkedin.com/in/mahmoud-shiri
