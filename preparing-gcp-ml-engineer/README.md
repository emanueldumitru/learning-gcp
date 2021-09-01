Google Cloud 

1. Data-Driven Decision Making
2. Product Recommandations using Cloud SQL and Spark
3. Real-time IoT Dashboards with Pub/Sub, Dataflow and Data Studio
4. Demand Forecasting using BigQueryML
5. Classify Text and Images using ML APIs, AutoML and DialogFlow
6. Summary

Big data challenges
- migrating existing data workloads
- analyse large datasets
- building streaming data pipelines
- applying machine learning to your data


Google cloud 
- big data and ML products
- compute power
- storage
- networking
- security


Google AI

Sight 
- Cloud Vision
- Cloud Video Intelligence
- AutoML Vision

Language
- Cloud translation
- Cloud natural language
- AutoML Translation
- AutoML Natural Language

Conversation
- Dialogflow Enterprise Edition
- Cloud Text-to-Speech
- Cloud Speech-to-Text

Creating a VM
Create Bucket storage 

gsutil ls gs://<bucket_name>
gsutil cp <file> gs://<bucket_name>


permissions on object storage


Elastic Storage with Google Cloud Storage
- Compute and storage are independent
- 4 types of storage : Standard Storage, Nearline Storage, Coldline storage, Archive Storage

BigQuery dataset, Cloud Storage Bucket, Compute Engine Instance, BigQuery dataset

lab exploring a big query dataset:
https://googlecoursera.qwiklabs.com/focuses/17479053?parent=lti_session



- Cloud Storage
- Dataproc ( spark jobs )
- Bigtable
- Bigquery ( data warehouse andML )
- Cloud SQL ( RDBMS )
- Dataflow
- Datastore
- Pub/Sub
- ML Engine
- Cloud Spanner
- AutoML

App Engine / Cloud Functions - sort of a lamba functions in AWS

App engine - long lived apps
Cloud functions - code triggered by events

Google fully managed database
- Cloud bigtable ( key value, realtime high througput )
- Cloud storage
- Cloud SQL ( a rdbms, one database is enough ) - MySQL and Postgres
- Cloud Spanner ( Horizontal scalability )
- Cloud Datastore ( nosql )
- BigQuery ( latency in seconds, data warehouse )


Cloud pub/sub -> Cloud Data Flow


Recommendation systems
----------------------

ML for housing rentals



RankBrain ( ML for searching )

Machine Learning = examples, not rules

Housing rental recommandations

Cloud data proc for spark jobs  / turn down cluster automatically based on idle time for example
Cloud data proc autoscaling  ( based on Hadoop YARN metrics )
Preemtible VMs

Dataproc 
-------
- hadoop without cluster management
- lift and shift existing hadoop workloads
- connect with cloud storage to separate compute and storage
- re-sze clusters effortlessly. ppremtible vms for cost savings

Lab product reommendations using cloud sql and spark
- what housing rentals should I recommend to my customers based on their history?
-  cloud sql / dataproc / pyspark 


*Lab recommending products using cloud sql and pyspark* 

machinelearning


Predict Visitor Purchases Using BigQuery ML

BigQuery
----------
- it is serverless
- flexible pricing model ( pay as you go, cache queries )
- data encryption and security
- geospatial data types and functions
- foundation for BI and AI

Analyze large datasets at scale
- query 2 billion lines of code in less than 30 seconds


BigQuery 
- fast SQL Query Engine
- Managed storage for datasets

Separate compute and storage 
BigQuery Storage Service ---- petabit network --- BigQuery Query service
Colossus filesystem

Common SQL operations include deduplication and cleansing

Cloud Dataprep - Cleaning and transforming data with a UI

batch or stream via api data to BigQuery

struct / arrays as rows in big query - native data types
datatype RECORD = so a struct

GIS - geographic insights
We can use BigQuery GIS to analyze geographic data

*Big Query has over 130 Public Datasets to explore*


Explore in data studio / BigQuery Geo Viz


Apply machine learning using SQL and BigQuery ML
------------------------------------------------

supervised learning
forecast - linear regression
classify - Logistic Regression
recommend - Matrix factorization

unsupervised learning
clustering

customer lifetime value - how much proffit can we make from a customer
feature columns / feature engineering

onehotencoding categorical
training data / validation data / test data / future data 

Creating ML models with SQL :) 

- StandardSQL and UDFs withing the ML queries
- Linear Regression for forecasting
- Binary and Multi-Class Logistic Regression
- Model evaluations for standard metrics, roc, precision recall 
- model weight inspection
- feature distribution analysis through standard functions

ML project phases
- ETL into BigQuery
- Preprocess features
- actual sql train model
- sql ml evaluate model
- sql ml predictions
- choosing the right model options ( hyperparameters, fine tune)
- prevent overfitting
- inspect what model learned with ml weights
- use ML.evaluate to see model performance

BigQuery ML Cheatsheet
- label = alias a columns as 'label' or specify column in options using input_label_cols
- feature = passed through to the model as part of your SQL SELECT statement
- model = an object created in BigQuery that resides in your BigQuery dateset
- Model types = LinearRegression, LogisticRegression
- Training progress 
- Inspect Weights
- Evaluation
- Prediction

Simpler
- dataset
- create/train
- evaluate
- predict/classify

Lab: Predicting Visitor Purchases with a classification model with BigQuery ML
https://googlecoursera.qwiklabs.com/focuses/17481802?parent=lti_session

Features and labels ( predicting values)

XGBoost - Boosted decision trees
AutoML
DeepNeural Network

Real time IoT Dashboard with Pub/Sub, Dataflow and Data Studio
--------------------------------------------------------------

Variety, Volume, Velocity

Message-oriented architectures using Pub/Sub

IoT devices
Data Ingestion -> Store Cloud Pub/Sub -> Cloud Dataflow -> Cloud Storage / Big Query -> Tableau / Data Studio

Pub/Sub topic 
Designing streaming pipelines with Apache Beam

Apache Beam
- work for both batch and streaming data
- portable

Cloud Data Flow - serverless, no-ops
- handled be default scaling, maintainance
- programming
- data analysis

Data Visualization with Data Studio
- Metrics and dimensions
- ui based way to explore your data

Lab: Creating a Streaming Data Pipeline with Dataflow
- setup a taxi streaming topic in Pub/Sub
- Create Dataflow job from template
- Stream and monitor pipeline in BigQuery
- Analyze results and create some view
- Visualize key metrics in Data Studio

https://googlecoursera.qwiklabs.com/focuses/17484116?parent=lti_session

In this lab, you own a fleet of New York City taxi cabs and are looking to monitor how well your business is doing in real-time. You will build a streaming data pipeline to capture taxi revenue, passenger count, ride status, and much more and visualize the results in a management dashboard.

Dataset from NYC: 
https://opendata.cityofnewyork.us/



Creating a dataset

```
bq mk taxirides
```

Creating a table

```
bq mk \
--time_partitioning_field timestamp \
--schema ride_id:string,point_idx:integer,latitude:float,longitude:float,\
timestamp:timestamp,meter_reading:float,meter_increment:float,ride_status:string,\
passenger_count:integer -t taxirides.realtime
```


Machine Learning on Unstructured Datasets
-----------------------------------------

How does ML on unstructured data work?
Deep learning 
show thousand of photos

input layer - neurons - output layer
use deep learning when you can't explain the labeling rules


Choosing the right ML approach

- pre-build AI models
google translate functions
- vision 
label detection
face detection
ocr extract text from images
explicit content detection
landmark detection
logo detection
- nlp DialogFlow
- automl vision





