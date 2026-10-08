# 🚀 Serverless Cloud ETL Pipeline (GCP)

An automated, serverless, and production-ready ETL pipeline deployed on **Google Cloud Platform (GCP)**. The system ingests reference city coordinates, population data, 5-day weather forecasts, and flight arrivals, transforming and storing them into a **Cloud SQL (MySQL)** relational database.

---

## 🏗️ Architecture Overview

```text
[ External APIs ] 
  ├── Open-Meteo API (Weather)
  └── RapidAPI / OpenSky (Flights)
          │
          ▼
[ GCP Cloud Functions (2nd Gen) ]  ◄── [ Cloud Scheduler (Daily Trigger: 0 1 * * *) ]
  │   ├── Python 3.10 Runtime
  │   └── SQLAlchemy & Pandas Engine
  │
  ├── Secret Manager 🔐 (Retrieves DB Passwords Securely)
  ▼
[ GCP Cloud SQL (MySQL Database) ]
  ├── cities
  ├── population
  ├── weather
  └── flights

---

🎯 Problem & Key Features
Automated Data Aggregation: Eliminates manual data collection by running scheduled daily pipelines via GCP Cloud Scheduler.

Serverless & Cost-Efficient: Built on GCP Cloud Functions, ensuring zero infrastructure management costs during idle time.

Enterprise Security Standard: Zero hardcoded credentials. Passwords and keys are retrieved at runtime via GCP Secret Manager and IAM Roles.

Normalized Data Model: Clean separation of concerns across MySQL relational tables for efficient querying.

📊 Pipeline Workflow
1_Cities (Reference Module): Processes target cities along with their latitude and longitude coordinates.

2_Population (Demographics Module): Loads historical demographic metrics for specified urban areas.

3_Weather (Forecast Module): Calls Open-Meteo REST API using geographic coordinates to extract a 5-day rolling weather forecast.

4_Flights (Aviation Module): Fetches real-time flight arrival data and scheduling details for target city airports.

Orchestration: Integrated into a unified HTTP function (run_full_etl) triggered automatically every night at 01:00 AM via Cloud Scheduler.

🛠️ Tech Stack & Dependencies
Cloud Infrastructure: GCP Cloud Functions (2nd Gen), GCP Cloud SQL, GCP Secret Manager, GCP Cloud Scheduler.

Core Libraries: Python 3.10+, pandas, SQLAlchemy, PyMySQL, requests, functions-framework.

```text

