# E-Commerce Sales Intelligence Data Warehouse: End-to-End ETL, Modelling, and Analytics Platform

**A SQL Data Warehouse project transforming the E-Commerce Public Datasets into an analytical powerhouse for business insights.**

---

## Project Overview
This project builds a **Data Warehouse** on top of the E-Commerce dataset to enable fast, reliable, and insightful business intelligence queries.

**Goals:**
- Centralise raw e-commerce data in a structured warehouse.
- Apply **ETL/ELT** processes to clean, transform, and model the data.
- Enable advanced analytics for **sales trends, customer behaviour, product performance, and delivery efficiency**.

---

## Dataset
The dataset contains real e-commerce orders from multiple marketplaces in Brazil between 2016 and 2018, including:
- Orders & Order Items
- Customers
- Products
- Sellers
- Payments
- Geolocation
- Reviews

📌 **Source:** [Kaggle - Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

---

## Architecture

### Data Flow
[Kaggle Dataset] → [Staging Tables] → [Transformations] → [Dimensional Model] → [BI / Analytics]

### Diagram
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/371ec815-cdf5-4d66-90da-3dd1b2e6d44b" />


**Layers:**
1. **Staging:** Raw data loaded as-is for auditing.
2. **Transformation:** Data cleaning, normalisation, and enrichment.
3. **Dimensional Model:** Star Schema with Fact and Dimension tables for analytics.

---

## Tools & Technologies
- **SQL** (PostgreSQL / BigQuery / Snowflake — adjust as applicable)
- **dbt** for transformations
- **Docker** for local environment
- **Airflow** for orchestration (optional)
- **Power BI / Tableau** for visualization

---

## 🗄 Data Model
**Star Schema:**
- **Fact Tables:**
  - `fact_orders`
  - `fact_order_items`
  - `fact_payments`
- **Dimension Tables:**
  - `dim_customers`
  - `dim_products`
  - `dim_sellers`
  - `dim_dates`
  - `dim_geolocation`

---

## 🚀 Setup Instructions

### 1️⃣ Clone Repository
```bash
git clone https://github.com/your-username/brazilian-ecommerce-dwh.git
cd brazilian-ecommerce-dwh

2️⃣ Configure Environment
Set up .env file with DB credentials.

Install dependencies:
pip install -r requirements.txt

3️⃣ Load Data
Download CSV files from Kaggle and place them in /data/raw/

Run initial load:
python scripts/load_staging.py

4️⃣ Build Warehouse

dbt run
📊 Example Analytical Queries
Top 5 Cities by Total Sales:

SELECT 
    dim_geolocation.city,
    SUM(fact_orders.total_price) AS total_sales
FROM fact_orders
JOIN dim_geolocation 
    ON fact_orders.geolocation_id = dim_geolocation.id
GROUP BY dim_geolocation.city
ORDER BY total_sales DESC
LIMIT 5;
Monthly Sales Trend:
SELECT
    dim_dates.year_month,
    SUM(fact_orders.total_price) AS total_sales
FROM fact_orders
JOIN dim_dates 
    ON fact_orders.date_id = dim_dates.id
GROUP BY dim_dates.year_month
ORDER BY dim_dates.year_month;
💡 Business Insights
With this warehouse, you can:

Identify best-selling products and categories.

Monitor delivery performance by region.

Understand customer purchasing patterns.

Track revenue growth trends over time.

⚡ Performance Optimisation
Partitioned fact tables by date.

Indexed foreign keys for faster joins.

Materialised views for common aggregations.

📜 License
This project is licensed under the MIT License.

🙏 Credits
Dataset by Olist on Kaggle.

Project maintained by Your Name.
Manny Ay

