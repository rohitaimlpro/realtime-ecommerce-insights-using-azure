# 📦 Real-Time E-Commerce Order Intelligence and Sales Monitoring (Azure-Based)

> **Live Analytics Project** using Azure Event Hub, Databricks (PySpark), Azure Blob Storage, and Power BI – built entirely using U.S.-based simulated e-commerce data.

---

## 🚀 Project Overview

This real-time data engineering project simulates and processes live e-commerce order data to deliver insightful dashboards for U.S. retail operations. We built an end-to-end pipeline using Azure-native tools and open-source technologies, following a **Bronze → Silver → Gold** architecture.

🔧 **Tech Stack**:  
- **Data Ingestion**: Azure Event Hub + Python Simulator  
- **Processing**: Azure Databricks (PySpark) – Bronze, Silver, Gold layers  
- **Storage**: Azure Blob Storage (Delta Format)  
- **Visualization**: Power BI Desktop (Live Connection to Gold Table)  
- **Version Control**: Git CLI & GitHub  

---

## 🧪 Project Structure

```
real-time-ecommerce-insights-azure/
│
├── CICD/                    # Git version tracking setup
├── Databrick Notebooks/    # Bronze, Silver, Gold notebooks
├── Event Hub/              # Namespace and Hub config
├── Power BI/               # Dashboard file (.pbix)
├── Simulator/              # Python script to simulate U.S. orders
├── Storage/                # Bronze, Silver, Gold Delta folders
├── requirements.txt        # Python dependencies
└── README.md               # 📄 This file
```

---

## 🧱 Step 1: Data Simulation + Event Streaming

📦 Created a Python simulator to continuously send fake U.S.-based e-commerce orders (TX, NY, CA...) to **Azure Event Hub**.

- Events included `order_id`, `state`, `city`, `product`, `quantity`, `price`, `timestamp`
- Used Python libraries: `uuid`, `random`, `json`, `time`, `azure-eventhub`
- Streamed events every second using a for-loop and `send_batch()` method

🪛 Commands:
- Used `pip install` to install Azure SDKs
- Set up Event Hub with namespace `e-commerce-namespace` and hub name `e-commerce-orders`
- Git-tracked simulator files with: `git add Simulator/`

---

## 🔁 Step 2: Real-Time Processing in Databricks

We created a **3-layer Delta Lake architecture** using **Structured Streaming** in PySpark.

### 🍂 Bronze Layer
- Read streaming data directly from Event Hub
- Parsed and flattened JSON events
- Wrote raw data to Azure Blob in Delta format

### 🔧 Silver Layer
- Cleaned, filtered, and type-casted Bronze data
- Removed nulls, bad records
- Stored refined data as a Delta table

### 🪙 Gold Layer
- Performed aggregation with **1-minute windows** (not hourly)
- Grouped by `state`, `product`, and `timestamp`
- Stored final result table (`gold`) to Blob in Delta

🧾 Notebooks:
- Named `1_bronze_stream.py`, `2_silver_clean.py`, `3_gold_agg.py`
- Git tracked using:  
```bash
git add Databrick\ Notebooks/
git commit -m "Add Bronze, Silver, Gold notebooks for streaming pipeline"
```

---

## 🗃️ Step 3: Azure Blob Storage – Delta Tables

Used Azure Blob Storage to persist all three layers in **Delta format**, organized as:

```
/mnt/data/bronze/  
/mnt/data/silver/  
/mnt/data/gold/
```

- Delta files were automatically updated via streaming write
- All Power BI visuals connected to the **Gold** layer

---

## 📊 Step 4: Power BI Dashboard (U.S. States)

Connected Power BI to **Databricks SQL Endpoint** to read the Gold Delta Table.

### 🔌 Connection Steps:
- Created SQL Warehouse in Databricks
- Connected Power BI using Azure Databricks connector (with token)
- Loaded `gold` table for visuals

### 📈 Visuals Created:
| Visual Type | Description |
|-------------|-------------|
| 📍 Map Chart | State-wise total sales |
| 📉 Line Chart | Sales trend over time (1-min window) |
| 🍩 Donut Chart 1 | Total sales per state |
| 🍩 Donut Chart 2 | Total items sold per state |
| 📄 Raw Data Table | Sorted by highest sales at top |

🧾 Tracked Power BI with:
```bash
cd Power\ BI/
git add .
git commit -m "Add Power BI dashboard with state-wise visuals"
```

> ❌ Note: Forecasting was planned but **not implemented** in the final version.

---

## 🔗 Git Version Control

Used Git CLI for all version tracking:
- `git init`, `git remote add origin ...`
- `git add`, `git commit`, `git push` at every phase
- Maintained clear folder-by-folder commits

---

## ✅ Final Outcome

This project delivers a **fully functional real-time analytics pipeline** powered by Azure and Delta Lake. The dashboard provides operations teams with **minute-level insights** into U.S. e-commerce orders by product, state, and time.

---

## 📌 Next Steps (Optional)

- Add live forecasting using Power BI’s built-in analytics
- Schedule CI/CD automation for Databricks notebooks using GitHub Actions
- Extend simulator to include product categories or geolocation lat/long

---

## 📁 Folder Summary

```
📂 Simulator         → Sends real-time JSON orders to Event Hub
📂 Event Hub         → Azure setup: namespace + hub
📂 Databrick Notebooks → Bronze → Silver → Gold PySpark logic
📂 Storage           → Delta Lake directory structure
📂 Power BI          → Final .pbix with charts and map
📂 CICD              → Git commit history & tracking
```

---

**Author**: *Your Name*  
**GitHub**: [yourusername](https://github.com/yourusername)

---

🎯 *Built for real-world, cloud-ready data engineering portfolios*