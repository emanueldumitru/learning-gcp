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
- Dataproc
- Bigtable
- Bigquery
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


Lab recommending products using cloud sql and pyspark

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
