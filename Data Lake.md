# Data Lake

A Data Lake is a centralized repository that allows you to **store**, **process**, and **analyze** vast amounts of 
**structured**, **semi-structured**, and **unstructured** data at any scale. 

Unlike traditional databases, which require data to be structured before storage, a data lake allows raw data to be 
stored as-is and later transformed based on analytical needs.

<br>

**Key Characteristics of a Data Lake**
- ✅ **Stores All Data Types** → Structured (SQL databases), Semi-structured (JSON, XML), and Unstructured (images, videos, logs).
- ✅ **Schema-on-Read** → Data is not transformed before storage, but rather interpreted when read.
- ✅ **Scalable & Cost-effective** → Uses low-cost storage like Amazon S3.
- ✅ **Supports Multiple Processing Engines** → SQL, Machine Learning, AI, Big Data Analytics.
- ✅ **Integration with BI Tools** → Compatible with AWS services, Apache Spark, Presto, and more.

<br>

**Use Cases**
| Use Case                   | Description | Example |
|----------------------------|-------------|---------|
| **Big Data Analytics**      | Store and analyze massive datasets from different sources. | **E-commerce platforms** analyzing customer behavior and trends. |
| **Machine Learning & AI**   | Train ML models using historical and real-time data. | **Predictive maintenance** in manufacturing using sensor data. |
| **Real-time Data Streaming** | Ingest and process streaming data from IoT devices, logs, and transactions. | **Fraud detection** in banking with real-time analysis. |
| **Data Warehousing & BI**   | Act as a source for data warehouses for BI and reporting. | **Retail companies** combining POS, online sales, and supply chain data. |
| **Compliance & Archiving**  | Store logs and records securely for regulatory requirements. | **Healthcare** storing patient records for compliance. |

<br>

**AWS Features Related to Data Lakes**

| AWS Service               | Role in Data Lake |
|---------------------------|------------------|
| **Amazon S3**             | Scalable, durable, and cost-effective storage for raw data. |
| **AWS Glue**              | Createa a schemha for the above data. <br> Serverless ETL (Extract, Transform, Load) to prepare and catalog data. |
| **Amazon Redshift Spectrum** | Queries structured and semi-structured data directly from S3. |
| **Amazon Athena**         | Serverless SQL-based querying on S3 data without infrastructure setup. |
| **AWS Lake Formation**    | Automates the setup of a secure data lake with governance and permissions. |
| **AWS Kinesis**           | Real-time data streaming into the data lake. |
| **Amazon QuickSight**     | BI and visualization tool for insights from data lakes. |
| **AWS IAM & Lake Formation Security** | Provides access control and governance for stored data. |
| **Amazon EMR**            | Big data processing using Spark, Hadoop, and Presto. |
| **AWS Data Pipeline**     | Automates data movement and transformation. |
