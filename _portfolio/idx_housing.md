---
title: "IDXExchange: California Housing Valuation Pipeline "
excerpt: "Predicting the close price for single family homes in California."
collection: portfolio
---

## Overview
Developed an end-to-end machine learning pipeline to estimate residential property values across California using more than 166,000 current real estate transactions. 
The project focused on building a production level, resuable workflow capable of preprocessing raw MLS data, engineering predictive features, training multiple regression models, and evaluating performance on forward-tested data.

## Problem
Residential property valuation requires integrating numerous geographic, structural, and market-related variables while handling missing values, categorical features, and highly skewed distributions. 
The objective was to predict final home sale prices using current transaction data while minimizing prediction error on future unseen properties.

## Dataset
- 166,000+ California residential property transactions
- Multiple monthly MLS exports
- Hundreds of numerical and categorical property features
- Separate training and forward testing datasets to simulate deployment

## Pipeline Architecture
The project was designed as a modular machine learning pipeline consisting of:
- Data ingestion
- Data cleaning and validation
- Missing value imputation
- Feature engineering
- Categorical encoding
- Model training
- Hyperparameter optimization
- Model evaluation
- Prediction generation

Each stage was implemented independently to improve maintainability and allow future experimentation with different preprocessing and modeling techniques.

## Feature Engineering
Feature engineering played a significant role in improving predictive performance.

Key techniques included:
- Haversine distance calculations to major California cities and public beach access
- Target encoding for high-cardinality categorical variables
- Logarithmic transformations for skewed numerical features
- Cyclical month encoding using sine and cosine transformations
- Random sample imputation for missing values
- Boolean feature normalization
- Feature scaling where appropriate for experimentation

## Model Selection
Several regression algorithms were evaluated, including:
- CatBoost (my personal choice)
- LightGBM
- Random Forest
- Baseline regression models

Hyperparameter optimization and cross-validation were used to compare model performance while balancing predictive accuracy and generalization. 
CatBoost ultimately demonstrated the strongest overall performance due to its native handling of categorical variables and missing data.
Hyperparameter optimization was done using the Optuna library and showed little improvment compared to computational cost, due to the strong baseline of CatBoost for this type of problem. 

## Results
The final pipeline achieved strong predictive performance on forward-tested property sales while maintaining a modular architecture suitable for future improvements.

Project outcomes included:
- End-to-end reusable valuation pipeline
- Automated preprocessing workflow
- High-performing gradient boosting models
- Reproducible feature engineering process
- Production-style code organization suitable for future expansion

## Technical Challenges
Some of the most significant engineering challenges included:

- Processing extremely large MLS datasets efficiently
- Combating extreme outliers that were valid listings
- Managing hundreds of categorical variables
- Handling extensive missing data across numerous features
- Preventing data leakage during preprocessing
- Aligning training and testing feature spaces after encoding
- Designing reusable preprocessing functions instead of one-off scripts

## Repository

[View Code]([https://github.com/SebastianGaeta/IDXExchange-DS44])
