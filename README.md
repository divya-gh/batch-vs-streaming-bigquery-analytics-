# batch-vs-streaming-bigquery-analytics
This project showcases how cloud-native analytics platforms like BigQuery enable both real-time and batch analytics, empowering businesses to make faster and smarter decisions using live data streams.

## 🚀 Project Overview

This project demonstrates how to identify, analyze, and query batch and streaming data sources using Google BigQuery. The use case is based on a real-world eCommerce scenario where near real-time shopping cart activity is analyzed to support merchandising and pricing decisions.

The project highlights how streaming data enables minute-by-minute insights, while batch data supports historical and aggregated analysis.

🧠 Business Scenario

### A lead merchandiser needs to monitor:

* Real-time items added to shopping carts

* Minute-by-minute trends for promotional effectiveness

* Using BigQuery, we analyze:

* Streaming source: shopping_cart table (live data ingestion)

* Batch source: orders table (periodic batch loads)

🏗️ ## Architecture

* Data Warehouse: Google BigQuery

* Streaming Source: User shopping cart activity

* Batch Source: Completed orders

* Analytics Layer: SQL queries with time-based aggregation

🔍 ## Key Concepts Demonstrated

* Difference between batch vs streaming data processing

* Identifying streaming buffers in BigQuery

* Real-time analytics using CURRENT_TIMESTAMP()

* Time-based aggregation with FORMAT_TIMESTAMP()

* Join operations between transactional and dimensional tables

* Designing queries for live dashboards

🧪 ## Queries Used
1️⃣ ### Identify Streaming Data
SELECT *
FROM `thelook_gcda.shopping_cart`
ORDER BY created_at DESC
LIMIT 10;

✔ Shows continuously changing results due to streaming inserts

2️⃣ Identify Batch Data
SELECT *
FROM `thelook_gcda.orders`
ORDER BY created_at DESC
LIMIT 10;

✔ Results remain static until the next batch load

3️⃣ Minute-by-Minute Streaming Analytics
SELECT
  p.category,
  FORMAT_TIMESTAMP('%H:%M', sc.created_at) AS added_at_minute,
  SUM(sc.quantity) AS sum_quantity
FROM `thelook_gcda.shopping_cart` sc
INNER JOIN `thelook_gcda.products` p
  ON p.id = sc.product_id
WHERE p.category = 'Jeans'
  AND sc.created_at > TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 HOUR)
GROUP BY p.category, added_at_minute
ORDER BY added_at_minute DESC;

✔ Enables real-time dashboarding for merchandising decisions

📈 Insights Generated

Streaming data provides real-time visibility into customer behavior

Batch data is ideal for historical reporting and reconciliation

Combining both enables hybrid analytics architectures

🛠️ Tools & Technologies

Google BigQuery

SQL

Streaming Buffers

Time-series Aggregation

Cloud Data Analytics

🎯 Skills Demonstrated

Cloud Data Analytics

Streaming vs Batch Processing

SQL for Analytics

Time-based Data Aggregation

Data Modeling & Joins

Business-Oriented Analytics Design

📌 Use Cases

Real-time dashboards

Promotion effectiveness analysis

Inventory and demand monitoring

eCommerce behavioral analytics

🏁 Conclusion

This project showcases how cloud-native analytics platforms like BigQuery enable both real-time and batch analytics, empowering businesses to make faster and smarter decisions using live data streams.

📎 This project was completed as part of the Google Cloud Data Analytics learning program.
