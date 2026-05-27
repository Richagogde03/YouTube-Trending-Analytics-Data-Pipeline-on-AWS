# YouTube Trending Analytics Pipeline

![Uploading image.png…]()


## Project Overview

This project is an end-to-end cloud-based YouTube Trending Analytics Data Pipeline built using AWS services. The pipeline extracts trending YouTube video data using the YouTube Data API, stores raw data in Amazon S3, processes and transforms the data using AWS Glue, and enables analytics using Amazon Athena.

The main goal of the project is to demonstrate a modern data engineering workflow using a layered data lake architecture (Bronze → Silver → Gold) and serverless AWS services.

---

# Architecture

## Workflow

1. AWS Lambda extracts YouTube trending data using the YouTube API.
2. Raw JSON and CSV files are stored in the Bronze layer in Amazon S3.
3. S3 event notifications trigger downstream processing.
4. AWS Glue Crawlers infer schema and update the Glue Data Catalog.
5. AWS Glue Jobs clean, transform, validate, and convert data into Parquet format.
6. Processed data is stored in the Silver layer.
7. Aggregated analytical datasets are stored in the Gold layer.
8. Amazon Athena is used to query the transformed data.
9. Amazon SNS is used for job notifications and alerts.

---

# AWS Services Used

| Service           | Purpose                                           |
| ----------------- | ------------------------------------------------- |
| AWS Lambda        | Extract YouTube API data and orchestrate pipeline |
| Amazon S3         | Store Bronze, Silver, and Gold layer data         |
| AWS Glue          | ETL processing and schema management              |
| Glue Crawler      | Automatically detect schema                       |
| Glue Data Catalog | Metadata management                               |
| Amazon Athena     | SQL-based analytics on S3 data                    |
| Amazon SNS        | Notifications and alerts                          |
| IAM               | Role-based access control                         |
| CloudWatch        | Logging and monitoring                            |

---

# Data Lake Architecture

## Bronze Layer

The Bronze layer stores raw ingested data directly from the YouTube API without major transformations.

### Stored Data

* Raw JSON files
* Raw CSV files
* API responses
* Reference data

### Purpose

* Preserve original source data
* Enable reprocessing if needed
* Maintain historical snapshots

---

## Silver Layer

The Silver layer contains cleaned and transformed datasets.

### Transformations Performed

* Schema enforcement
* Null handling
* Deduplication
* Data type conversions
* Standardized column names
* Date formatting
* Data quality validation
* Conversion to Parquet format

### Benefits

* Faster querying
* Better compression
* Optimized analytics performance

---

## Gold Layer

The Gold layer contains business-level analytical datasets.

### Example Analytics

* Most viewed trending videos
* Category-wise trends
* Channel performance analysis
* Regional trending insights
* Engagement metrics
* Daily trending statistics

---

# Project Folder Structure

```text
youtube-trending-analytics/
│
├── lambda/
│   ├── extract_statistics.py
│   ├── extract_reference_data.py
│
├── glue_jobs/
│   ├── bronze_to_silver_statistics.py
│   ├── bronze_to_silver_reference.py
│   ├── silver_to_gold.py
│
├── data/
│   ├── raw/
│   ├── processed/
│
├── architecture/
│   ├── architecture_diagram.png
│
├── README.md
```

---

# YouTube API Data Extraction

The pipeline uses the YouTube Data API v3 to collect trending video information.

## Extracted Fields

* Video ID
* Title
* Channel Name
* Category ID
* Publish Time
* View Count
* Like Count
* Comment Count
* Tags
* Region Code

The extraction process is automated using AWS Lambda.

---

# AWS Lambda

AWS Lambda is used for serverless data ingestion.

## Responsibilities

* Connect to YouTube API
* Fetch trending data
* Convert API responses into JSON/CSV
* Store data into S3 Bronze layer
* Trigger downstream processing

## Benefits

* Fully serverless
* Auto scaling
* Cost efficient
* Event-driven architecture

---

# AWS Glue

AWS Glue is used for ETL (Extract, Transform, Load) processing.

## Glue Crawlers

Glue Crawlers automatically scan S3 data and create metadata tables in the Glue Data Catalog.

## Glue Data Catalog

The Glue Data Catalog acts as a centralized metadata repository for all datasets.

## Glue Jobs

Glue Jobs perform transformations such as:

* Data cleansing
* Schema validation
* Deduplication
* Partitioning
* Parquet conversion
* Aggregation

---

# Athena Queries

Amazon Athena is used to perform serverless SQL queries directly on S3 data.

## Example Queries

### Top 10 Trending Videos

```sql
SELECT title, view_count
FROM youtube_gold
ORDER BY view_count DESC
LIMIT 10;
```

### Most Popular Categories

```sql
SELECT category_name, COUNT(*) AS total_videos
FROM youtube_gold
GROUP BY category_name
ORDER BY total_videos DESC;
```

---

# Data Quality Checks

The pipeline includes multiple data quality validations.

## Validations

* Null value checks
* Duplicate removal
* Invalid record filtering
* Schema consistency
* Standardized timestamps

---

# Notifications and Monitoring

Amazon SNS is used for sending notifications.

## Notifications

* Job success alerts
* Job failure alerts
* Pipeline monitoring updates

CloudWatch is used for:

* Lambda logs
* Glue job logs
* Error monitoring
* Performance tracking

---

# Security

IAM roles and policies are used to provide secure access between AWS services.

## Security Features

* Least privilege access
* Secure S3 bucket permissions
* Role-based authentication
* Controlled service access

---

# Challenges Faced

* Handling nested YouTube API JSON responses
* Managing schema evolution
* Optimizing Glue job performance
* Deduplicating trending video records
* Handling API rate limits

---

# Future Enhancements

* Real-time streaming using Kafka or Kinesis
* Dashboard integration using Power BI or QuickSight
* Machine learning-based trend prediction
* Automated CI/CD deployment
* Data quality monitoring framework
* Multi-region analytics

---

# Key Learnings

* Building serverless data pipelines
* Working with AWS data engineering services
* Implementing ETL workflows
* Managing cloud-based data lakes
* Optimizing analytics pipelines
* Metadata management using Glue Catalog

---

# Conclusion

This project demonstrates how to build a scalable and serverless YouTube Analytics Data Engineering Pipeline using AWS services. It covers data ingestion, transformation, storage, metadata management, querying, monitoring, and analytics using modern cloud-native architecture principles.
