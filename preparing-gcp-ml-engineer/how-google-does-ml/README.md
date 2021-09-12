## Learning objectives

- Use machine learning to transform the way you do business

Data quality supervised learning
Data Pipelines Keras and Tensorflow
Improving Model Accuracy through Feature Engineering
ML Models Optmization / fine tune and experiment / hyperparameters


### ML at google

- classify pictures in google photos
- smart reply in inbox
- targeted ads to display in adswords
- smart reply in inbox
- recommendations for the next video in youtube
- self-driving cars
- spam detection in gmail


Data Engineering with Cloud Data Flow
- to be good at ML, you need to be good at data engineering


### What it means to be AI First

- Artificial Inteligence is a discipline like phisics
- ML is a toolset - solve sort of AI problems

They don't start out inteligent, they become intelingent

First stage
- Learn based on samples/examples - label and input
- the model is a mathematical functions

Data scientist must focus on both the training and inference stage of ML

Second stage
- put model in production and they can run inferences

### Neural network

- neural network are one important tech we use

input -> layer -> layer -> layer -> layer -> output


- too many layers - long time to train and nan and can learn bad 
- avoid the monolithic thinking that one ML model will solve all your problems


OCR - Optical Character Recognition

Sequence to sequence model
- the most complex model in production at google is Gmail smart reply 

RankBrain - Deep Neural Network for search ranking used at google
ML - replace heuristic rules

ML can solve anything that you are writing rules for today? if then else with ML

*idea: ML on testing software ( writes unit tests, integration tests by its own)*


### Pre-Trained ML API-s

Custom ML models
- TensorFlow
- Cloud AI Platform

REST API requests

- Cloud Vision
- Vision API / Cloud Vision
- Speech-to-Text
- Jobs API
- Translation API
- NLP API
- Video Inteliligence API

*idea: Route data based on something*

If you want to use Tensorflow on CCP managed resources, there is a Cloud Machine Learning Engine - Cloud AI Platform Notebook


NLP WaveNet Voice


Lab: Invoking Machine Learning APIs

https://googlecoursera.qwiklabs.com/focuses/17501314?parent=lti_session


AI Platform Notebook

jupyter lab

### It is all about data

How to collect data?
If machine learning is a rocket engine, data is the fuel - ML strategy <-> Data strategy


Training and serving skew
manual analysis help you fail fast, insights from the data

to build a good machine learning algorithm you will have to know your data


You are getting value from ML through predictions

Many ML projects fail because of training-serving skew
The model see the same data ? for batch for streaming? as it saw during training period

How to fix this?

use the same code, Cloud data flow process both batch and stream -> Open source Apache Beam

Perf metrics for training are different than for predictions
- training should scale to handle a lot of data
- predictions should scale to handle large number of queries per second

**ML Training phases**
1. Training phase  labeled data -> ml algorithm -> trained model
2. Inference phasa new data -> served model -> predictions

MLOps is a lifecycle management discipline for machine learning
- continous integration
- continous delivery
- continous training - monitoring, measuring, retraining and serving the model

Testing and validating data, data schemas, models, ML pipeline

DATA

```The real challenge is to build an integrated ML system and maintain it in production```


**Example of data pipeline**

Raw Data -> Data extraction -> Data analysis (EDA - Exploratory Data Analysis ) -> Data preparation ( Feature engineering , split data
, data cleaning, apply transformations )-> Model training -> Model evaluation -> Model validation + Fine tuning and improving of the model
-> Training model -> Model registry -> Model serving -> Prediction service -> Performance monitoring

ML pipeline


**What it means to be AI First**
AI Platform ( previous Cloud ML engine ) helps you build and run your own machine learning applications


Failing fast will allow you to iterate

Unstructured data accounts for 90% of enterprise data ( emails, video footage, texts, reports, catalogs, events, news, etc )



Machine learning - process of computer program writing a computer program to accomplish a task by only looking at a set of examples

The secret success at google - organizational know how

**Avoid these top 10 ML pitfalls**
1. ML requires just as much software infrastructure
2. No data collected yet
3. Assume the data is ready for use
4. Keep humans in the loop
5. Product launch focused on the ML algorithm
6. ML optimizing for the wrong thing
7. Is your ML improving things in the real world
8. Using a pre-trained ML algorithm vs building your own
9. ML algorithms are trained more than once
10. Trying to design your own perception or NLP algorithm


Don't leap into a fully ML Solution

The path to ML

Input > Process -> Outputs -> Insight generation -> tuning -> Process ( Automate every step )

Individual contributor -> delegation -> digitization -> big data -> ml



**What is bias**

picture a shoe, everyone pictured a different type of shoe
now imagine a computer trying to recognize a shoe

machine learning - computer finding a solution by learning from patterns in data

- interaction bias -- most people draw same type of shoe and computer didn't recognize other types
- latent bias - training a computer to recognize phisicist and pass very historic data, woman didn't recognize
- selection bias - model to recognize faces

prevent human bias


### Evaluating metrics for inclusion - Inclusive Machine Learning

evaluate model over subgroups
confusion matrix
Model predictions (positive, negative)
Labels (positive, negative)

acurracy and achieve less false positives and false negatives


Equality of opportunity  -  working for a bank and qualify for a loan

Qualify for classification -> Equal change of selection -> Desired outcome
scrutinized your model



Picking a credit score threshold involves a tradeoff

Threshold too low or too high

maximize the correct decision, granted and payback


Classification and Discrimination must obey the equality of opportuninity principle

A,B - group equaly positive rate ; A - will pay back the loan, B - will not pay back the loan
individuals in A group who qualify for a positive income same chance as the individuals not in A group

**Facets**

A tool from Google that will give users a quick understanding of the distribution of values across features of their datasets
- In facets features are sorted by non-uniformity, with the feature with the most non-uniform distribution at the top
- categorical features
- facets features are sorted by distribution distance
- detect incorrect labelled data

### Python data notebooks in the cloud
- Cloud Data Lab notebooks - runs on compute engines 
- Compute Engine and Cloud Storage
- Cloud data lab with Big Query
- Data Analysis with Big Query
- Machine Learning APIs

AI platform notebooks

**LAB: Analysing data using AI Platform Notebooks and BigQuery**
https://googlecoursera.qwiklabs.com/focuses/17640444?parent=lti_session


Cloud Deployment manager

```!pip install google-cloud-bigquery==1.25.0```

### Summary ML - strategy


Machine learning bias, also sometimes called algorithm bias or AI bias, is a 
phenomenon that occurs when an algorithm produces results that are systematically
prejudices due to erroneous assumptions in the machine learning process.

invoked pre-trained machine learning models