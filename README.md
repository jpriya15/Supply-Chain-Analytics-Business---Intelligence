# Supply Chain Analytics & Business Intelligence Dashboard

Power BI | Snowflake | SQL | Supply Chain Analytics

---

## Project Overview

This project delivers an end-to-end cloud business intelligence and data analytics solution to evaluate retail supply chain operations, shipping efficiency, and sales profitability across global markets. 

Raw multi-table transactional data was loaded and staged in **Snowflake Data Cloud**, modeled into structured dimension and fact views via **SQL**, and connected to **Power BI** for advanced DAX modeling, ETL transformation, and executive dashboard design.

* **Tools Used:** Snowflake, SQL, Power BI Desktop, Power Query (ETL), DAX, Excel
* **Domain:** Supply Chain, Logistics & Sales Analytics
* **Architecture:** Snowflake Data Warehouse $\rightarrow$ Star Schema Modeling $\rightarrow$ Power BI BI Layer

---

## Data Architecture & Engineering (Snowflake & SQL)

* **Data Ingestion & Staging:** Structured CSV order, customer, and shipping data ingested into Snowflake staging tables (`STG_SUPPLY_CHAIN_ORDERS`).
* **Data Modeling (Star Schema):** Modeled dimensional entities using SQL views within Snowflake to optimize querying performance:
  * `FACT_SALES`: Transactional storing orders, net revenue, profit, shipping delays, and line-item metrics.
  * `DIM_DATE`: Centralized calendar dimension with chronological sorting keys (`YearMonthKey`).
  * `DIM_ORDER`: Order status, shipping modes, payment types, and geographical hierarchies.
  * `DIM_PRODUCT`: Product categories, departments, and unit pricing.
  * `DIM_CUSTOMER`: Customer segment profiles and location mappings.

---

## Dataset Description

The dataset contains global order transactions encompassing customer profiles, product hierarchy, shipment timelines, geographic markets, and financial metrics across multi-year sales operations.

* **Key Dimensions & Columns Used:** `Order ID`, `Order Date`, `Shipping Date`, `Delivery Status`, `Shipping Mode`, `Customer Segment`, `Market`, `Order Region`, `Order Country`, `Order State`, `Order City`, `Department Name`, `Category Name`, `Product Name`, `Sales Amount`, `Discount Rate`, `Profit`, `Scheduled Shipping Days`, `Actual Shipping Days`.

---

## Dashboard Pages

### Page 1: Executive Overview
Focuses on high-level commercial growth, sales mix, top-performing product lines, and chronological revenue momentum.
* **KPI Cards:** Total Net Sales ($33.05M), Total Profit ($3.97M), Total Orders (66K), Profit Margin % (12.00%), On-Time Delivery Rate % (45.18%).
* **Donut Chart:** Net Sales distribution across Customer Segments (`Consumer`, `Corporate`, `Home Office`).
* **Horizontal Bar Chart:** Top 10 Products by Revenue.
* **Line & Clustered Column Chart:** Monthly Net Sales and Profit Margin % Trend across a continuous timeline.
* **Slicers:** Year tiles and Global Market tiles.

---

### Page 2: Supply Chain & Logistics Performance
Focuses on operational fulfillment, lead times, scheduled vs. actual delivery performance, and geographic delivery risks.
* **KPI Cards:** Average Actual Shipping Days (3.5), Average Scheduled Shipping Days (2.9), Average Shipping Delay Days (0.6), Late Delivery Risk % (54.82%).
* **Donut Chart:** Order volume breakdown by Delivery Status (`Late delivery`, `Advance shipping`, `Shipping on time`, `Shipping canceled`).
* **Matrix Table with Data Bars:** Regional breakdown comparing Total Orders, Late Delivery Orders, and Late Delivery Risk % across global markets.
* **Clustered Bar Chart:** Actual vs. Scheduled Shipping Days compared across Shipping Modes (`Standard Class`, `Second Class`, `First Class`, `Same Day`).
* **Slicers:** Symmetrical 2x2 grid for `SHIPPING_MODE` and structured list for `ORDER_REGION`.

---

### Page 3: Customer & Financial Deep-Dive
Focuses on product portfolio profitability, regional contribution, and discount sensitivity.
* **Treemap:** Revenue and Profit Contribution across global countries.
* **Scatter Plot:** Discount Sensitivity vs. Profit Margin % by product category (highlighting high-margin vs. margin-diluting discount thresholds).
* **Decomposition Tree:** Interactive root-cause breakdown of Total Profit ($3.97M) across `Department Name` $\rightarrow$ `Category Name` $\rightarrow$ `Product Name`.
* **Slicers:** `DEPARTMENT_NAME` selector and `Order Profit Segment` buttons (`Loss-Making` vs. `Profitable`).

---


## DAX Measures Created

```
Total Net Sales = SUM(FACT_SALES[NET_SALES_AMOUNT])

Total Profit = SUM(FACT_SALES[ORDER_PROFIT])

Profit Margin % = DIVIDE([Total Profit], [Total Net Sales], 0)

Late Delivery Risk % = 
DIVIDE(
    CALCULATE(COUNTROWS(FACT_SALES), FACT_SALES[DELIVERY_STATUS] = "Late delivery"),
    COUNTROWS(FACT_SALES),
    0
)

On-Time Delivery Rate % = 
DIVIDE(
    CALCULATE(COUNTROWS(FACT_SALES), FACT_SALES[DELIVERY_STATUS] IN {"Shipping on time", "Advance shipping"}),
    COUNTROWS(FACT_SALES),
    0
)
```

---

## Repository Structure

```
├── sql/
│   ├── 01_snowflake_staging.sql   # Snowflake DDL and staging ingestion scripts
│   └── 02_star_schema_views.sql   # SQL transformation views (Dimension & Fact tables)
├── data/
│   └── DataCoSupplyChainDataset_SampleData.csv      # Raw transactional dataset
├── pbix/
│   └── Supply_Chain_BI.pbix # Interactive Power BI report file
├── screenshots/
│   ├── 01_executive_overview.png
│   ├── 02_supply_chain_logistics.png
│   └── 03_customer_financial_deep_dive.png
└── README.md                      # Project documentation
---

## Author

**Josyula Sai Krishna Priya**  
Data Analyst | Power BI | SQL | Python  
jskp2001@gmail.com  
https://jpriya15.github.io/jpriya15.github.io.portfolio-/

---

*This is a portfolio project built using a publicly available HR dataset to demonstrate People Analytics capabilities.*




