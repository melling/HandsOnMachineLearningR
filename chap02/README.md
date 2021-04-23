# Chapter 2: Model Process

https://bradleyboehmke.github.io/HOML/process.html


With minimal knowledge of the problem or data at hand, it is difficult to know which ML method will perform best. This is known as the no free lunch theorem for ML (Wolpert 1996). 

Approaching ML modeling correctly means approaching it strategically by 
- spending our data wisely 
- on learning and validation procedures
-  properly pre-processing the feature and target variables, 
- minimizing data leakage (Section 3.8.2), 
- tuning hyperparameters, and 
- assessing model performance

```r

# Helper packages
library(dplyr)     # for data manipulation
library(ggplot2)   # for awesome graphics

# Modeling process packages
library(rsample)   # for resampling procedures
library(caret)     # for resampling and model training
library(h2o)       # for resampling and model training

# h2o set-up 
h2o.no_progress()  # turn off h2o progress bars
h2o.init()         # launch h2o

```

can convert any R data frame to an H2O object (i.e., import it to the H2O cloud) 
easily with as.h2o(<my-data-frame>)

**generalizability**

**Training set**

**Test set**

It is critical that the test set not be used prior to selecting your final model.

The two most common ways of splitting data include **simple random sampling** and **stratified sampling**.

### 2.2.1 Simple random sampling

### 2.2.2 Stratified sampling

If we want to explicitly control the sampling so that our training and test sets have similar### Y
### Y
distributions, we can use stratified sampling

more common with classification problems where the response variable may be severely imbalanced (e.g., 90% of observations with response “Yes” and 10% with response “No”).

we can also apply stratified sampling to regression problems for data sets that have a small sample size and where the response variable deviates strongly from normality (i.e., positively skewed like Sale_Price).

## 2.3 Creating models in R


### 2.3.1 Many formula interfaces

Formula rules:Y ~ X where we say “Y is a function of X”.


### 2.3.2 Many engines

meta engines that can be used to help provide consistency.

Meta engines provide you with more consistency in how you specify inputs and extract outputs but can be less flexible than direct engines.

For meta engines, we’ll focus on the **caret** package in the hardcopy of the book while also demonstrating the newer **parsnip** package in the additional online resources.

## 2.4 Resampling methods**

second method is to use a *validation* approach, which involves splitting the training set further to create two parts (as in Section  [2.2](https://bradleyboehmke.github.io/HOML/process.html#splitting) ): a training set and a validation set (or *holdout set*).

**Resampling methods** provide an alternative approach by allowing us to repeatedly fit a model of interest to parts of the training data and test its performance on other parts. The two most commonly used resampling methods include *k-fold cross validation* and *bootstrapping*.

### 2.4.1 k-fold cross validation**


*k*-fold cross-validation (aka *k*-fold CV)

The model is fit on k− 1
folds and then the remaining fold is used to compute model performance.

one typically uses k = 5
or k = 10

LOOCV

*k*-fold CV still tends to have higher variability than bootstrapping

### 2.4.2 Bootstrapping

DISCUSS 

A bootstrap sample is a random sample of the data taken *with replacement*

bootstrap sample is the same size as the original data set from which it was constructed.

original observations not contained in a particular bootstrap sample are considered *out-of-bag* (OOB).


## 2.5 Bias variance trade-off

DISCUSS

many algorithms that are capable of achieving high generalization performance have lots of *hyperparameters* that control the level of model complexity (i.e., the tradeoff between bias and variance).

### 2.5.3 Hyperparameter tuning**


grid search - an automated approach to searching across many combinations of hyperparameter values.

## 2.6 Model evaluation


 it has become widely accepted that a more sound approach to assessing model performance is to assess the predictive accuracy via *loss functions*. 

Loss functions are metrics that compare the predicted values to the actual value (the output of a loss function is often referred to as the *error* or pseudo *residual*).

### 2.6.1 Regression models

**MSE**: Mean squared error

**RMSE**: Root mean squared error

**Deviance**: Short for mean residual deviance. In essence, it provides a degree to which a model explains the variation in a set of data when using *maximum likelihood estimation*

**MAE**: Mean absolute error

**RMSLE**: Root mean squared logarithmic error

**R^2**
: This is a popular metric that represents the proportion of the variance in the dependent variable that is predictable from the independent variable(s). Unfortunately, it has several limitations

**Objective: maximize**

### 2.6.2 Classification models



## 2.7 Putting the processes together

