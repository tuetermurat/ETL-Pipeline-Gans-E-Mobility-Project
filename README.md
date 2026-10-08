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

