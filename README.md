# retail_etl
# Retail Sales ETL Pipeline 🚀

## Project Overview
An end-to-end ETL pipeline that ingests retail sales data, transforms it using DBT, and loads it into Snowflake for business intelligence reporting.

## Architecture

CSV Data → Python ETL → Snowflake (Bronze) → DBT → Silver Layer → DBT → Gold Layer

## Tools & Technologies
- **Python** — Data extraction and loading
- **Snowflake** — Cloud data warehouse
- **DBT Cloud** — Data transformation
- **SQL** — Data modeling

## Data Source
- Superstore Sales Dataset from Kaggle (9,994 rows, 21 columns)

## Pipeline Layers
### Bronze Layer (Raw)
- Raw data loaded as is from the CSV file
- Table: `RETAIL_DB.RAW.SUPERSTORE`

### Silver Layer (Staging)
- Cleaned and standardized data
- Converted date columns to proper date format
- Removed rows with null Order IDs
- Table: `RETAIL_DB.DBT_VTALLAPALLY.STG_SUPERSTORE`

### Gold Layer (Marts)
- Business ready aggregated data
- Sales summary by Region, Category, Segment and Date
- Table: `RETAIL_DB.DBT_VTALLAPALLY.MART_SALES_SUMMARY`

## Project Structure

retail_etl/
│
├── data/
│   └── Sample - Superstore.csv
│
├── etl/
│   └── extract_load.py
│
├── models/
│   ├── staging/
│   │   └── stg_superstore.sql
│   └── marts/
│       └── mart_sales_summary.sql
│
├── .env
└── README.md

## How To Run
### 1. Install Dependencies
```bash
pip install pandas snowflake-connector-python python-dotenv
```

### 2. Set Up Environment Variables
Create a `.env` file with your Snowflake credentials:

SNOWFLAKE_ACCOUNT=your_account
SNOWFLAKE_USER=your_username
SNOWFLAKE_PASSWORD=your_password
SNOWFLAKE_DATABASE=RETAIL_DB
SNOWFLAKE_SCHEMA=RAW
SNOWFLAKE_WAREHOUSE=RETAIL_WH

### 3. Run Python ETL Script
```bash
python etl/extract_load.py
```

### 4. Run DBT Models
```bash
dbt run
```

## Key Learnings
- Built a full ETL pipeline from scratch
- Implemented bulk loading for fast data ingestion
- Applied Medallion Architecture (Bronze/Silver/Gold)
- Used DBT for data transformation and modeling
