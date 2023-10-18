# snowflake-overview
A little overview of snowflake topics and most important features

<div id="section0"></div>

# Index

- [Getting started](#section1)
- [Architecture](#section2)
- [Loading Data](#section3)
- [Copy Options](#section4)
- [Unstructured Data](#section5)
- [Performance](#section6)
- [Load from AWS](#section7)
- [Load from Azure](#section8)
- [Load from GCP](#section9)
- [Snowpipe](#section10)
- [Time Travel](#section11)
- [Fail Safe](#section12)
- [Table Types](#section13)
- [Zero-Copy Cloning](#section14)
- [Data Sharing](#section15)
- [Data Sampling](#section16)
- [Scheduling Tasks](#section17)
- [Visualizations](#section18)
- [Streams](#section19)
- [Materialized views](#section20)
- [Data Masking](#section21)
- [Access Management](#section22)
- [Partner Connect](#section23)
- [Best practices](#section24)

<div id="section1"></div>

# Getting started

## Worksheets 

Worksheets are the most important part of our dashboard because in this part you can execute queries. 

```sql
create database snowflake_sample_data from share sfc_samples.sample_data;
grant imported privileges on database snowflake_sample_data to role public;
```

If already exists some database you can query it directly

```sql
SELECT * FROM SNOWFLAKE_SAMPLE_DATA.TPCH_SF1.CUSTOMER;
```

## Architecture

* Storage:
    - Hybrid Columnar Storage
    - Saved in blobs instead of rows
* Query Processing
    - Muscle of the system
    - Performs MMP (Massive Parallel Processing)
    - Virtual Warehouse
* Cloud Services
    - Brain of the system 
    - Managing infraestructure, Access control, security, Optimizer, Metadata, etcetera.

## Virtual warehouse sizes

Or servers size:

* XS: 1
* S: 2
* M: 4
* L: 8
* XL: 16
* 4XL: 128

In enterprise version you can have a Multi-Clustering option.

## Setting up using graph interface

Admin > Warehouse > + Warehouse 

Please check the advanced options.

## Setting up using SQL commands 

```sql
CREATE OR REPLACE WAREHOUSE TESTING_SQL_WH
WITH 
WAREHOUSE_SIZE = XSMALL
MAX_CLUSTER_COUNT = 3
MIN_CLUSTER_COUNT = 1
AUTO_SUSPEND = 300
AUTO_RESUME = TRUE
INITIALLY_SUSPENDED = TRUE
COMMENT = 'This is a testing warehouse created using sql commands';
```

```sql
SELECT * FROM CUSTOMER;
```

```sql
DROP WAREHOUSE TESTING_SQL_WH;
```

## Scalling Policy

Multi-Clustering is key for this approach. Depending on the workload shutdown or star new clusters. 

The auto-scaling is the base policy:

* Standard: default settings
* Economy: conserve credits rather than starting additional warehouses. 

## Exploring tables and databases

Data > Databases > + Database
We can create schemas. 

```sql
create table <table_name> (
    <col1_name> <col1_type>
    -- , <col2_name> <col2_type>
    -- supported types: https://docs.snowflake.com/en/sql-reference/intro-summary-data-types.html
    )
    -- comment = '<comment>';
```

```sql
create or replace TABLE FIRST_DB.FIRST_SCHEMA.FIRST_TABLE (
	TEXTCOLUMN VARCHAR(16777216)
)COMMENT='This is our first table'
;
SELECT * FROM FIRST_DB.FIRST_SCHEMA.FIRST_TABLE;
```

```sql
SELECT * FROM FIRST_DB.FIRST_SCHEMA.FIRST_TABLE;
```

## Loading data in snowflake

```sql
ALTER DATABASE FIRST_DB RENAME TO OUR_FIRST_DB; 

CREATE TABLE "OUR_FIRST_DB"."PUBLIC"."LOAN_PAYMENT" (
  "Loan_ID" STRING,
  "loan_status" STRING,
  "Principal" STRING,
  "terms" STRING,
  "effective_date" STRING,
  "due_date" STRING,
  "paid_off_time" STRING,
  "past_due_days" STRING,
  "age" STRING,
  "education" STRING,
  "Gender" STRING);

//Check that table is empty
USE DATABASE OUR_FIRST_DB;

SELECT * FROM LOAN_PAYMENT;

 
 //Loading the data from S3 bucket
  
 COPY INTO LOAN_PAYMENT
    FROM s3://bucketsnowflakes3/Loan_payments_data.csv
    file_format = (type = csv 
                   field_delimiter = ',' 
                   skip_header=1);
    

//Validate
 SELECT * FROM LOAN_PAYMENT;
```

```sql
-- Exercise
CREATE OR REPLACE TABLE EXERCISE_DB(
ID INT,
first_name varchar,
last_name varchar,
email varchar, 
age INT,
city varchar
) COMMENT='Table based on exercise for unit two';

COPY INTO EXERCISE_DB
    FROM s3://snowflake-assignments-mc/gettingstarted/customers.csv
    file_format = (type = csv 
                   field_delimiter = ',' 
                   skip_header=1);

SELECT * FROM EXERCISE_DB;
```

[Index](#section0)

<div id="section2"></div>

# Architecture

## What is a datawarehouse?

Consolidate and integrate different data sources and working with that information. 

Challenges:
* Work with different formats
* Work with different os.

ETL = Extract, Transform and Load

Different layers:
* Raw data from the data sources (stagin area).
* Data integration (Data transformation).
    * Transformed
    * Cleaned
    * Integrated
* Access layer.
    * Reportging
    * Data Science
    * Other apps

## Cloud computing

Is the step after Data Centers. 

Snowflake is SaaS:
* Application
    * databases, tables, etc

Snowflake:
* Software
* Data
* Operating system

Cloud provider:
* Physical servers
* Virtual machines
* Physical storage

## Snowflake editions

* Standard: introductory level
* Enterprise: additional features for the needs of large-scale enterprises
* Business critical: even higher levels of data protection for organizations with extremely sensitive data
* Virtual private: highest level of security

## Snowflake princing

Compute and storage are separated. 

Storage:
* Monthly storafe fees
* Based on average storage used per month
* Cost calculated after compression
* Cloud providers

Compute:
* Charged for active warehouse per hour
* Dependin on the size of the warehouse
* Billed by second (minimun one minute)
* Charged in Snowflake credits (no usd or euros)

Credit:
* Standard: $2
* Enterprise: $3
* Business Critical: $4

Storage pays:
* On demand Storage
* Capacity Storage

## Monitor Usage

Admin > Usage

## Roles in Snowflake

Admin > Users & Roles

Roles: 
* ACOUNTADMIN
* SECURITYADMIN / SYSADMIN
* USERADMIN
* PUBLIC


[Index](#section0)

<div id="section3"></div>

# Loading Data

[Index](#section0)

<div id="section4"></div>

# Copy Options

[Index](#section0)


<div id="section5"></div>

# Unstructured Data

[Index](#section0)


<div id="section6"></div>

# Performance

[Index](#section0)


<div id="section7"></div>

# Load from AWS

[Index](#section0)


<div id="section8"></div>

# Load from Azure

[Index](#section0)


<div id="section9"></div>

# Load from GCP

[Index](#section0)


<div id="section10"></div>

# Snowpipe

[Index](#section0)


<div id="section11"></div>

# Time Travel

[Index](#section0)


<div id="section12"></div>

# Fail Safe

[Index](#section0)


<div id="section13"></div>

# Table Types

[Index](#section0)


<div id="section14"></div>

# Zero-Copy Cloning

[Index](#section0)


<div id="section15"></div>

# Data Sharing

[Index](#section0)


<div id="section16"></div>

# Data Sampling

[Index](#section0)


<div id="section17"></div>

# Scheduling Tasks

[Index](#section0)


<div id="section18"></div>

# Visualizations

[Index](#section0)


<div id="section19"></div>

# Streams

[Index](#section0)


<div id="section20"></div>

# Materialized views

[Index](#section0)


<div id="section21"></div>

# Data Masking

[Index](#section0)


<div id="section22"></div>

# Access Management

[Index](#section0)


<div id="section23"></div>

# Partner Connect

[Index](#section0)


<div id="section24"></div>

# Best practices

[Index](#section0)