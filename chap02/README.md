# Model Process

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
