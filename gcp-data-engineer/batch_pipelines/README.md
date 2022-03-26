# Build Batch data pipelines with Google Cloud 

- EL, ELT and ETL

EL - data is already clean and correct, good quality 
Cloud Run and Cloud Functions

- ELT experimental datasets where you are not yet sure what kinds of transformations
SQL for transformations

- ETL for complex transformations -- DataFlow and land the data in BigQuery

Extract data from pub/sub, cloud storage, cloud spanner, cloud sql, etc.
Spanner is used for massive scale writes per second
Scalability

Transform data using DataFlow, DataProc or Cloud Data Fusion


Latency, throughput             - Dataflow to BigTable
Spark pipelines                 - Dataproc
Visual pipeline building        - Cloud Data Fusion

Data Lineage
- what format is it in
- what qualities does it have
- Is it fit for the intended use
- Can you transform or process it to make it fit for the intended purposes

Labelling resources for data catalog
Track lineage

Data Catalog metadata as a service


# Running Hadoop on dataproc

- managed hardware and configuration
- simplified version management
- low cost with preemtible vms
- super fast
- resizable clusters
- open source ecosystem
- integrated
- managed
- versioning

use GCS instead of HDFS

setup - configure - optimize - utilize - monitor

!! Run jobs from composer and use metadata

Jupiter network and Colossus storage 
Distcp to move data

# Optmizing Dataproc

- make sure that cloud storage bucket is in the same region as dataproc region
- 10000 input files ( try to combine and union them )

1. Local hdfs is necessary at times
- modify hdfs frequently
- your jobs require a lot of metadata operations
- you heavily use the append operation to hdfs files ( copy objects to a new key )
- heavy IO, partition writes
- You have I/O workloads
- increase / decrease hdfs by increasing/decreasing the size of primary persistent disks

- parallel hints, producer consumer pattern


!! accessing data from another region severe impact of performance ( data is copied on the region)

Persistent clusters are expensive....  efemeral model ( you only pay for what you use)
Cluster scheduled deletion for dataproc clusters, idle

Isolate dev staging and prod on different clusters

1- Create cluster
2- Run job -> store to cloud storage
3- Delete cluster


Yaml template -> DAg -> Create a cluster/Select existing cluster by label / submit jobs / wait on deps / delete cluster -> Dataproc
Scale based on YARN memory


Dataproc autoscaling
- cluster nodes minimum
primary.min_workers and primary.max_workers
scale_up.factor
cooldown_period
graceful_decommision_timeout
scale_down.factor
cooldown_period


# Cloud logging and cloud monitoring

label resources

```
gcloud dataproc jobs sumit hadoop --driver-log-levels
spark.sparkContext.setLogLevel('Debug')
```

dataproc works on top of compute engine resources 


```
git -C ~ clone https://github.com/GoogleCloudPlatform/training-data-analyst


export DP_STORAGE="gs://$(gcloud dataproc clusters describe sparktodp --region=us-central1 --format=json | jq -r '.config.configBucket')"


gsutil -m cp ~/training-data-analyst/quests/sparktobq/*.ipynb $DP_STORAGE/notebooks/jupyter


export PROJECT_ID=$(gcloud info --format='value(config.project)')
gsutil mb gs://$PROJECT_ID

wget https://archive.ics.uci.edu/ml/machine-learning-databases/kddcup99-mld/kddcup.data_10_percent.gz
gsutil cp kddcup.data_10_percent.gz gs://$PROJECT_ID/

# analysis

gsutil cp gs://$PROJECT_ID/sparktodp/spark_analysis.py spark_analysis.py

nano submit_onejob.sh

#!/bin/bash
gcloud dataproc jobs submit pyspark \
       --cluster sparktodp \
       --region us-central1 \
       spark_analysis.py \
       -- --bucket=$1

chmod +x submit_onejob.sh

./submit_onejob.sh $PROJECT_ID
```


# Runnning pipelines usind Dataflow

serverless
use same code for both batch and streaming
apache beam
scalability
low latency

Apache beam - batch + stream

PTransforms ( inputs -> transforms -> outputs )
PCollections are immutable 
Pipeline
Pipeline runners ( backend system, GKE )

Each PCollection can be batch or stream and can be distributed for parallel processing
Unbounded PCollection


Why dataflow? compute and storage

efficient apache beam
- graph optimization
- resource management
- sink
- work scheduler
- resources auto-scaler
- dynamic work rebalancer
- intelligent watermarking
- auto-healing
- monitoring
- log collection
- scaling 
- fully managed and autoconfigure
- groupy by key
- rebalancing using idle machines


Simple Dataflow pipeline

PCollection_In -> PTransform_1 -> PTransform_2 -> PTransform_3 -> PCollection_Out


Read data from local file system, Cloud Storage, Pub/Sub, BigQuery

ParDo transforming data, ParDo implements parallel processing 
ParDo requires code passed as a DoFn function




Lab

```
git clone https://github.com/GoogleCloudPlatform/training-data-analyst

BUCKET="<your unique bucket name (Project ID)>"
echo $BUCKET

cd ~/training-data-analyst/courses/data_analysis/lab2/python
nano grep.py


gsutil cp ../javahelp/src/main/java/com/google/cloud/training/dataanalyst/javahelp/*.java gs://$BUCKET/javahelp

gsutil cp gs://$BUCKET/javahelp/output* .
cat output*

```
more code in dataflow code directory


Data skew makes grouping less efficient at scale


CoGroupByKey joins two or more key-value pairs

CombineFn works by overriding existing operations

Partition splits PCollections into smaller PCollections


```
git clone https://github.com/GoogleCloudPlatform/training-data-analyst
cd ~/training-data-analyst/courses/data_analysis/lab2/python
nano is_popular.py


```


Side inputs and Windows of data
Sliding windows ( capture 60 seconds but a start a new window of 30s ) SlidingWindows(60, 30)


BQ run
```
SELECT
  content
FROM
  `fh-bigquery.github_extracts.contents_java_2016`
LIMIT
  10
```

```
SELECT
  COUNT(*)
FROM
  `fh-bigquery.github_extracts.contents_java_2016`
```

# Dataflow tempaltes and re-using pipeline templates


# Dataflow SQL

- use sql queries to develop and run dataflow jobs from the bigquery web UI 
- you can implement with sql streaming jobs

Data heavily skewed use group by 
PTransforms, GroupByKey and Combine


# How to manage data using Cloud Data Fusion and Cloud Composer

Cloud Data Fusion is a fully managed cloud native enterprise data integration tool to build data pipelines
- cleanse, match, deduplicate, blend, transform, partition, transfer, standardize, automate and monitor
- wrangler framework for data preparation
- data pipeline framework for data operations join, lookup, filtering, etc.
- rules engine tool business data transformation and checks transformations, define complex logic
- metadata aggregator tool - aggregate business, technical and operational metadata .. data lineage - understanding data
- microservice framework - build specialized logic for processing data
- event condition action application -- for IoT event processing 

Cloud Data Fusion UI 
- control center ( application, artifact, dataset )
- pipelines ( developer studio, preview, export, schedule, connector and function pallete, navigation )
- wrangler ( connections, transforms, data quality, insights and functions )
- integration metadata ( search , tags and properties, lineage field and data )
- hub ( plugsin, use cases ,prebuilt)
- entities ( pipeline , application, plugin, driver, library, directive )
- administration ( management -services and metrics and configuration namespace, compute profiles, preferences, system artifacts and rest client )

Cloud Data Fusion 
- build a data pipeline ( graph DAG )

Building and executing a pipeline graph in Cloud Data Fusion

```
gcloud auth list
gcloud config list project
gcloud services disable datafusion.googleapis.com
gcloud services enable datafusion.googleapis.com


export BUCKET=$GOOGLE_CLOUD_PROJECT
gsutil mb gs://$BUCKET
gsutil cp gs://cloud-training/OCBL017/ny-taxi-2018-sample.csv gs://$BUCKET

gsutil mb gs://$BUCKET-temp


SELECT
  zone_id,
  zone_name,
  borough
FROM
  `bigquery-public-data.new_york_taxi_trips.taxi_zone_geom`



  SELECT
  *
FROM
  `trips.trips_pickup_name`


```

# Cloud composer to orchestrate automatic workflow

The heart of any workflow is a DAG


- push ( event triggered , cloud functions )
- pull 

Logging and monitoring



```
gcloud auth list
gcloud config list project

```