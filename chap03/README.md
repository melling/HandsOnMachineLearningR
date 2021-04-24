# Chapter 3: Feature & Target Engineering

https://bradleyboehmke.github.io/HOML/engineering.html

“live with your data before you plunge into modeling” Leo Breiman

## 3.2 Target engineering

not always a requirement, transforming the response variable can lead to predictive improvement, especially with parametric models

the response variable for the Ames housing data (Sale_Price) is right (or positively) skewed

in the House Prices: Advanced Regression Techniques Kaggle competition11, which used the Ames housing data, the competition focused on using a log transformed Sale Price response because “…taking logs means that errors in predicting expensive houses and cheap houses will affect the result equally.” 

There are two main approaches to help correct for positively skewed target variables:

**Option 1**: normalize with a log transformation

transformed_response <- log(ames_train$Sale_Price)

Handle negative numbers 

```r
log(-0.5)
## [1] NaN
log1p(-0.5)
## [1] -0.6931472
```

**Option 2**: use a *Box Cox transformation*

At the core of the Box Cox transformation is an exponent, lambda (λ), which varies from -5 to 5. 

The “optimal value” is the one which results in the best transformation to an approximate normal distribution. 

## 3.3 Dealing with missingness

https://github.com/Quartz/bad-data-guide

Data can be missing for many different reasons; however, these reasons are usually lumped into two categories: *informative missingness* (Kuhn and Johnson 2013) and *missingness at random*

values that are missing at random may deserve deletion or imputation.

### 3.3.1 Visualizing missing values

```r
sum(is.na(AmesHousing::ames_raw))
```

Heat maps are an efficient way to visualize the distribution of missing values for small- to medium-sized data sets.

The code is.na(<data-frame-name>) will return a matrix of the same dimension as the given data frame, but each cell will contain either TRUE (if the corresponding value is missing) or FALSE

vis_miss() function in R package visdat (Tierney 2019) also allows for easy visualization of missing data patterns 

### 3.3.2 Imputation

*Imputation* is the process of replacing a missing value with a substituted, “best guess” value.

#### Statistic Imputation

#### K-nearest neighbor Imputation

all features are quantitative then standard Euclidean distance is commonly used as the distance metric to identify the *k* neighbors and when there is a mixture of quantitative and qualitative features then Gower’s distance (Gower 1971) can be used

**Tree-based**

## 3.4 Feature filtering

Zero and near-zero variance variables are low-hanging fruit to eliminate.

## 3.5 Numeric feature engineering

Numeric features can create a host of problems for certain models when their distributions are skewed, contain outliers, or have a wide range in magnitudes.

Tree-based models are quite immune

### 3.5.1 Skewness

Non-parametric models are rarely affected by skewed features; 

however, normalizing features will not have a negative effect on these models’ performance. For example, normalizing features will only shift the optimal split points in tree-based algorithms. Consequently, when in doubt, normalize.

### 3.5.2 Standardization

must also consider the scale on which the individual features are measured

Models that incorporate smooth functions of input features are sensitive to the scale of the inputs.

Standardizing features includes *centering* and *scaling* so that numeric variables have zero mean and unit variance, 

## 3.6 Categorical feature engineering




### 3.8.3 Putting the process together