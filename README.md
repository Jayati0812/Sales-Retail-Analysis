# Sales-Margin-Analysis
# Finance Analysis

## 1. Project Title
**Finance Analysis**

Built an end-to-end sales retail analysis solution in Microsoft Fabric, ingesting ~1M+ records through a Fabric pipeline to understand Which customers, products, and regions are actually driving our revenue.

## 2. Short Description
The Sales Retail Analysis is an analytical report designed to help Priya (from Head of Sales Ops) understand Our sales team and leadership keep asking me the same question in every weekly review: 'Which customers, products, and regions are actually driving our revenue — and which ones are quietly dying?. This dashboard focuses on identifying what is the repeat customer rate over time and revenue drivers. This tool is intended for use by data analysts, the sales department, management, and data-driven strategists who want to understand revenue trends.

## 3. Tech Stack
The dashboard was built using the following tools and technologies:

- **Microsoft Fabric Pipeline** – Ingested ~1M+ records through an online dataset and applied transformations using a notebook.
- **Microsoft PySpark Notebook** – Data transformation, cleaning, and feature engineering for preparing the data using PySpark.
- **Microsoft Lakehouse** – Primary data source with structured Delta tables in the Tables section.
- **Microsoft Fabric Semantic Model** – Created the data model and built relationships.
- **DAX (Data Analysis Expressions)** – Used for calculated measures, dynamic visuals, and conditional logic.
- **Power BI Desktop** – Main data visualization platform used for report creation.
- **OneLake Security** – Implemented column-level and row-level security to ensure the safety of personal data.
- **App** – Published `App_Sales` for end-user access.
- **File Format** – `.pbix` for development and `.png` for dashboard previews.

## 4. Data Source
- **Source:** UCI Machine Learning Repository Online Retail II
- **Link:** [[Sales Retail Dataset](https://archive.ics.uci.edu/dataset/502/online+retail+ii)

Data covers ~1M+ records, including details such as invoice date, invoice, description, customer id, stock code, and quantity for the years 2012–2013.

## 5. Workflow
The end-to-end pipeline was built entirely within Microsoft Fabric:

- **Workspace** – Created `ws_finance` to host all Fabric items for this project.
- **Notebook** – Created a PySpark notebook and built the pipeline following medallion architecture: **Bronze** (raw invoice data ingested, checked types/nulls/row counts), **Silver** (cleaned, correctly typed, deduplicated), and **Gold** (aggregated and enriched with aging buckets, invoice amount buckets, and customer-level summaries for reporting).
- **Lakehouse** – Loaded all three layers into `lh_finance` as structured Delta tables, with Bronze, Silver, and Gold sitting inside the same lakehouse.
- **Security** – Applied column-level security (hiding `InvoiceAmount`) and row-level security (filtering by `countryCode`) directly on `lh_finance` using OneLake security, so protection is enforced consistently across every engine that queries it, not just the report.
- **Semantic Model** – Built `Finance_semantic`, which automatically inherits the OneLake security rules with no separate configuration needed.
- **Report** – Created the Finance Analysis report in Power BI, with separate pages for Collections (who's chronically late) and Treasury (cash flow and DSO trends).
- **App** – Published `App_Finance` for end-user access.

![Workflow](images/workflow.png)

## 6. Feature Highlights

### Business Problem
I used AI as a client, roleplaying as Rakesh from the Finance department, where the company sells on credit to distributors and business clients under standard 30/45/60-day payment terms. Over the last few quarters, the company's Days Sales Outstanding (DSO) had been creeping up — cash that should be in the company's account was sitting with customers longer than it should.

**Key Questions:**
- How much money are we actually talking about?
- Which customers have consistently been late?
- Is there a pattern in why people pay late?
- Is late payment behavior worsening month over month?
- When customers are late, how late?

### Goal of the Dashboard
The goal of this dashboard was to create an interactive report that helped the Finance department understand the cause of payment delays relative to the standard 30/45/60-day payment terms. This dashboard helped Rakesh from Finance communicate to leadership and senior management what steps could be taken to reduce and manage DSO by identifying its key drivers.

### Key Visuals

**KPIs used in this report:**
- **Money at Risk:** 53.96K — total invoice amount with late customers
- **Late Customers:** 83 — count of customers who paid late
- **Total Customers:** 100 — distinct count of customers
- **Late Customer % YoY Comparison:** -3.51% — late payment performance improved by 3.51%
- **Avg Days Late:** 9.68 — average days a customer paid after the invoice date

**Slicers used:**
- Year (invoice year)
- Month (invoice month)
- Country Code

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
