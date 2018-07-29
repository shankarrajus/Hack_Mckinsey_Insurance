# Mckinsey Insurance Hackathon 

My approach and codes for this hackathon (Leaderboard score: Within top 25%)

## Problem Statement

An insurance firm has presented you with a problem of identifying which policy will get renewed and how much incentives need to be provided for the agents to increase the net revenue.

For every insurance, the client has provided information such as its premium amount, Income, number of times premium missed, etc.  


## Evaluation Metric

The Evaluation Metric for this competition is as follows:
0.75*(AUC score of renewal) + 0.25*(incentives to increase net revenue)

## Submission Format

Policy ID, renewal probability , incentive amount

eg - [23, 0.96754, 1203.43]

# My approach


## Observation on dataset
* 80K training and 30K test rows
* Only 6% of policy is not renewed

## Data transformations

* Categorical variables are converted using dummy variables 

* Using median values for the missing continuous variables. Since boosting algorithms can handle missing values efficiently, defaulted -1 for missing values.


## Feature engineering

Various new fields are derived:
* Amount fields are scaled using MinMaxScaler
* Calculated policy age based on late count and number of premiums paid
* Policy older than year or not
* Calculated age, income, premium bands based on insurer's age, income and premium respectively
* Ratio of premium to the income

## Model selection

* I tried with simple classifier algorithms and found LogisticRegression is better
* LGB and XGB was giving much better performance

## What has worked

* Keeping underwrite_score and premium ratio appears to be best predictors
* Ensemble of 10 XGB improved the score
* Keeping both the derived and actual fields gave little boost
* Ensemble of XGB with LGB improved the score

## What did not worked

* Filling the missing underwrite_score based on premium bands
* Many derived fields reduced the AUC score
* Ensembling of Logistic Regression and Random Forest did not provide much boost
* Optimizing the incentive calculation based on public LB score resulted in overfitting
* SMOTE oversampling, lead to serious overfitting.

## I wanted to try but could not

* Stacking of various model results
* Wanted to experiment the Neural Nets but spent much time on incentive optimization part
