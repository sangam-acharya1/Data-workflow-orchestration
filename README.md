# NYC Taxi Data Engineering Pipeline

An end-to-end Data Engineering pipeline built using Kestra, PostgreSQL, Docker, and SQL to automate ingestion, transformation, and loading of NYC Taxi Trip data.

---

# Project Overview

This project demonstrates a production-style ETL/ELT pipeline that:

- Downloads NYC Taxi datasets automatically
- Extracts and loads CSV data into PostgreSQL
- Uses staging and final tables
- Generates unique row IDs for deduplication
- Merges only new records into production tables
- Automates workflows using Kestra schedules
- Uses Docker for containerized setup

---

# Architecture

```text
                +-------------------+
                |      Kestra       |
                | Workflow Engine   |
                +---------+---------+
                          |
                          v
                +-------------------+
                | Download CSV Data |
                +---------+---------+
                          |
                          v
                +-------------------+
                |  Staging Tables   |
                |   PostgreSQL      |
                +---------+---------+
                          |
                          v
                +-------------------+
                | Data Transformation|
                |  Deduplication     |
                +---------+---------+
                          |
                          v
                +-------------------+
                | Final Production  |
                |      Tables       |
                +-------------------+

                          ^
                          |
                    +-----------+
                    |  pgAdmin  |
                    +-----------+
```

---

# Tech Stack

- Kestra
- PostgreSQL
- pgAdmin
- Docker & Docker Compose
- SQL
- YAML
- Shell Commands (wget, gunzip)

---

# 📂 Project Structure

```bash
.
├── docker-compose.yml
├── flows/
│   └── workflow-orchestration.yml
├── screenshots/
├── README.md
```

# Features

## Automated Workflow Orchestration

- Scheduled monthly data ingestion
- Separate workflows for Yellow and Green taxi datasets

## Data Ingestion

- Downloads NYC Taxi data directly from source
- Supports compressed `.csv.gz` files

## Data Transformation

- Creates staging tables
- Generates `unique_row_id` using MD5 hashing
- Prevents duplicate records

## Production-style Loading

- Uses SQL `MERGE` statements
- Inserts only new records into final tables

## Containerized Setup

- PostgreSQL
- pgAdmin
- Kestra
- Kestra internal PostgreSQL database

---

## Start Docker Containers

```bash
docker compose up -d
```

---

## Access Services

### Kestra

```text
http://localhost:8080
```

### pgAdmin

```text
http://localhost:8085
```

---

# Pipeline Workflow

1. Download NYC Taxi dataset
2. Extract compressed CSV files
3. Load data into PostgreSQL staging tables
4. Generate unique row identifiers
5. Merge only new records into production tables
6. Clean temporary execution files

---

# Scheduling

The workflow is automatically triggered monthly using cron schedules.

| Dataset     | Schedule                           |
| ----------- | ---------------------------------- |
| Green Taxi  | 9:00 AM on 1st day of every month  |
| Yellow Taxi | 10:00 AM on 1st day of every month |

---

# Concepts Learned

- ETL / ELT Pipelines
- Workflow Orchestration
- Docker Containerization
- PostgreSQL Data Warehousing
- Data Deduplication
- Staging vs Production Tables
- SQL MERGE Operations
- Scheduled Pipelines
- Production-style Data Engineering

# Dataset Source

NYC Taxi Trip Data:
https://github.com/DataTalksClub/nyc-tlc-data/releases

---

# Acknowledgements

This project was inspired by real-world Data Engineering workflows and ETL pipeline architectures.
