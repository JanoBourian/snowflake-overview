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

## Exploring tables and databases

## Loading data in snowflake



[Index](#section0)

<div id="section2"></div>

# Architecture

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