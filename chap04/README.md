# Chapter 4: Linear Regression

https://bradleyboehmke.github.io/HOML/linear-regression.html

## 4.1 Prerequisites

Using ames_train data set from Section 2.7.

```r
# Helper packages
library(dplyr)    # for data manipulation
library(ggplot2)  # for awesome graphics

# Modeling packages
library(caret)    # for cross-validation, etc.

# Model interpretability packages
library(vip)      # variable importance
```

## 4.2 Simple linear regression

linear regression is really a problem of estimating a conditional mean:

### 4.2.1 Estimation

OLS criterion finds the “best fitting” line by minimizing the residual sum of squares (RSS)

### 4.2.2 Inference

Three major assumptions of the linear regression model:

- Independent observations
- The random errors have mean zero, and constant variance
- The random errors are normally distributed

## 4.3 Multiple linear regression

Interaction effects are quite prevalent in predictive modeling

It is important to understand a concept called the **hierarchy principle** —which demands that all lower-order terms corresponding to an interaction be retained in the model—when considering interaction effects in linear regression models.
