
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
* **Scatter Plot:** Discount Sensitivity vs. Profit Margin % by product category 
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
│   ├── Snowflake_Supply_Chain.sql               # Complete Snowflake DDL, staging ETL, and Star Schema script
├── data/
│   └── DataCoSupplyChainDataset_SampleData.csv  # Raw transactional dataset
├── pbix/
│   └── Supply_Chain_BI.pbix                     # Interactive Power BI report file
├── Dashboard_Screenshots/
│   ├── 01_Executive_Overview.png
│   ├── 02_Supply_Chain_Logistics_Performance.png
│   └── 03_Customer_Financial_Deep_Dive.png
└── README.md                                    # Project documentation
```

---

## Author

**Josyula Sai Krishna Priya**  
Data Analyst | Power BI | SQL | Python  
jskp2001@gmail.com  
https://jpriya15.github.io/jpriya15.github.io.portfolio-/

---

*This is a portfolio project built using a publicly available HR dataset to demonstrate People Analytics capabilities.*




