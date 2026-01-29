# SME Financial Automation Suite

## 📌 Project Overview
This project is a full-stack financial reporting solution designed for **Restora Kebab**, a retail food service business in Poland. The goal was to replace manual paper-based accounting with an automated **Business Intelligence (BI)** pipeline.

**The Business Problem:**
The business relied on decentralized data entry (receipts, manual ledgers), leading to a lack of visibility into daily profitability and time-consuming monthly reconciliation.

**The Solution:**
I engineered an automated ETL pipeline and Dashboard system that:
- Reduces monthly administrative time by **~40%**.
- Provides real-time visibility into **EBITDA**, **Net Profit**, and **Cash Flow**.
- Automates complex Polish tax calculations (**VAT**, **CIT**, **ZUS**).

---

## 🛠️ Tech Stack & Skills
* **Data Source:** Microsoft Excel (Advanced Data Validation, Structured Tables).
* **ETL (Extract, Transform, Load):** Power Query (M Language).
* **Data Modeling:** Power BI (Star Schema, Relationships).
* **Analysis:** DAX (Data Analysis Expressions).
* **Visualization:** Power BI Interactive Dashboard.

---

## 📊 The Architecture

### 1. Data Normalization (Power Query)
Raw transactional data from daily sales was originally unstructured ("Wide" format). I used Power Query to:
* **Unpivot** transactional columns to create a normalized database structure.
* Clean and type-cast currency formats for Polish Złoty (PLN).
* Create a dedicated **Date Table** for time-intelligence analysis.

### 2. The Data Model (Star Schema)
I constructed a Star Schema data model to ensure accurate filtering across different data streams:
* **Fact Tables:** `SalesTable`, `CostTable`, `LaborTable`.
* **Dimension Tables:** `Calendar` (Date Intelligence), `ChannelChart` (For Visualization).
* **Relationships:** One-to-Many relationships connecting all ledgers to the central Calendar table.

### 3. Key Financial Logic (DAX)
To calculate the true "Bottom Line," I implemented several custom measures.

**Net Profit Calculation:**
```dax
EBITA = [Total Revenue] - [Total COGS] - [Total Labor]

Profit Before Tax = [EBITA]-[VAT]

CIT = ([Profit Before TAX] * 0.12) - 300

Net Profit=[Profit Before Tax]-[CIT]

Net Profit Margin = DIVIDE([Net Profit], [Total Revenue], 0)
