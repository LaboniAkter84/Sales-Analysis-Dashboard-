# Sales_Analysis_Dashboard
An end-to-end Power BI dashboard that analyzes global bike & accessories sales data across customers, products, regions, and time — built to uncover revenue drivers, profitability gaps, customer value, and return-rate risk.

## Dashboard Preview
Live Power BI (Fabric) Link: **[View Live Power BI Dashboard](https://app.powerbi.com/links/nA4WHfC9nM?ctid=3cd07988-5263-4064-ad55-e956ab3dd117&pbi_source=linkShare&bookmarkGuid=d7023ad9-4c19-4043-bb16-006cdfde7a0a)**


## Project Overview
This project is an interactive business intelligence report analyzing global bike and accessories sales performance, built on a three-year (2020–2022) transactional dataset covering customers, products, returns, and territories.

The report is designed to support commercial decision-making by presenting revenue, profitability, customer value, and geographic performance in a single, explorable dashboard. It combines a company-wide overview with focused deep-dives into regional performance, customer segmentation, and product-category profitability, consistently connecting how much revenue is generated with how profitable and how risky (returns) that revenue actually is.

Built entirely in Power BI, the project covers the full analytics workflow: data extraction and transformation via Power Query, a hybrid star–snowflake data model connecting eight tables, custom DAX measures for revenue/cost/profit, and a four-page report with a consistent global KPI header and cross-page navigation.

## Problem Statement
The business had raw transactional data spread across multiple disconnected tables (orders, returns, products, customers, territories) with no centralized way to track performance or make investment decisions. Assessing where the business is actually winning and losing money requires synthesizing order-level sales, return behavior, customer demographics, and geography — information that is typically scattered across separate exports, inconsistent in format, and difficult to interpret without dedicated analysis.


## Objectives
- Consolidate sales, returns, customer, product, and territory data into a single relational data model.
- Present company-wide performance (Revenue, COGS, Profit, Profit %, Order Qty) alongside page-level drill-downs for immediate context.
- Analyze the relationship between revenue and profitability at the product-category level to surface hidden margin differences.
- Track geographic performance and return-rate risk by continent, country, and region.
- Evaluate customer-segmentation logic against actual revenue contribution.
- Deliver the analysis as an interactive, explorable report rather than a static summary, enabling stakeholders to drill into the specific view most relevant to their decision-making.

## Skills, Tools & Technologies

### Skills

- Data Modeling (Hybrid Star–Snowflake Schema)
- DAX (Measures, calculated columns, time intelligence)
- Data Cleaning & Transformation (ETL)
- Data Visualization
- Business/Commercial Analysis

### Tools

- Power BI Desktop
- Power BI Fabric (publish + share link)
- Power Query


### Techniques

- Conditional formatting
- KPI cards
- Toggle-driven metric switching (Revenue/Profit/Order Qty/Cost)
- Correlation between revenue and margin
- Geographic mapping

## Datasets

The dataset is provided as individual CSV files inside the Adventure Work All Table Dataset folder (rather than a single zip), so each table is directly browsable and previewable on GitHub, and any future update to one table shows up as a clean diff instead of re-uploading a whole archive.
https://github.com/LaboniAkter84/Sales-Analysis-Dashboard-/tree/main/Adventure%20Work%20All%20Table%20Dataset


## Data Preparation & Modeling
### ETL

Data preparation was handled entirely in Power Query before loading into the model.

Fact tables — Sales_Data and Returns_Data were cleaned by standardizing data types (dates, currency, whole numbers), removing blank/duplicate rows, and correcting inconsistent text (e.g., product color casing).

Dimension/lookup tables — Customer_Lookup, Product_Lookup, Product_Subcategories_Lookup, Product_Categories_Lookup, and Territory_Lookup were cleaned and type-corrected, then loaded into the model. A dedicated Calendar table was built (instead of relying on Power BI's auto date/time) to enable proper Year/Quarter time intelligence.

### Data Modeling

The model combines **both star and snowflake patterns**, depending on the dimension:

**Star-schema dimensions** (connect directly to the fact tables, 1-to-many):

- Customer_Lookup → Sales_Data
- Territory_Lookup → Sales_Data and Returns_Data
- Calendar → Sales_Data and Returns_Data (drives all time intelligence)
- Product_Lookup → Sales_Data and Returns_Data

**Snowflaked dimension** (normalized into multiple linked lookup tables rather than flattened into one):

- Product_Categories_Lookup → Product_Subcategories_Lookup → Product_Lookup
- CategoryName doesn't connect to the fact tables directly — it flows through Subcategory, then Product, before reaching Sales/Returns data, which is the defining trait of a snowflake structure.

So the overall design is a hybrid star–snowflake schema: Customer, Territory, and Calendar follow the classic star pattern with direct links to the facts, while the product hierarchy is snowflaked into three normalized tables (Category → Subcategory → Product). This keeps the product hierarchy clean and non-redundant (no repeated category/subcategory text on every product row) while keeping the rest of the model simple and fast to query.

Key DAX measures built on top of this model include Total Revenue, Total COGS, Total Profit, Profit %, Total Order Qty, and Return Rate, used consistently across all four pages.

 **Data Model Screenshot**

<img width="1307" height="792" alt="Data Modeling" src="https://github.com/user-attachments/assets/c376c090-172f-408d-867b-116d3170b620" />

## Dashboard & Insights

Every page shares the same global KPI header — Total Revenue $24.91M, Total COGS $14.46M, Total Profit $10.46M, Profit % 41.97%, Total Order Qty 84.17K, Total Customers 18,148 — plus a top navigation bar (Home / Map / Customer / Product), so the report reads as one connected story rather than four separate charts.

### 1. Home

<img width="1432" height="801" alt="Home page" src="https://github.com/user-attachments/assets/e68f4bfc-49f9-4b6d-bb77-ce3e1439feb2" />


**Revenue by Year and Quarter:** Revenue holds fairly flat through 2020–2021, then inflects sharply upward starting Q3 2021 and continues climbing into Q1–Q2 2022 — a clear recent growth phase worth investigating for its underlying driver (new markets, seasonality, or a product push).

**Subcategory Performance:** (Revenue / COGS / Profit / Profit %). Helmets lead both revenue ($205.8K) and margin (63.66%), followed by Fenders, Vests, Bike Racks, Cleaners, and Bike Stands, which cluster tightly around a consistent ~62.6% margin — a remarkably stable accessory subcategory once bikes are excluded.

**Revenue by Gender:** An almost even split — Female 50.23%, Male 49.14%, 0.63% unclassified — showing the customer base isn't gender-skewed, so marketing doesn't need to over-index on one gender.

**Revenue by Product Color:** Black dominates at 7.9M, nearly double the next color (Red, 4.9M), followed by Yellow (4.6M) and Silver (4.4M), with Blue, NA, Multi, and White trailing far behind — a direct signal for inventory and purchasing to prioritize the top four colors.

**Return Rate by Occupation** Manual workers return products at by far the highest rate (62.30%), well ahead of Clerical (46.02%), Management (41.74%), Skilled Manual (30.70%), and Professional (23.07%, the lowest). Return-reduction efforts — better sizing guides, clearer product descriptions, fit tools — should be targeted at the Manual and Clerical segments first.

### 2. Map

<img width="1431" height="804" alt="Mag Images" src="https://github.com/user-attachments/assets/95687462-0a04-4e12-9150-e3239e678965" />


**Revenue by Region:** An interactive map plots revenue across North America (Northwest, Southwest, Northeast, Southeast, Central), Europe (UK, France, Germany), and the Pacific (Australia), with metric toggles (Revenue/Profit/Order Qty/Cost) and geography-level toggles (Continent/Country/Region) so the same map supports exploration at any zoom level.

**Growth Momentum — YOY Trend by Continent:** All three continents start close together in 2020, but by 2022 Europe has overtaken North America as the fastest-growing continent, while the Pacific region grows the slowest and lags noticeably by 2022 — flagging Europe as the current growth engine and Pacific as an underperforming region worth investigating.

**Where Revenue Is Leaking:** Return Rate by Country. The United States leads in revenue (7.9M) but also carries a comparatively high return rate, while the UK's return rate spikes even though its revenue (2.9M) is far lower — a signal that the UK market may have a disproportionate returns problem worth a dedicated regional audit (sizing, shipping damage, or product-market fit).

### 3. Customer

<img width="1429" height="807" alt="Customer page" src="https://github.com/user-attachments/assets/44c8f0aa-776d-42a4-b099-cb503b599ee5" />


**Cost-to-Serve Matrix:** A first-name-level breakdown of Revenue/Profit/Order Qty/Cost across 2020, 2021, and 2022 with running totals, answering "which customers cost the most to serve over time?" — letting analysts spot high-cost or declining customers year over year rather than relying on one aggregated number.

**Top 5 Customers by Revenue:** The top spenders — Ian (128K), Morgan (125K), Chloe (119K), Seth (115K), and Kaitlyn (113K) — are tightly clustered, showing revenue concentration isn't dangerously dependent on a single "whale" customer, but does point to a small VIP cohort worth a dedicated retention strategy.

**Total Revenue by Customer Priority:** This is the most counter-intuitive finding in the whole report: customers labeled "Average" priority generate the most revenue (12M), followed by "Low" (9M), while "High" (3M) and "High Value" (1M) tiers generate the least revenue. This strongly suggests the current customer-priority labeling is misaligned with actual revenue contribution, and the business may be under-investing attention in its true top-revenue segment while over-prioritizing a small "High Value" tag that isn't actually the most valuable.

### 4. Product

<img width="1431" height="805" alt="Product page" src="https://github.com/user-attachments/assets/c60561c0-56e4-4b3a-885a-5f70f91b9203" />


**Product Profitability:** A year-by-year (2020/2021/2022) profit breakdown by product name. Mountain-200 Black, 46 leads at $571.6K total profit, with the rest of the Mountain-200 line filling out the top ranks, followed by the Road-250 series.

**Top Selling Category by Revenue:** Bikes overwhelmingly dominate revenue at 24M, dwarfing Accessories (1M) and Clothing (0M) — bikes are clearly the core product line driving the business.

**Profit % by Category:** This is the nuance that balances the chart above: despite bikes generating the most revenue, Accessories actually carries the highest profit margin (42.39%), followed by Clothing (29.86%), with Bikes the lowest of the three (27.75%). This is a critical strategic insight — the business should consider bundling and upselling accessories with every bike sale, since accessories are both an easy attach-sale and meaningfully more profitable per dollar of revenue.







