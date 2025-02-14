# Data Engineering YouTube Analysis Project

## Overview
This project aims to securely manage, streamline, and analyze structured and semi-structured YouTube video data based on video categories and trending metrics.

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

## Data Flow and Architecture
### 1. Data Ingestion
- YouTube trending video data (structured and semi-structured) is collected.
- Raw data is uploaded to Amazon S3 (Landing Area).

### 2. Data Processing
- AWS Glue processes and transforms data (removing null values, categorization, etc.).
- AWS Lambda is used for additional transformations such as filtering, aggregations, and JSON to Parquet conversion.

### 3. Data Storage (Data Lake)
- Cleansed/enriched data is stored in Amazon S3 for further processing.

### 4. Data Access
- AWS Athena allows querying the structured dataset.

### 5. Data Architecture

## Data Flow Diagram
Our Data Architecture
# Our Data Architecture

## Data Flow
# Our Data Architecture

## Data Flow
```mermaid
graph TD;
    %% Source Systems
    A[Source Systems] -->|Bulk| B[S3 API];

    %% Data Platform
    subgraph Data Platform
        subgraph Data Lake
            C[S3 Landing Area] --> D[S3 Cleansed / Enriched];
            D --> E[S3 Analytics / Reporting];
        end
        subgraph Data Processing
            F[AWS Glue] --> G[AWS Glue Data Catalog];
            F --> H[AWS Lambda];
        end
    end

    %% AWS Step Functions
    X[AWS Step Functions] -->|Triggers Processing| F;

    %% Data Flow Connections
    B --> C;
    E -->|Processed Data| F;
    G -->|Catalogued Data| I[AWS Athena];

    %% Analytical Data Access
    I --> J[API];
    J --> K[Analytical Data Access];
    K --> L[Redshift (Optional)];

    %% Monitoring / Alert
    subgraph Monitoring / Alert
        M[AWS CloudWatch];
    end

    %% Target Systems
    subgraph Target Systems
        N[Notebooks (Optional)];
        O[QuickSight];
        P[Power BI (Optional)];
        Q[Qlik];
    end



    %% IAM & Security
    subgraph AWS Identity & Access Management
        IAM[AWS IAM];
    end

    IAM -.->|Access Control| B;
    IAM -.->|Access Control| J;
    IAM -.->|Access Control| K;
```

---

## S3 bucket file import from terminal:
# To copy all JSON Reference data to same location:
aws s3 cp . s3://dataeng-on-youtube-raw-euwest2-vishw/youtube/raw_statistics_reference_data/ --recursive --exclude "*" --include "*.json"

### 5. Reporting and Analytics
- Business intelligence tools such as QuickSight, Power BI, and Qlik generate insights.
- Engagement metrics like views, likes, and comments are analyzed for trend patterns.

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

