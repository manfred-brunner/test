
# 🌐 OpenSky Flight Data Analytics Project

## ✈️ Project Summary
This portfolio project demonstrates a full end-to-end **big data analytics pipeline** for real-time aircraft tracking using the **OpenSky Network API**, AWS services, and visualization in **Amazon QuickSight**. It highlights key concepts such as **ETL**, **data lakes**, **data warehouses**, **API integration**, and **cloud-based data visualization**.

The goal is to ingest live flight data, process and transform it, store it in a relational database, and visualize aircraft positions, speed, and altitude in an interactive dashboard.

---

## 🎓 Key Concepts & Technologies

| Concept           | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| **API**          | The OpenSky Network REST API provides real-time aircraft data.             |
| **ETL**          | Extract, Transform, Load process implemented using AWS Lambda and Glue.    |
| **Data Lake**    | Raw flight data is stored in Amazon S3 in JSON format.                     |
| **Data Warehouse** | Transformed data is stored in Amazon RDS (PostgreSQL) for analytics.        |
| **AWS Glue**     | Used for data transformation and ETL jobs. Includes Glue Crawlers and Jobs.|
| **AWS Lambda**   | Used to fetch live data from the API and store in S3 automatically.        |
| **Amazon QuickSight** | Used to create live dashboards for visualization.                          |
| **pgAdmin**      | Used for inspecting and querying the PostgreSQL database.                  |

---

## 🚀 High-Level Steps Performed

### 1. **Set Up Data Ingestion**
- Created an AWS Lambda function `fetch_opensky_flight_data_toS3` to:
  - Call the OpenSky Network REST API
  - Fetch live flight state vectors
  - Save them to Amazon S3 as JSON files in a `raw/` folder

### 2. **Set Up the Data Lake**
- Raw flight data stored in Amazon S3
- Created a Glue Crawler to:
  - Scan the S3 bucket
  - Infer schema and create a table in the Glue Data Catalog

### 3. **Transform Data with AWS Glue Job**
- Created a Glue ETL Job to:
  - Load data from the Glue Catalog
  - Explode the nested `states` array
  - Extract and cast aircraft attributes like `icao24`, `callsign`, `velocity`, `altitude`, `true_track`, etc.
  - Load transformed data into Amazon RDS PostgreSQL (`flights_live` table)

### 4. **Set Up the Data Warehouse**
- Deployed Amazon RDS PostgreSQL database (`opensky-postgres`)
- Connected with `pgAdmin` to inspect the `flights_live` table

### 5. **Visualize Data in Amazon QuickSight**
- Created a dataset connected to the PostgreSQL table
- Built an interactive dashboard with:
  - Map of live aircraft positions using `latitude` and `longitude`
  - Point color based on velocity (slow, medium, fast)
  - Point size based on altitude
  - Tooltip with `callsign`, `heading (true_track)`, and speed

---

## 🏆 Achievements
- Integrated real-time data from a public API
- Implemented a robust ETL pipeline on AWS
- Built a clean, interactive flight tracker dashboard in QuickSight
- Demonstrated the difference between a **data lake** (S3) and a **data warehouse** (RDS)
- Used SQL (PostgreSQL) to verify data, with potential for stored procedures & views

---

## 📂 Project Files (GitHub)
You can include the following in your GitHub repo:
- `lambda_fetch_opensky.py`: The Lambda function code
- `glue_etl_script.py`: The Glue ETL transformation logic
- `README.md`: This markdown summary
- `dashboard_screenshot.png`: Screenshot of the QuickSight dashboard

---

## 📄 Future Work (Optional Enhancements)
- Schedule the Lambda and ETL jobs to run automatically
- Add Athena + S3 Parquet storage for cheaper querying
- Add filters or controls to the dashboard (e.g. by country, speed, or altitude)
- Export or embed the dashboard in a portfolio website
