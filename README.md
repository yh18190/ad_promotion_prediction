# Problem : ad promotion prediction

This repository is based on ad promotion prediction problem whether user would like/click a particular ad based on historical promotions displayed to users 

- Given: much data on past  promotional ads performance and whether or not users clicked on those links.
- Predict: the probability/likelihood that a  user will click/like on a given ad. Basically its a CTR(Click through rate Prediction) problem which is a kind of binary classfication task with evaluation metric being logarthmic loss(log_loss).A model with lower impression logloss is preferred and is often used as an indicator of model performance in online advertisement industry.


# Data Description

Features Description :All features are categorical, with some non-visible feature names and hashed values.This dataset has 40Million records for 11 days of ad clicks/impressions collected during 21st Dec 2019 till 30th Dec 2019 .The dataset has 17% success rate(liked/click rate) and 83% of unclicked/disliked ads.


- like: 0/1 user likes the promotion or not (target variable)
- hour: YYMMDDHH format
- sid: site id
- sdomain: site domain
- scat: site category
- aid: mobile application id
- adomain: mobile application domain
- acat: mobile application category
- did: mobile device id
- dip: ip of the originating request
- dmodel: device mode: iphone, samsung, nokia, etc..
- dtype: device type: smartphone, tablet, etc..
- dconn: connection used by the device: 4G, WIFI, etc..
- pos: position where the promotion was displayed on the user’s mobile
- A-I: non-visible feature names

 Number of impressions = number of times an advertisement was served/offered
 
 Number of Clicks = number of times an ad was clicked/liked out of interest

# Notebooks:

- Data_Preparation_Transformations.ipynb :  The code is used for analysing,cleaning and transforming the data to generate training dataset with additional new features being created as part of feature engineering process. It also contains visualizations of relationships between the data attributes for analysis.I have also included  report(pandas profiling) of EDA analysis  and data attributes distribution/visualization in Visual_Analysis.html. 

- Modelling.ipynb : The entire modelling of training data is part of this code.Have tried 5 different models including hyperparameter tuning and H2o AutoML ensemble modelling.


# Challenges:
Its a huge dataset when loaded is over 5GB(40 Million records). In memory sklearn transforms and models pretty much cause the python process to run out of memory and processing issues. Considering the time constraint and other factors of visualisation etc , Instead I had to choose randomly sampled subset dataset to 1Million records.

Feature engineering: In order to optimise the memory consumption and other curse of dimensionality/cardinality issues I choose Hashing technique instead of One-hot encoding or label encoding techniques.If we choose One hot encoding etc then we might run out of memory considering the categories in certain columns having huge number of unique values.

Modelling Phase : Considering the time constraints and size of dataset, I managed to stick to few hyperparameter tuning and algorithms.


# Algorithms Trained:

- Logistic Regression 											(Log_loss 0.6931)
- Random forest classifier	 								(Log_loss 0.5270)
- LightGBM Classifier Default Paramters 		(Log_loss 0.404813)
- Xgboost Classifier 												(Log_loss 0.40139)
- LightGBM -Hyperparamter Tuned(few parameters only because of time constraints etc) (Log_loss 0.39895781)
- Xgboost -Hyperparamter Tuned(few parameters only because of time constraints etc)  (Log_loss 0.40226)
- H2o AutoML (GBM Ensemble Model) (Log_Loss 0.3997)


# Areas of Improvement 

- 1.Hyperparamter Tuning using Gridsearch/RandomsearchCV/Hyperopt and other  tuning techniques to be implemented to further finetune models.Right now because of the size of dataset and also time constraints,I couldnot spend more time on this aspect of modelling.

- 2.Incremental learning and other Stocastic Gradient techniques could be used to learn the whole dataset in chunks instead of relying on random sample.We can also use PySpark MLLib to handle such bigdatasets in cluster environment.

- 3.FFM(Field Aware Factorization Machines) algorithms have proven better in online ad CTR prediction.This could be implemented using LibFFM library or xlearn.Factorization Machines are usually trained by using one of the three main solvers – Stochastic Gradient Descent (SGD), Alternative Least Squares (ALS) or Markov Chain Monte Carlo (MCMC).

- 4.Encoding technqiues like Mean encoders or Onehot encoders could be tried to see the effect of curse of dimensionality during training process.

- 5.As part of feature engineering , did(device id),device ip(dip),device model(dmodel) could be merged to get better representation of users.As we have seen 85% of data is originating from one single device.We can identify the user with device id if it is not null and device ip(dip) + device model(dmodel) for others.

- 6.Similarly Site ID (sid),Site domain (sdomain) could be merged to better represent publishers site.

- 7.Recursive Feature elimination and other feature selection techniques can be tried for reducing the feature space etc.








