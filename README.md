# Insurance Claims Analytics Pipeline

<div align="center">

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![dbt](https://img.shields.io/badge/dbt-FF694B?logo=dbt&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white)
![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?logo=snowflake&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?logo=powerbi&logoColor=black)

**A comprehensive data pipeline for insurance claims processing, fraud detection, and business intelligence**

</div>

---

## Project Overview

This project demonstrates an **end-to-end data engineering pipeline** that transforms insurance claims data into actionable insights. Built as a portfolio demonstration using synthetic data, the pipeline showcases modern data stack practices including ETL/ELT workflows, cloud data warehousing, and business intelligence.

**What This Project Demonstrates:**
- Building scalable data pipelines with modern tools (Airbyte, dbt, Snowflake)
- SQL-based data transformation and modeling best practices
- Data quality testing and validation frameworks
- Business intelligence through interactive dashboards
- Real-world data engineering workflows and architecture

---

## Key Insights & Results

**Business Insights Discovered:**
- Identified **5.2% fraud rate** across 10,000+ synthetic claims
- Auto insurance claims showed **highest fraud prevalence (7.8%)** vs Health (2.3%)
- Claims above **$10K had 3x higher fraud risk** compared to smaller claims
- **Q4 showed 25% spike** in claim volume, indicating seasonal patterns

**Technical Achievements:**
- Processed 10K+ records through automated ETL pipeline
- Built 3-layer dbt model (staging → intermediate → marts)
- Implemented data quality tests with 100% pass rate
- Created incremental models for optimized processing

---

## Architecture Overview

<div align="center">

![Data Pipeline Workflow](workflow.png)

*Complete data flow from MongoDB to Power BI with dbt transformations*

</div>

### Pipeline Components

| Stage | Technology | Purpose |
|-------|------------|---------|
| **Source** | MongoDB Atlas | OLTP database for real-time claims |
| **Warehouse** | Snowflake | Cloud data warehouse for analytics |
| **Transformation** | dbt | SQL-based data modeling |
| **Visualization** | Power BI | Interactive dashboards |

---

## Quick Start

### Prerequisites
- Python 3.8+
- MongoDB Atlas account (free tier)
- Snowflake account
- Power BI Desktop

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/insurance-claims-pipeline.git
cd insurance-claims-pipeline

# 2. Install dependencies
pip install -r requirements.txt

# 3. Configure database connections
cp data-generator/ins_dbt/profiles.yml.example data-generator/ins_dbt/profiles.yml
# Edit profiles.yml with your database credentials

# 4. Generate sample data
python data-generator/generator.py

# 5. Run dbt transformations
cd data-generator/ins_dbt
dbt run

# 6. Test data quality
dbt test
```

### Power BI Setup
1. Open Power BI Desktop
2. Connect to Snowflake using your credentials
3. Import the `claims_summary` table
4. Build dashboard (see [Dashboard Guide](#-power-bi-dashboard))

---

## Data Model

### Source Schema (MongoDB)
```json
{
  "claim_id": "CLM_001",
  "customer_id": "CUST_123",
  "claim_type": "Auto",
  "claim_amount": 2500.00,
  "claim_date": "2024-01-15",
  "fraud_indicator": false,
  "processing_status": "Approved",
  "created_at": "2024-01-15T10:30:00Z"
}
```

### Transformed Schema (Snowflake)
```sql
-- claims_summary table
SELECT 
    claim_type,
    DATE_TRUNC('month', claim_date) as month,
    COUNT(*) as claims_count,
    SUM(claim_amount) as total_amount,
    SUM(CASE WHEN fraud_indicator THEN 1 ELSE 0 END) as fraud_count,
    AVG(claim_amount) as avg_claim_amount,
    ROUND(fraud_count::DECIMAL / claims_count * 100, 2) as fraud_rate_pct
FROM {{ ref('stg_claims') }}
GROUP BY 1, 2
```

---

## Power BI Dashboard

**Overview:**
- **KPI Cards**: Total Claims, Total Amount, Fraud Rate, Average Claim Amount
- **Monthly Trends**: Interactive time-series analysis with drill-down capabilities
- **Fraud Analysis**: Risk assessment by claim type and region

**Features:**
- Interactive filters by claim type and date range
- Conditional formatting for fraud alerts

---

## Configuration

### Environment Variables
```bash
# Database configuration
export MONGODB_URI="mongodb+srv://username:password@cluster.mongodb.net/"
export SNOWFLAKE_ACCOUNT="your-account.snowflakecomputing.com"
export SNOWFLAKE_USER="your-username"
export SNOWFLAKE_PASSWORD="your-password"
export SNOWFLAKE_WAREHOUSE="COMPUTE_WH"
export SNOWFLAKE_DATABASE="INSURANCE_CLAIMS"
export SNOWFLAKE_SCHEMA="PUBLIC"
```

### Custom Data Generation
```python
# Modify data-generator/generator.py
CLAIM_TYPES = ['Auto', 'Home', 'Health', 'Life', 'Business']
FRAUD_PROBABILITY = 0.05  # 5% fraud rate
DATE_RANGE = 365  # Generate 1 year of data
RECORDS_PER_DAY = 50  # Claims per day
```

---

## Testing

```bash
# Run dbt tests
dbt test

# Test data freshness
dbt source freshness
```

---
