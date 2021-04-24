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


Most models require that the predictors take numeric form. There are exceptions; for example, tree-based models naturally handle numeric or categorical features. However, even tree-based models can benefit from preprocessing categorical features

### 3.6.1 Lumping

Sometimes features will contain levels that have very few observations. For example, there are 28 unique neighborhoods represented in the Ames housing data but several of them only have a few observations.

Sometimes we can benefit from collapsing, or “lumping” these into a lesser number of categories.

Tree-based models often perform exceptionally well with high cardinality features and are not as impacted by levels with small representation

### 3.6.2 One-hot & dummy encoding

Many models require that all predictor variables be numeric. 

The most common way to recode is referred to as one-hot encoding, where we transpose our categorical variables so that each level of the feature is represented as a boolean value

*full rank* encoding

this creates perfect collinearity which causes problems with some predictive modeling algorithms (e.g., ordinary linear regression and neural networks).

Alternatively, we can create a full-rank encoding by dropping one of the levels (level c has been dropped). This is referred to as *dummy* encoding.

Since one-hot encoding adds new features it can significantly increase the dimensionality of our data

### 3.6.3 Label encoding

*Label encoding* is a pure numeric conversion of the levels of a categorical variable. 

If a categorical variable is a factor and it has pre-specified levels then the numeric conversion will be in level order. 

If no levels are specified, the encoding will be based on alphabetical order. 

### 3.6.4 Alternatives

target encoding is the process of replacing a categorical value with the mean (regression) or proportion (classification) of the target variable.

Target encoding runs the risk of *data leakage* since you are using the response variable to encode a feature

## 3.7 Dimension reduction

Dimension reduction is an alternative approach to filter out non-informative features without manually removing them

## 3.8 Proper implementation

we should think of feature engineering as creating a blueprint rather than manually performing each task individually. This helps us in two ways: (1) thinking sequentially and (2) to apply appropriately within the resampling process.

### 3.8.1 Sequential steps

here is a suggested order of potential steps that should work for most problems:

    1	Filter out zero or near-zero variance features.
    2	Perform imputation if required.
    3	Normalize to resolve numeric feature skewness.
    4	Standardize (center and scale) numeric features.
    5	Perform dimension reduction (e.g., PCA) on numeric features.
    6	One-hot or dummy encode categorical features.

### 3.8.2 Data leakage

*Data leakage* is when information from outside the training data set is used to create the model

To minimize this, feature engineering should be done in isolation of each resampling iteration.

### 3.8.3 Putting the process together