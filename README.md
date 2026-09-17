# Brazilian E-Commerce Sales & Operations Dashboard (Power BI + PostgreSQL)

An end-to-end BI project analyzing the [Olist Brazilian E-Commerce dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data) — from raw CSVs, through a normalized PostgreSQL warehouse, into a live **DirectQuery** Power BI report covering sales, logistics, customer behavior, payments, and seller performance.

## 🔗 Live Report / Files
- `PowerBI-Project/` — Power BI Project (.pbip) files: report layout + semantic model (TMDL), open directly in Power BI Desktop
- `sql/` — All PostgreSQL DDL, indexes, and BI views used to build the warehouse
- `dax/measures.dax` — Every DAX measure used across the report
- `screenshots/` — Static exports of each report page

## 📊 What's in the Report

| Page | What it shows |
|---|---|
| **Overview (Executive Dashboard)** | Headline KPIs — Revenue, Orders, Customers, AOV, On-Time %, YoY growth — plus top categories, revenue trend, and order status split |
| **Sales Trends** | Revenue and order volume over time |
| **Category & Product** | Performance breakdown by product category |
| **Customers Geographic** | Customer distribution and revenue by state/city |
| **Delivery & Logistics** | Delivery times, on-time vs. late delivery analysis |
| **Ratings & Reviews** | Review score distribution and sentiment buckets |
| **Payments** | Payment method mix and installment behavior |
| **Sellers** | Revenue and order volume by seller |

### Key metrics surfaced
- **₹14.21M** total revenue across **98.67K** orders from **95.42K** customers
- **144.01** average order value (AOV)
- **93.23%** on-time delivery rate
- **4.03** average review rating
- **253.07%** YoY revenue growth

## 🏗️ How it was built

1. **Data source**: Raw CSVs from the Kaggle Olist dataset (customers, orders, order items, payments, reviews, products, sellers, geolocation)
2. **Warehouse**: Loaded into PostgreSQL, modeled into normalized tables with primary/foreign keys and indexes on all join/filter columns (see `sql/01_create_tables.sql`, `02_foreign_keys.sql`, `03_indexes.sql`)
3. **BI Views**: Built cleaned, pre-joined views (`bi_fact_sales`, `bi_fact_order`, `bi_dim_product`, etc.) in PostgreSQL so Power BI queries stay lightweight — see `sql/04_bi_views.sql`
4. **Connection mode**: Power BI connects via **DirectQuery** straight to the PostgreSQL BI views (no data imported/cached in the report), with a separate imported Date dimension table related to the fact views
5. **DAX layer**: ~25 measures covering revenue, orders, AOV, YoY/rolling trends, delivery performance, review sentiment, and seller metrics — full list in `dax/measures.dax`
6. **Report design**: 8 report pages built around a consistent KPI-card + chart layout

## 🧰 Tech Stack
- **PostgreSQL** — data warehouse, views, indexing
- **Power BI Desktop** — DirectQuery semantic model, DAX, report design
- **DAX** — measure layer (time intelligence, ratios, conditional buckets)
- **SQL** — table design, foreign keys, BI views


Since no data is cached in the file, the screenshots in `screenshots/` are the best way to view the report without setting up the database.

## 📁 Repo Structure
```
├── PowerBI-Project/        → .pbix
├── sql/                     → table creation, keys, indexes, BI views
├── dax/measures.dax         → all DAX measures
├── screenshots/             → exported report pages
└── README.md
```

---
*Dataset: [Olist Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data) (Kaggle, public/anonymized). No proprietary or personal data used.*
