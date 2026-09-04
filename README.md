# Sales-Margin-Analysis

## 1. Project Title
**Finance Analysis**

Built an end-to-end sales retail analysis solution in Microsoft Fabric, ingesting ~1M+ records through a Fabric pipeline to understand Which customers, products, and regions are actually driving our revenue.

## 2. Short Description
The Sales Retail Analysis is an analytical report designed to help Priya (from Head of Sales Ops) understand Our sales team and leadership keep asking me the same question in every weekly review: 'Which customers, products, and regions are actually driving our revenue — and which ones are quietly dying?. This dashboard focuses on dashboard that shows revenue trends, customer segments (who's valuable, who's at risk), regional performance, and product performance, sliceable by date.. This tool is intended for use by data analysts, the sales department, management, and data-driven strategists who want to understand revenue trends.

## 3. Tech Stack
The dashboard was built using the following tools and technologies:

- **Microsoft Fabric Pipeline** – Ingested ~1M+ records through an online dataset and applied transformations using a notebook.
- **Microsoft PySpark Notebook** – Data transformation, cleaning, and feature engineering for preparing the data using PySpark.
- **Microsoft Lakehouse** – Primary data source with structured Delta tables in the Tables section.
- **Microsoft Fabric Semantic Model** – Created the data model and built relationships.
- **DAX (Data Analysis Expressions)** – Used for calculated measures, dynamic visuals, and conditional logic.
- **Power BI Desktop** – Main data visualization platform used for report creation.
- **OneLake Security** – Implemented column-level and row-level security to ensure the safety of personal data.
- **App** – Published `App_Retail` for end-user access.
- **File Format** – `.pbix` for development and `.png` for dashboard previews.

## 4. Data Source
- **Source:** UCI Machine Learning Repository Online Retail II
- **Link:** [[Sales Retail Dataset](https://archive.ics.uci.edu/dataset/502/online+retail+ii)

Data covers ~1M+ records, including details such as invoice date, invoice, description, customer id, stock code, price, country and quantity, for the years 2009–2011.

## 5. Workflow
The end-to-end pipeline was built entirely within Microsoft Fabric:

- **Workspace** – Created `ws_sales_retail` to host all Fabric items for this project.
- **Notebook** – Created a PySpark notebook and built the pipeline following medallion architecture: **Bronze** (raw invoice data ingested, checked types/nulls/row counts), **Silver** (cleaned, correctly typed, deduplicated), and **Gold** (aggregated and enriched with region, net revenue, and customer-level summaries for reporting).
- **Lakehouse** – Loaded all three layers into `lh_sales_retail` as structured Delta tables, with Bronze, Silver, and Gold sitting inside the same lakehouse.
- **Security** – Applied column-level security (hiding `price`) and row-level security (filtering by `region`) directly on `lh_sales_retail` using OneLake security, so protection is enforced consistently across every engine that queries it, not just the report.
- **Semantic Model** – Built `sales_retail_model`, which automatically inherits the OneLake security rules with no separate configuration needed.
- **Report** – Created the Sales Retail Analysis report in Power BI, with separate pages for Overview and Performance(repeat customer rate over time).
- **App** – Published `App_Retail` for end-user access.

![Workflow](images/workflow.png)

## 6. Feature Highlights

### Business Problem
I used AI as a client, roleplaying as Priya from Head of Sales Ops, Our sales team and leadership keep asking me the same question in every weekly review: 'Which customers, products, and regions are actually driving our revenue — and which ones are quietly dying?

**Key Questions:**
Are we retaining customers, or is flat revenue masking churn that's being covered up by new customer acquisition?
Which countries/regions are growing vs. declining?
Are a small number of wholesale/bulk customers propping up the numbers while our regular customer base shrinks?
What's our repeat purchase rate, and which products drive repeat business vs. one-off purchases?
Are we over-relying on a handful of SKUs, and what happens to revenue if one of them has a supply issue?

### Goal of the Dashboard
The goal of this dashboard was to create an interactive report that helped the Sales department understand Which customers, products, and regions are actually driving our revenue — and which ones are quietly dying. This dashboard helped Priya from Sales communicate to leadership and senior management what steps could be taken to manage revenue and customer repeat rate and help business grow.

### Key Visuals

**KPIs used in this report:**
- **Net Revenue:** $18.85M — total revenue excluding cancellation
- **Average order value:** 351.71 
- **Total Customers:** 5943 — distinct count of customers
- **total orders:** 53,597 — total orders placed excluding cancelled one
- **Cancellation Rate:** 0.05% — how many orders were cancalled divided by total order including cancelled one
- top 10 customer revenue share %- 26.98% - top 10 customers are contributing to total revenue
- top 10 product revenue share %- 7.69% - top 10 products are contributing to total revenue
- repeat customer rate - 75.38% - customers ordering more than 1

**Slicers used:**
- Year (invoice year)
- Month (invoice month)
- Region

**Total Invoices and Customer % Late Trend Over Time:**
A line-and-column combo chart where columns represent total invoices each month and the line represents late customer % — showing what proportion of invoices were late over time.

**Customer % Late by Disputed Bills:**
A bar chart showing whether disputed bills drive late payment issues.

**Customers Late by 30+ Days:**
A matrix of customers who paid after 30+ days, showing whether the amount owed by them was significant — helping plan treasury more easily and in advance.

**Top 10 Customers by Avg Days Late:**
A matrix of the customers with the highest late payment %, along with total invoices and average days late.

**Customer % Late by Type of Bill:**
A bar chart showing whether paper bills or electronic bills are more likely to be late, helping plan a shift toward the bill type that causes fewer late payments.

## 7. Insights
- Money at risk — the total amount with late customers — is 53.96K.
- DSO, or late customer %, has improved by 3.5% year over year.
- The top 10 customers with the highest late-payment % need to be contacted first.
- Some customers who pay after 30 days also carry high invoice amounts.
- Disputed bills tend to have more late payments.
- Paper bills tend to generate more late payments.
- Bills in the larger invoice amount band receive the most late payments.

## 8. Business Impact
- Treasury planning should account for the money at risk — 53.96K.
- DSO is improving year over year but needs further improvement.
- Collection teams should call the top 10 late-paying customers first to plan treasury effectively.
- Customers with average days late greater than 30 and high invoice amounts need strict follow-up action.
- Customers should be encouraged to shift toward electronic bills.
- Customers with large invoice amounts should be checked more frequently to track payment status.
  
## 9. Screenshots
**Workspace (ws_finance)**
![Workspace](images/workspace_finance.png)
**Data ingesting through pipeline(pl_ingest_finance)**
![Pipeline](images/Pipeline.png)
**Data loading to Lakehouse (lh_finance)**
![Dataflow_Gen2_to_Lakehouse](images/data_loading_into_lakehouse.png)
**Data in Lakehouse (lh_finance)**
![Lakehouse](images/Lakehouse_finance.png)
**Semantic Model (Finance_Model)**
![Semantic_Model](images/finance_model.png)
**Overview of Dashboard**
![Overview](images/Overview.png)
**Implementing Row Level Security**
![Deep Dive](images/Deep_Dive.png)
**Row Level Security Applied**
![CLS](images/CLS.png)
**Column Level Security Applied**
![Column_Level_Security](images/Column_Level_Security.png)
**App (App_Finance)**
![App_Overview](images/App_Overview.png)
