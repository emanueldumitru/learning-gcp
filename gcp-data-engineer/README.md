# Data Engineering on Google Cloud

Difference between data lake and data warehouses with Google Cloud
DataFusion?

Pub/Sub for streaming data + DataFlow
BigQuery/BigTable for query analysis

Data engineering - build data pipelines

role of a data engineer
- get the data
- make it usable
- add new value to it
- manage it
- productionize it

Data lake brings data from multiple sources to a Data Lake 
store it to a cloud storage bucket

ETL

Data processing - Dataproc, DataFlow
Streaming data processing - pub/sub. dataflow, bigquery

Data engineering challenges: 
- access to data
- data accuracy and quality
- availability of computational resources
- query performance
- clean, transform and store optimal in a data warehouse


raw data - replicate - data lake - etl - data warehouse

sink for both batch and streaming data pipelines

Visualization - data studio, Tableau

analyze geographic data in Bigquery - 100 000 rows per second

Big Query
- automate data delivery
- make insights accessible
- build the foundation for AI
- tee up real-time insights
- fully managed
- simplify date operations


Cloud SQL, Cloud Storage, Federated query 

store, web, catalog, inventory, promotions -> data lake - > data warehouse



* Big Query BI Engine
* Cloud monitoring / Stackdriver monitoring
* Cloud Audit Logs

Manage data access and governenence

* Cloud data catalog 
* Cloud data loss prevention api ( DLP API )


* Cloud Composer ( apache airflow ) - orchestrate production workflows

# Building a data lake 

- scalable and secure data platform that allows enterprises to ingest,
store, process and analyze any type or volume information.
- data sinks
- data pipelines
- raw data
- orchestration with airflow
- build every aspect of your business operation
- tends to be application-specific

# Data warehouse
- use case is defined
- procesesed, organized, transformed
- provide faster insights
- current, historical data for reporting
- tends to have consistent schemas across applications

high-troughput stream cloud bigtable

data sink

EL - extract and load ( import data as is)
ETL - extract, transform and load
ELT - extract, load and transform


# Cloud storage
- standard
- nearline 30 days
- coldline 90 days
- archive 365 days
- IAM at bucket level, ACL at object level

GMEK - google managed encryption keys

# Data Locking for audits at bucket level and object level

Transactional system are 80 % writes and 20 % reads

Cloud SQL, Spanner sql scaled

```
gcloud auth list
gcloud config list project

export PROJECT_ID=$(gcloud info --format='value(config.project)')
export BUCKET=${PROJECT_ID}-ml

gcloud sql instances create taxi \
    --tier=db-n1-standard-1 --activation-policy=ALWAYS




gcloud sql users set-password root --host % --instance taxi \
--password Passw0rd


export ADDRESS=$(wget -qO - http://ipecho.net/plain)/32

gcloud sql instances patch taxi --authorized-networks $ADDRESS


MYSQLIP=$(gcloud sql instances describe \
taxi --format="value(ipAddresses.ipAddress)")

mysql --host=$MYSQLIP --user=root \
      --password --verbose




create database if not exists bts;
use bts;
drop table if exists trips;
create table trips (
  vendor_id VARCHAR(16),		
  pickup_datetime DATETIME,
  dropoff_datetime DATETIME,
  passenger_count INT,
  trip_distance FLOAT,
  rate_code VARCHAR(16),
  store_and_fwd_flag VARCHAR(16),
  payment_type VARCHAR(16),
  fare_amount FLOAT,
  extra FLOAT,
  mta_tax FLOAT,
  tip_amount FLOAT,
  tolls_amount FLOAT,
  imp_surcharge FLOAT,
  total_amount FLOAT,
  pickup_location_id VARCHAR(16),
  dropoff_location_id VARCHAR(16)
);


gsutil cp gs://cloud-training/OCBL013/nyc_tlc_yellow_trips_2018_subset_1.csv trips.csv-1
gsutil cp gs://cloud-training/OCBL013/nyc_tlc_yellow_trips_2018_subset_2.csv trips.csv-2


mysqlimport --local --host=$MYSQLIP --user=root --password \
--ignore-lines=1 --fields-terminated-by=',' bts trips.csv-*

```

# Building a data warehouse

- a dwh should consolidate data from many resources
- impose a schema / consolidated data / schema 
- high speed query performance 
- serverless
- no-ops, including ad-hoc queries
- big query are not optimize for updating!!!!
- focus on the fact that query are based only on few columns
- big query slots! ( cpu, ram and network )
- execution details 


10b - 415 GB 10 seconds bigquery perf
100b - 4.1 TB 30 seconds  bigquery perf

IAM access on datasets, tables, views

ROW-LEVEL security in BigQuery
Authorized views / Materielized views ( persisted views, the table is not queried all the time)
Big query will keep the views up to date

Query native tables / external storage files ( GCS ; federated queries )
You can separate cost of storage and cost of queries


BQ addresses backup and disaster recovery at the service level ( time travel )
Data backfills ( adding missing past data to fill the gaps)


# Loading data into bq

```
bq load \
--source_format=CSV \
--autodetect \
--noreplace  \
nyctaxi.2018trips \
gs://cloud-training/OCBL013/nyc_tlc_yellow_trips_2018_subset_2.csv
```

# Nested datam json, structs, arrays

structs records, arrays repeated
arrays can be part of regular fields or structs
a single table can have many structs

UNNEST command

- instead of joins use nested repeated fields denormalized tables
- normalized under 10GBs use join
- denormalized over 10Gbs

finding the number of elements with ARRAY_LENGTH(<array>)
deduplicating elements with ARRAY_AGG(DISTINCT <field>)
ordering elements with ARRAY_AGG(<field> ORDER BY <field>)
limiting ARRAY_AGG(<field> LIMIT 5)

You need to UNNEST() arrays to bring the array elements back into rows
UNNEST() always follows the table name in your FROM clause (think of it conceptually like a pre-joined table)


Recap of STRUCTs:

A SQL STRUCT is simply a container of other data fields which can be of different data types. The word struct means data structure. Recall the example from earlier:

__STRUCT(__"Rudisha" as name, [23.4, 26.3, 26.4, 26.1] as splits__)__AS runner

STRUCTs are given an alias (like runner above) and can conceptually be thought of as a table inside of your main table.

STRUCTs (and ARRAYs) must be unpacked before you can operate over their elements. Wrap an UNNEST() around the name of the struct itself or the struct field that is an array in order to unpack and flatten it.


# Optimize with partitioning and clustering

ingestion time, timestamp, datetime, date, timestamp, integer typed column
automatically partition by date, expire partition

cluster organize data into multiple blocks -- filtering pe cluster columns

auto reclustering as you get new data -- free

use FAKE data partition with all columns null if you want to use Clustering without partitioning

Data engineer build data pipelines

