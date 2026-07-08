---
title: "Cherry Blossom Prediction 2026"
order: 4
excerpt: "Forecasting peak bloom dates using chill accumulation and growing degree days for GMU/WSA's Cherry Blossom Competition."
---

## Overview
This was my submission to GMU/WSA's Cherry Blossom Competition for 2026. 
It was judged on the aboslute error between your prediction and true bloom peak bloom dates this year for cherry blossoms in five major cities. 
I used a hueristic threshold model based on the cherry blossom tree phenology for my predictions. 
I forecasted the required chill accumulation and growing degree days (GDD) needed based on historic bloom date and temperature data for each city. 
As a current Washington, DC resident, I predicted April 3rd as the peak bloom date for our cities cherry trees. 

> **NB:** Peak bloom date, per the National Parks Service, is when 70% of the Yoshino cherry trees are in bloom. 


## Dataset
Historical bloom date data was provided by the competition's host. 
All historic temperature data was aquired through the NOAA API, while all predicted temperatures were scraped of the Accuweather website. 
Temperature data was in the form of: TMIN, TMAX, and TAVG

## Methodology
- Simulation function to predict bloom date-of-yea(DOY) using a chill threshold which turns into a heat accumulation threshold in the spring and end when peak bloom supposedly happens
- GDD requirement is estimated from historical bloom dates and averaged
- Grid search for optimal chill threshold
- Rolling Origin Cross-Validation

<figure style="text-align: center; margin: 2em 0;">
  <img src="/assets/images/projects/cherry_blossoms_project/rollingorg_cross_val_cherries.png"
       alt="Rolling-origin cross-validation for cherry blossom prediction"
       style="max-width: 100%; border-radius: 6px;">
  <figcaption>
    <strong>Figure.</strong> Rolling-origin cross-validation framework used to evaluate the phenology model. The training window expands over time while each fold predicts an unseen bloom season, providing a realistic assessment of forecasting performance on future years.
  </figcaption>
</figure>

## Results

Washington, DC: April 3rd, DOY = 93
Kyoto: April 2nd, DOY = 92
Liestal: April 7th, DOY = 97
NYC: March 29th, DOY = 88
Vancouver: April 8th, DOY = 98

## Repository

[View Code](https://github.com/joe-ledford-04/WSA-Petals-and-Probabilities-2026-Team-Data-United-)
