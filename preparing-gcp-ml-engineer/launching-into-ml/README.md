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
 







