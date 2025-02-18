# Data Engineering YouTube Analysis Project

This project aims to build an end-to-end data engineering pipeline that ingests, processes, analyzes, and visualizes YouTube trending video data. By leveraging Amazon Web Services (AWS) for data processing and Power BI for data visualization, the project transforms raw data into actionable insights.

## Project Overview

The primary goal of this project is to construct a data pipeline that processes YouTube trending video data to uncover trends and patterns across different regions. The pipeline utilizes AWS services for data storage, processing, and analysis, while Power BI is employed for creating interactive visualizations.

## Tools and Technologies Used

- **AWS S3 (Simple Storage Service)**: Scalable storage for raw and processed data.
- **AWS Glue**: Managed ETL (Extract, Transform, Load) service for data preparation and transformation.
- **AWS Lambda**: Serverless compute service for automating data processing tasks.
- **AWS Athena**: Interactive query service for SQL-based querying of data stored in S3.
- **Power BI**: Business analytics tool for creating interactive visualizations and dashboards.
- **AWS IAM (Identity and Access Management)**: Manages user access and permissions for AWS resources.

## Project Goals
- **Data Ingestion** – Build a mechanism to ingest data from different sources.
- **ETL System** – Transform raw data into a structured format.
- **Data Lake** – Centralized storage for multiple sources.
- **Scalability** – Ensure the system can scale as data size increases.
- **Cloud Infrastructure** – Utilize AWS for efficient data processing.
- **Reporting** – Develop a dashboard for insights and analytics.

## Services Used
- **Amazon S3** – Object storage for data lakes.
- **AWS IAM** – Identity and Access Management.
- **Power BI** – Business intelligence and analytics.
- **AWS Glue** – Serverless ETL for data processing.
- **AWS Lambda** – Compute service for data transformation, including JSON to Parquet conversion.
- **AWS Athena** – Interactive querying of S3 data.


### Data Ingestion
## 1. Data Collection
Obtain the YouTube trending videos dataset from Kaggle. This dataset includes daily records of trending videos across multiple regions, provided in JSON and CSV formats.

## 2. Uploading Data to S3
Upload the collected dataset to the Landing Zone in S3 using the AWS CLI:
## S3 bucket file import from terminal:
# To copy all JSON Reference data to same location:
aws s3 cp . s3://dataeng-on-youtube-raw-euwest2-vishw/youtube/raw_statistics_reference_data/ --recursive --exclude "*" --include "*.json"

## 3. Automating Ingestion with AWS Lambda
Set up AWS Lambda functions to automate the ingestion process. Configure S3 event triggers to invoke Lambda functions whenever new data is uploaded, ensuring real-time data processing.

### Data Processing and Transformation
## 1. Cataloging with AWS Glue
Use AWS Glue Crawlers to scan the raw data in the Landing Zone. Crawlers automatically infer the schema and create metadata tables in the AWS Glue Data Catalog, making the data readily accessible for querying.

## 2. ETL Jobs with AWS Glue
Develop AWS Glue ETL jobs to perform data cleaning and transformation tasks:

 Data Cleaning: Handle missing values, standardize data formats, and correct inconsistencies.
 Data Transformation: Parse JSON structures, extract relevant fields, and convert data into columnar formats like Parquet for efficient querying.

## 3. Storing Processed Data (Data Lake)
Save the transformed data to the Cleansed Zone in S3, organizing it into partitions (e.g., by region and date) to enhance query performance.

### Data Analysis
## Querying with AWS Athena
# Configure AWS Athena to query the processed data stored in S3:
1. Connecting to the Data Catalog: Athena integrates with the AWS Glue Data Catalog, allowing seamless querying of the cataloged data.
2. Running SQL Queries: Use standard SQL syntax to perform exploratory data analysis, aggregating metrics such as view counts, likes, dislikes, and comment counts across different video categories and regions.

# Creating Views
Define views in Athena to encapsulate complex queries, simplifying future analyses and promoting reusability.

### Data Visualization
## Exporting Data for Power BI
After analyzing the data with Athena, export the query results to S3 in a format compatible with Power BI, such as CSV or Parquet.

## Connecting Power BI to S3
Use Power BI's Amazon S3 connector to import the processed data:

Data Source Configuration: In Power BI, select the S3 connector and provide the necessary credentials and bucket details to access the data.
Data Preparation: Utilize Power BI's Power Query Editor to perform any additional data transformations or calculations as needed.

### Building Dashboards
Design interactive dashboards in Power BI to visualize key insights:
Trend Analysis: Visualize trends in video popularity over time, identifying patterns in viewership.
Geographical Insights: Create maps and charts to compare trending metrics across different regions.
Category Performance: Analyze performance metrics across various video categories to determine audience preferences.

## Dashboard Insights
<img width="1280" alt="Screenshot 2025-02-02 182856"  src ="https://github.com/user-attachments/assets/5bb94cd6-3c55-41ec-9036-bb9d23e96bf3">
The dashboard provides detailed visualizations and analysis on the following:
- **Total Views, Likes, and Trending Rank**: Overview of total engagement across different categories.
- **Engagement by Video Category**: Comparison of video types and their popularity.
- **Region-based Virality Analysis**: Understanding how engagement varies across different geographical regions.
- **Engagement Rate Over Time**: Identification of trends and seasonal variations in video popularity.
- **Comment Analysis**: Impact of comments being enabled or disabled on engagement levels.

## Features of the Dashboard
- **Filters for Region and Category**: Enables targeted analysis.
- **Virality Index Calculation**: Measures how quickly videos gain traction.
- **Comparison of Video Engagement**: Helps identify which types of content perform best.
- **Trend Tracking**: Helps businesses and creators optimize their content strategies.

## Automation and Scheduling
# Orchestrating with AWS Glue Workflows
Use AWS Glue Workflows to define and manage the sequence of ETL jobs:
Workflow Definition: Create workflows that specify the order of job execution, including dependencies and conditional triggers.
Monitoring and Alerts: Set up monitoring to track job execution status and configure alerts for failures or anomalies.

# Event-Driven Processing with AWS Lambda
Enhance automation by configuring AWS Lambda functions to respond to specific events:
S3 Event Triggers: Set up triggers that invoke Lambda functions upon new data uploads, initiating ETL processes automatically.
Scheduled Events: Use Amazon CloudWatch Events to schedule periodic execution of Lambda functions for regular data processing tasks.

## Why Use Parquet Instead of JSON
Parquet is a columnar storage file format optimized for analytical queries, whereas JSON is a row-based format primarily designed for data interchange. The advantages of using Parquet over JSON include:
Efficient Query Performance: Parquet's columnar structure allows for reading only the necessary columns, reducing I/O operations and speeding up query execution.
Reduced Storage Costs: Parquet files are highly compressed, often resulting in significantly smaller file sizes compared to JSON. This compression reduces storage costs and improves data retrieval times.
Schema Enforcement: Parquet enforces a predefined schema, ensuring data consistency and making it suitable for structured data analysis.


## Key Questions Answered
- What are the most popular YouTube video categories based on engagement?
- How does video engagement vary across different regions?
- Which videos have the highest virality index?
- How does disabling comments impact engagement levels?
- What are the trends in video popularity over time?

## Conclusion
This project successfully integrates YouTube trending data into a scalable AWS-based data pipeline, enabling efficient storage, processing, and analysis. The insights derived from the dashboard provide valuable information to content creators, businesses, and analysts. By leveraging AWS Glue, Lambda, Athena, and visualization tools like Power BI, the system ensures effective data handling and reporting. The results offer actionable insights for optimizing content strategies, identifying trends, and understanding regional engagement patterns.

## Dataset
https://www.kaggle.com/datasets/datasnaek/youtube-new?resource=download

