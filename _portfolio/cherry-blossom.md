---
title: "Cherry Blossom Prediction 2026"
order: 4
excerpt: "Forecasting peak bloom dates using chill accumulation and growing degree days for GMU/WSA's Cherry Blossom Competition."
---
## Overview

This project was my submission to GMU/WSA's 2026 Cherry Blossom Prediction Competition. The competition evaluated forecasts based on the absolute error between predicted and observed peak bloom dates for cherry blossoms across five major cities.

I built a phenology-inspired forecasting model based on two biological stages of bloom development: winter chill accumulation and spring heat accumulation. The model first estimates when trees satisfy a required chill threshold, then accumulates growing degree days (GDD) until the predicted peak bloom date is reached.

As a Washington, DC resident, I was especially interested in forecasting the city's Yoshino cherry trees. My final prediction for Washington, DC was **April 3, 2026**.

> **Note:** Peak bloom is defined by the National Park Service as the date when 70% of Yoshino cherry blossoms are open.

## Problem

Cherry blossom bloom timing is highly seasonal and temperature-dependent. A useful forecast needs to account for both historical bloom behavior and recent weather patterns while avoiding data leakage from future years.

The goal of this project was to design a simple, interpretable forecasting model that could predict peak bloom dates using historical bloom records, observed temperatures, and forecasted temperatures.

## Dataset

Historical bloom date data was provided by the competition organizers. Temperature data came from two sources:

* Historical daily temperature data from the NOAA API
* Forecasted 2026 temperature data scraped from AccuWeather

The temperature features included:

* Daily minimum temperature (`TMIN`)
* Daily maximum temperature (`TMAX`)
* Daily average temperature (`TAVG`)

## Methodology

The model uses a threshold-based simulation approach inspired by cherry tree phenology.

The process works in two stages:

1. **Chill accumulation:** Count days below a chill threshold during the dormant season.
2. **Heat accumulation:** Once the chill requirement is met, accumulate growing degree days until the estimated bloom requirement is reached.

To tune the model, I performed a grid search over possible chill thresholds. For each threshold, I estimated the required GDD from historical bloom dates and evaluated prediction error.

Because bloom forecasting is a time-dependent problem, I also used **rolling-origin cross-validation**. This allowed the model to train only on past years and predict the next unseen bloom season, creating a more realistic evaluation setup than a random train/test split.

<figure style="text-align: center; margin: 2em 0;">
  <img src="/assets/images/projects/cherry_blossoms_project/rollingorg_cross_val_cherries.png"
       alt="Rolling-origin cross-validation for cherry blossom prediction"
       style="max-width: 100%; border-radius: 6px;">
  <figcaption>
    <strong>Figure.</strong> Rolling-origin cross-validation framework used to evaluate the phenology model. The training window expands over time while each fold predicts an unseen bloom season, providing a realistic assessment of forecasting performance on future years.
  </figcaption>
</figure>

## Results

The final model produced the following 2026 peak bloom predictions:

| City           | Predicted Date | Day of Year |
| -------------- | -------------: | ----------: |
| Washington, DC |        April 3 |          93 |
| Kyoto          |        April 2 |          92 |
| Liestal        |        April 7 |          97 |
| New York City  |       March 29 |          88 |
| Vancouver      |        April 8 |          98 |

For Washington, DC, the optimized model estimated that cherry trees require approximately **54 chill days below 7.2°C**, followed by roughly **204 growing degree days using a 4.4°C base temperature**.

<figure style="text-align: center; margin: 2em 0;">
  <img src="/assets/images/projects/cherry_blossoms_project/dc_peakbloom_histdates.png"
       alt="Historical distribution of Washington, D.C. peak bloom dates"
       style="max-width: 100%; border-radius: 6px;">
  <figcaption>
    <strong>Figure.</strong> Historical distribution of Washington, D.C. peak bloom dates used in the analysis. The figure illustrates the natural year-to-year variability in bloom timing, providing context for the forecasting task and highlighting the range of phenological responses to changing seasonal weather conditions.
  </figcaption>
</figure>

## Technical Challenges

The main challenge was avoiding an overly optimistic evaluation. If the GDD requirement is estimated using all historical years, the model indirectly uses information from the year being predicted. Rolling-origin cross-validation helped correct for this by estimating the GDD requirement only from past years before predicting each future bloom season.

Other challenges included:

* Aligning fall/winter temperature seasons with spring bloom years
* Converting bloom dates into day-of-year targets
* Combining historical temperatures with forecasted 2026 temperatures
* Designing a simple model that remained interpretable

## Repository

[View Code](https://github.com/joe-ledford-04/WSA-Petals-and-Probabilities-2026-Team-Data-United-)
