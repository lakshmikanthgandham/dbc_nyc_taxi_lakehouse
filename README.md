# dbc_nyc_taxi_lakehouse

NYC_Taxi_Lakehouse

📌 Project Overview

The NYC_Taxi_Lakehouse project is designed to process High Volume For-Hire Vehicle Trip Records (FHV Trip Data) from NYC Taxi & Limousine Commission. The goal is to implement a Medallion Lakehouse architecture using Databricks, PySpark, and Snowflake for scalable, fault-tolerant ETL pipelines, enabling analytics-ready reporting.

**Key objectives:**

Ingest large Parquet datasets for June, July, and August into a Bronze layer.

Perform data transformation, validation, and deduplication to create a Silver layer.

Aggregate and curate data into a Gold layer for reporting.

Track loaded files via an ingested_files table.

Load curated Gold data into Snowflake for analytics and reporting dashboards.

Orchestrate the entire ETL workflow using a Databricks Job.

🏗 Architecture
External GCS Bucket (Raw Parquet) -> Bronze Layer (raw ingestion) -> Silver Layer (cleaned & validated) -> Gold Layer (aggregated, reporting-ready) -> Snowflake (analytics & dashboards)


Bronze: Raw FHV trip data as ingested from GCS

Silver: Cleaned, validated, and deduplicated records

Gold: Aggregated data ready for analytics and reporting

Ingested_files: Tracks ingested Parquet files to prevent reprocessing

⚙️ Tech Stack
Layer/Tool	Technology
Data Ingestion	PySpark, Databricks, GCS
Data Processing	PySpark, Delta Lake, Databricks Notebooks
Storage	Delta Lake (Bronze/Silver/Gold tables)
Catalog & Schema	Databricks Catalog & Schemas (nyc_taxi_catalog)
Orchestration	Databricks Jobs (sequential notebook execution, retries)
Reporting / Analytics	Snowflake
Version Control	GitHub
📝 Project Structure
NYC_Taxi_Lakehouse/
├─ notebooks/            
│   ├─ ingest_bronze.py        # Ingest raw Parquet files into Bronze
│   ├─ transform_silver.py     # Clean, validate, deduplicate for Silver
│   ├─ aggregate_gold.py       # Aggregate & prepare Gold layer
│   ├─ load_snowflake.py       # Load Gold data into Snowflake
├─ jobs/                 
│   └─ nyc_taxi_etl_job.json   # Databricks job orchestrating all notebooks
├─ src/                  
│   └─ utils.py                # Helper Python functions (file tracking, logging)
├─ README.md                 
├─ requirements.txt           

🚀 How to Run
1. Clone Repo
git clone https://github.com/lakshmikanthgandham/dbc_nyc_taxi_lakehouse.git
cd NYC_Taxi_Lakehouse

2. Configure Databricks Repo

Link repo in Databricks Repos

Install Python dependencies if needed:

pip install -r requirements.txt

3. Run Databricks Job

The job executes notebooks sequentially:

ingest_bronze.py → ingest raw Parquet files from GCS

transform_silver.py → transform data into Silver layer

aggregate_gold.py → aggregate for Gold layer

load_snowflake.py → load Gold layer into Snowflake

The job tracks files in ingested_files table to avoid reprocessing.

Supports auto-retry for fault tolerance.

⚡ Key Features

Medallion Architecture: Bronze → Silver → Gold

High-Volume ETL: Efficient handling of large Parquet datasets using PySpark

File Tracking: Avoids reprocessing with ingested_files table

Fault-Tolerant Pipeline: Databricks Jobs with retries

Scalable Analytics: Gold data loaded into Snowflake for reporting

Version Control: Notebooks, job JSON, and scripts stored in GitHub