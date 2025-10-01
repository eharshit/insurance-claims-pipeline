# 🏥 Insurance Claims Analytics Pipeline


![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![dbt](https://img.shields.io/badge/dbt-FF694B?logo=dbt&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white)
![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?logo=snowflake&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?logo=powerbi&logoColor=black)


## Summary

This project demonstrates a **production-ready data pipeline** that transforms raw insurance claims data into actionable business intelligence. The pipeline processes real-time insurance data through a modern tech stack, enabling fraud detection, trend analysis, and executive-level reporting.

**Key Features:**
- End-to-end data pipeline from source to visualization
- Automated fraud detection and analysis
- Real-time dashboards for business intelligence
- Scalable architecture for data processing

---

## 🏗️ Workflow


![Data Pipeline Workflow](workflow.png)

---


## Pipeline Components

| Stage | Technology | Purpose |
|-------|------------|---------|
| **Source** | MongoDB Atlas | OLTP database for real-time claims |
| **Warehouse** | Snowflake | Cloud data warehouse for analytics |
| **Transformation** | dbt | SQL-based data modeling |
| **Visualization** | Power BI | Executive dashboards |

---

##  Quick Start

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


## 📊 Data Model

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

## 📁 Project Structure

```
insurance-claims-pipeline/
├── 📁 data-generator/
│   ├── 🐍 generator.py              # Synthetic data generation
│   ├── 📄 requirements.txt          # Python dependencies
│   └── 📁 ins_dbt/                 # dbt project
│       ├── 📄 dbt_project.yml      # dbt configuration
│       ├── 📄 profiles.yml         # Database connections
│       ├── 📁 models/              # SQL transformations
│       │   ├── 📄 stg_claims.sql   # Staging model
│       │   ├── 📄 claims_summary.sql # Final model
│       │   └── 📄 source.yml       # Source definitions
│       ├── 📁 tests/               # Data quality tests
│       ├── 📁 macros/              # Reusable SQL functions
│       └── 📁 seeds/               # Reference data
├── 📁 docs/                        # Documentation
├── 📄 .gitignore                   # Git ignore rules
├── 📄 LICENSE                      # MIT License
├── 📄 README.md                    # This file
└── 🖼️ workflow.png                 # Architecture diagram
```

---

## 🔧 Advanced Configuration

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

## 🧪 Testing

```bash
# Run dbt tests
dbt test

# Test data freshness
dbt source freshness
```

---

