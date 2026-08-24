# Sales_Analysis_Dashboard
An end-to-end Power BI dashboard that analyzes global bike & accessories sales data across customers, products, regions, and time — built to uncover revenue drivers, profitability gaps, customer value, and return-rate risk.

## Dashboard Preview
Live Power BI (Fabric) Link: https: https://app.powerbi.com/links/nA4WHfC9nM?ctid=3cd07988-5263-4064-ad55-e956ab3dd117&pbi_source=linkShare&bookmarkGuid=d7023ad9-4c19-4043-bb16-006cdfde7a0a

## Project Overview
This project is an interactive business intelligence report analyzing global bike and accessories sales performance, built on a three-year (2020–2022) transactional dataset covering customers, products, returns, and territories.

The report is designed to support commercial decision-making by presenting revenue, profitability, customer value, and geographic performance in a single, explorable dashboard. It combines a company-wide overview with focused deep-dives into regional performance, customer segmentation, and product-category profitability, consistently connecting how much revenue is generated with how profitable and how risky (returns) that revenue actually is.

Built entirely in Power BI, the project covers the full analytics workflow: data extraction and transformation via Power Query, a hybrid star–snowflake data model connecting eight tables, custom DAX measures for revenue/cost/profit, and a four-page report with a consistent global KPI header and cross-page navigation.

## Problem Statement
The business had raw transactional data spread across multiple disconnected tables (orders, returns, products, customers, territories) with no centralized way to track performance or make investment decisions. Assessing where the business is actually winning and losing money requires synthesizing order-level sales, return behavior, customer demographics, and geography — information that is typically scattered across separate exports, inconsistent in format, and difficult to interpret without dedicated analysis.


## Objectives
Consolidate sales, returns, customer, product, and territory data into a single relational data model.
Present company-wide performance (Revenue, COGS, Profit, Profit %, Order Qty) alongside page-level drill-downs for immediate context.
Analyze the relationship between revenue and profitability at the product-category level to surface hidden margin differences.
Track geographic performance and return-rate risk by continent, country, and region.
Evaluate customer-segmentation logic against actual revenue contribution.
Deliver the analysis as an interactive, explorable report rather than a static summary, enabling stakeholders to drill into the specific view most relevant to their decision-making.

## Skills, Tools & Technologies

Tools

Power BI Desktop

Power BI Fabric (publish + share link)

Power Query

Skills

Data Modeling (Hybrid Star–Snowflake Schema)

DAX (Measures, calculated columns, time intelligence)

Data Cleaning & Transformation (ETL)

Data Visualization

Business/Commercial Analysis

Techniques

Conditional formatting

KPI cards

Toggle-driven metric switching (Revenue/Profit/Order Qty/Cost)

Correlation between revenue and margin

Geographic mapping

## Datasets

The dataset is provided as individual CSV files inside the Adventure Work All Table Dataset folder (rather than a single zip), so each table is directly browsable and previewable on GitHub, and any future update to one table shows up as a clean diff instead of re-uploading a whole archive.
https://github.com/LaboniAkter84/Sales-Analysis-Dashboard-/tree/main/Adventure%20Work%20All%20Table%20Dataset



