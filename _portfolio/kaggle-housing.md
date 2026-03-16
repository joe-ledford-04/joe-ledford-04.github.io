---
title: "California Housing Price Prediction"
excerpt: "Machine learning model predicting housing prices. Top 10% finish with RMSE of 0.12106."
image: /assets/images/kaggleVisualization.png
---

## Overview

I built a machine learning model predicting housing prices in Ames, Iowa for the Kaggle Housing Price Competiton.
This was my first serious attempt at making a machine learning model and we extremely motiavated by the results.  
It paved the way for my internship at IDX Exchange, working on the same task, but at the industry level with lots more cleaning and feature engineering required.  
 


## Dataset

The dataset for this competiton included 1459 observations of residential homes in Ames, Iowa. 
It had 79 features variables with around 60% of them being mumeric. 

## Methodology
- Mode and constant value imputation for missing values
- Log transformations for skewed numeric features
- Sinsodial transoformation for cyclical feautres 
- Dummy encoding for categoricals
- Scaling
- target transformation
- Pycaret library for model comparison and feature importance
- Optimized using Optuna library
- Bagging Ensemble using:
  - CatBoost Regressor
  - Bayesian Ridge
  - LightGBM
  - Ridge Regressor
- Cross validation using K-Fold

## Results
My final model ended with an RMSE of 0.12381, ranking Top 511 globally at the time.

## Repository

[View Code](https://github.com/joe-ledford-04/Kaggle-Housing-Price-Competition)
