---
title: "Cherry Blossom Prediction 2026"
except: "Forecasting peak bloom dates using chill accumulation and growing degree days."
---

## Overview
This was my submission to GMU/WSA's Cherry Blossom Competition for 2026. 
It was judged on the aboslute error between your prediction and true bloom peak bloom dates this year for cherry blossoms in five major cities. 
I used a hueristic threshold model based on the cherry blossom tree phenology for my predictions. 
I forecasted the required chill accumulation and growing degree days (GDD) needed based on historic bloom date and temperature data for each city. 
As a current Washington, DC resident, I predicted April 3rd as the peak bloom date for our cities cherry trees. 

> [!NOTE]
> **Nota Bene:** Peak bloom date, per the National Parks Service, is when 70% of the Yoshino cherry trees are in bloom. 


## Dataset
Historical bloom date data was provided by the competition's host. 
All historic temperature data was aquired through the NOAA API, while all predicted temperatures were scraped of the Accuweather website. 
Temperature data was in the form of: TMIN, TMAX, and TAVG

## Methodology
- Simulation function to predict bloom date-of-yea(DOY) using a chill threshold which turns into a heat accumulation threshold in the spring and end when peak bloom supposedly happens
- GDD requirement is estimated from historical bloom dates and averaged
- Grid search for optimal chill threshold
- Rolling Origin Cross-Validation

## Results

Washington, DC: April 3rd, DOY = 93
Kyoto: April 2nd, DOY = 92
Liestal: April 7th, DOY = 97
NYC: March 29th, DOY = 88
Vancouver: April 8th, DOY = 98

## Repository

[View Code](https://github.com/joe-ledford-04/WSA-Petals-and-Probabilities-2026-Team-Data-United-)
