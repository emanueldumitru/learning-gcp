### Introduction to Launching Machine Learning

- Identify why deep learning is currently popular
- Optimize and evaluate models using loss functions and performance metrics
- Mitigate common problems that arise in machine learning 
- Create repeatable training, evaluation and test datasets

Entire purpose of machine learning is to predict on new dataset

Generalization and sampling

### Improve Data Quality and Exploratory Data Analysis ( EDA )

Quality data
- Accurate
- Complete
- Timely
- Consistent


Ways to improve data quality
- resolve missing values
- convert the date feature column to datetime format
- parse date/time features
- remove unwanted values
- convert categorical columns to "one-hot-encodings"


Phases of machine learning:
- training phase

labelled data -> ML algorithm -> trained model 
- inference phase

new data -> served model -> predictions

**LAB: Improving data quality**
https://googlecoursera.qwiklabs.com/focuses/17640973?parent=lti_session


### Exploratory Data Analysis

the purpose of eda is to find theories that can be tested later with the ML part
test assumptions

Approaches to analyse data
- Classical data analysis ( Problem -> Data -> Model -> Analysis -> Conclusions )
- Exploratory data analysis ( Problem -> Data -> Analysis -> Model -> Conclusions )

- Bayesian ( Problem -> Data -> Model -> Prior distribution -> Analysis -> Conclusions )
Determine posterior probababilities using prior probabilities

- EDA is mostly graphic ( plots, etc )

Exploratory data analysis
- Univariate

Categorical, Continous
Numerical EDA using pandas, Visual EDA using plots, seaborn sns, matplotlib

- Bivariate
Category to Category, Category to Contionous, Continous to Category ( relationships )
seaborn, matplotlib

**LAB: Exploratory Data Analyis using Python and BigQuery**
https://googlecoursera.qwiklabs.com/focuses/17641464?parent=lti_session



### Linear regression

weighted sum of inputs

y = w0x0 + w1x1 + ...
y = Xw

The loss function for linear regression is mean squared error


### Perceptron

single layer neural network used as linear binary classifiers 

**LAB: Introduction to Linear Regression**
https://googlecoursera.qwiklabs.com/focuses/17878101?parent=lti_session


**LAB: Introduction to Logistic Regression**

### Decision Trees

Random forest
Ensemble methods
Subsample

Boosting - aggregate multiple weak learners to produce a strong learner

Majority vote

low variance -> better generalization

**LAB: creating decision trees and random forests in python**



### Kernel methods ( non linear activation )
Support vector machines 

small margin, large margin 
maximum likelihood, lower likelihood

distance between support vectors is the margin

data is not lineary separable -- apply kernels to transform the input
space into a more feature space


Deep learning - series of matrix multiplication and some nonlinear transformation
 

### Machine learning models optimization

- quantify model performance using loss functions
- use loss functions as the basis for an algorithm called gradient
- optimize gradient descent to be as efficient as possible
- use performance metrics to make business decisions


ML models are mathematical functions with params and hyperparams

params = real valued variable that changes during model training
hyperparams = setting that we set before training and it does not change afterwards

Linear models have two types of params: bias and weight

hyperplane

LTSM
multi class vs multi label classification


ML problem: How do we predict a baby's health before the are born

Groups of data( quantiles )

Use Gradient descent when an analytical solution is no longer an option
Optimization - search in parameters space -- weight and biases, points in 2D space


## Loss functions

Estimate the quality of models parameters

Composing a loss function by calculating errors

error = actual(true) - predicted value 

One loss function metric is Root Mean Squared Error ( RMSE ) - for regression problems

1. get the errors for the training examples
2. compute the squares of the error values
3. computer the mean of the squared error values

Lower RMSE indicates a better performing model

* Log loss or cross entropy loss is the most used loss function for classification

Finding global minimum

Learning rate - scaling hyperparameter for gradient descent
Hyperparameter tuning


Problem: My model changes every time I retrain it
- loss surface with a global minimum - convex
- loss surface with more than one minima - non-convex

loss surface vary with respect of the numbers of minima that we have 


They are more equivalent parameters



Problem: MOdel training is still too slow
1. Calculate derivative
2. Take a step
3. Check loss

number of data points
number of model parameters


Regularization

Mini-batching reduces cost while preserving quality
Mini-batching - sampling from our training set during training

batch_size - hyperparameters (10-1000 samples)

## Tensorflow Playground

https://goo.gl/EEuEGp

harder dataset to classify

https://goo.gl/ou9iMB - loss function will never get close to 0 , data have a non linear relatioship ( you can't draw a straight like between orange and blue, the two classes)

non-linear decision boundary


Feature engineering
There are more complex models that can solve non-linear decision boundary problems



Activation functions separate non-linear models from neural networks

http://goo.gl/VyoRWX

1 hidden layer with 4 neurons

ReLU and Sigmoid

Neural network to classify a spiral dataset

scatter plots
http://goo.gl/hrXd9T


rate of covergence <-> tpye of batch

neural networks - high hierarchy of features


before neural networks, data scientist spent lot of time on feature engineering

when models overfit they generalize poorly -- generalization and sampling


## Loss curve troubleshooting

- big drops in loss metrics early on ( big steps )
- many smaller steps as we get closer to a minima

learning rate is a hyperparameter
hyperparameter tunning



## Performance metrics

How to choose effective performance metrics

Innapropriate minima??

Reduce the loss function will minimize the wrong predictions

Gradient descent will make incremental change to our weights

Performance metrics 
- after trainings
- easier to understand
- directly connected to business goals

pass models that have innapropriate minima


### Confusion matrix
--------------------

The more false positives the less precision
The more false negatives the less recall


accuracy, precision, recall

### Explore data and asses if your model is overfitting or not


Assess if your model is overfitting
Gauge when to stop model training
Create repeatable training, evaluation and test datasets
Establish performance benchmarks


We want a model that performs great on unseen data, unknown data

Generalization and ML Models

Prediction of the duration of pregnancy base on mother's weigh gain -- regression problem

Loss metrics

mse 
rmse

the closer to 0 is our loss function, the better
free parameter or hyperparameters

rmse = 0? is model production ready or not ? :D
memorizing dataset <-> overfitting <-> a invata mecanic


Split the data to prevent the process of overfitting to take place, the model will have more changes to start generalize well
compare performance on training and test dataset 


When to stop model training?


Start with a NN with one set of hyperparameters - > train model using training dataset
-> increase model complexity ( hyperparameters ) -> is it overfitting?


if it is not overfitting then stop fine tuning
Use model with hyperparameters of last non-overfit model for prediction

Cloud Machine Learning engine can help us with this

Dataset
- Experimental ( Training, Validation )
- Test

Evaluate the final model with cross-validation
Avg validation loss -- bootstraping / cross-validation

if you have lots of data -> use a held-out test dataset
if you don't have lot of data -> use cross-validation


Models that generalize well wil have similar loss metrics or error values across training and validation

Sorting data can add some bias to it


Split a dataset into training/validation/test using the hashing and modulo operators

MOD(ABS(FARM_FINGERPRINT

Develop your Tensorflow code on a small subset of data, then scale it out to the cloud



70 millions of flight data, take only 1.5 % out of it and then split that data ( 800k )

use a hash function instead of naive split in BigQuery -- this to split the data into training, validation and test dataset 

Estimate taxi fare on NYC taxi 

benchmark helps you set a goal for a good value for the error metric. 

Explore / Create ML Datasets / Benchmark --- mandatory to do in any machine learning program



















 


