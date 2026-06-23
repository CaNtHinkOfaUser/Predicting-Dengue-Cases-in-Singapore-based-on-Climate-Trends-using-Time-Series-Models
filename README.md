# Dengue Case Prediction Using Climate Variables

## Overview

This project investigates the relationship between climate conditions and dengue outbreaks in Singapore by developing machine-learning and statistical forecasting models to predict future dengue case trends.

The study combines historical dengue case counts with weather variables, including rainfall, temperature, and wind speed, to assess whether environmental factors can be used to forecast dengue transmission patterns. By leveraging time-series modelling techniques, the project aims to provide insights that may support public health planning and early intervention efforts.

---

## Problem Statement

How can climate variables be used to predict future dengue outbreaks in Singapore?

We can predict dengue outbreak cases in Singapore by analysing climate trends such as temperature, rainfall, and humidity, which are increasingly affected by global warming. These factors influence the breeding and activity of Aedes mosquitoes, the primary carriers of dengue. By using predictive models that incorporate such climate data, public health agencies can prepare in advance, allocate resources more efficiently, and issue timely alerts to the public. This benefits not only health authorities but also citizens, who can take preventive action, and researchers, who can use the data to inform policy. However, challenges include the complexity of the factors influencing dengue beyond climate alone, the need for high-quality, localised data, and the risk of inaccurate predictions. Despite these challenges, climate-informed forecasting offers a valuable tool for reducing infections, managing outbreaks proactively, and building a more resilient public health system in the face of climate change.						

## Dataset

https://data.gov.sg/datasets?query=dengue&resultId=d_ac1eecf0886ff0bceefbc51556247015&page=1
https://data.gov.sg/datasets?query=weather&resultId=d_03bb2eb67ad645d0188342fa74ad7066&page=1&dataExplorerPage=286&columnLegendPage=1

### Dengue Data

* Weekly dengue case counts
* Years analysed: 2014–2017
* Epidemiological week information included

### Weather Data

* Mean daily rainfall
* Mean temperature
* Mean wind speed
* Maximum wind speed

The datasets were cleaned, merged, and transformed into a unified time-series format suitable for forecasting.

## Methodology

### Data Preprocessing

The preprocessing stage involved:

* Cleaning missing and inconsistent values
* Aligning weather and dengue datasets by epidemiological week
* Transforming data into a time-series format
* Exploratory data analysis and visualisation

This ensured that all variables were suitable for modelling and forecasting.

## Exploratory Data Analysis

Several visualisations were created to identify seasonal trends and relationships between weather patterns and dengue outbreaks.

### Total Dengue Cases by Year

This visualisation was used to compare overall dengue incidence across different years and identify periods of elevated transmission.

<img width="930" height="556" alt="image" src="https://github.com/user-attachments/assets/411f5b9f-5046-49ea-a1f9-ad5d204c8be6" />

### Average Weekly Dengue Cases Across All Years

This graph was designed to identify seasonal patterns by averaging weekly dengue cases across all years.

#### Key Observations

* Dengue cases increase noticeably between epidemiological weeks 25–35.
* Peak transmission commonly occurs around July.
* Case counts generally decline towards the beginning and end of the year.
* The recurring pattern suggests strong seasonal influences on dengue transmission.

Possible contributing factors include:

* Increased rainfall creates mosquito breeding sites
* Warmer temperatures are accelerating mosquito development
* Higher humidity improves mosquito survival

<img width="930" height="473" alt="image" src="https://github.com/user-attachments/assets/f7387df9-9a3e-416c-abcc-abf8d0018bb1" />


### Weather Variable Trends

The following weather indicators were analysed across the study period:

* Mean Daily Rainfall
* Mean Temperature
* Mean Wind Speed
* Maximum Wind Speed

#### Mean Daily Rainfall

* Clear seasonal fluctuations were observed.
* Recurring peaks correspond to monsoon periods.
* Rainfall may increase mosquito breeding opportunities through stagnant water accumulation.
  <img width="862" height="268" alt="image" src="https://github.com/user-attachments/assets/0975b928-05b7-4d0c-8a48-436ade227b4d" />

#### Mean Temperature

* Temperatures remained relatively stable throughout the year.
* Slight increases were observed during mid-year periods.
* Warmer temperatures may accelerate mosquito reproduction and virus incubation.
<img width="866" height="269" alt="image" src="https://github.com/user-attachments/assets/50372f8b-cf85-4af1-b7b2-80a860b66986" />

#### Mean Wind Speed

* Wind speed fluctuated throughout the year.
* Seasonal peaks may influence mosquito movement and habitat suitability.

<img width="866" height="281" alt="image" src="https://github.com/user-attachments/assets/82a530ad-61ba-4108-b9f0-85493387b033" />

#### Maximum Wind Speed

* Sharp spikes corresponded to short-term weather events and storms.
* Such events may affect mosquito populations and human activity patterns.
<img width="875" height="295" alt="image" src="https://github.com/user-attachments/assets/f23844a0-0ad3-4726-ab0f-2b45f0a2bebf" />

Collectively, these observations support the hypothesis that climate conditions influence dengue transmission.

## Models Evaluated

Two forecasting approaches were evaluated and compared.

### Model 1: Vector Auto Regression (VAR)

VAR is a multivariate time-series forecasting model that captures relationships among multiple variables simultaneously.

This makes it particularly suitable for dengue prediction because multiple weather variables may influence disease transmission.

#### Hyperparameter Tested

Trend Vector Configuration:

1. Constant
2. Constant + Linear
3. Constant + Linear + Quadratic

### Model 2: Auto-Regressive Integrated Moving Average (ARIMA)

ARIMA is a traditional univariate forecasting model that predicts future values based primarily on historical trends.

#### Hyperparameters Tested

* Auto-regression order (p)
* Differencing degree (d)
* Moving average order (q)

Configurations evaluated:

* p = 4
* d = 2
* q = 5

## Evaluation Metrics

### Akaike Information Criterion (AIC)

AIC evaluates model performance while penalising unnecessary complexity.

Lower values indicate a better balance between accuracy and simplicity.

### Bayesian Information Criterion (BIC)

BIC is similar to AIC but applies a stronger penalty to complex models.

Lower values indicate superior performance.

<img width="700" height="419" alt="image" src="https://github.com/user-attachments/assets/d572b461-69b4-4dc4-a91e-1d84215cf3da" />


## Hyperparameter Tuning Results

### VAR Results

| Configuration                 | AIC   | BIC    |
| ----------------------------- | ----- | ------ |
| Constant                      | -24.8 | -24.1  |
| Constant + Linear             | -12.4 | -11.6  |
| Constant + Linear + Quadratic | -10.1 | -9.148 |

#### Best VAR Configuration

Constant trend vector

* AIC = -24.8
* BIC = -24.1

This configuration achieved the lowest scores and therefore demonstrated the strongest performance.

### ARIMA Results

| Configuration | AIC    | BIC    |
| ------------- | ------ | ------ |
| p = 4         | 2721.0 | 2742.4 |
| d = 2         | 2762.5 | 2773.2 |
| q = 5         | 2720.7 | 2738.5 |

#### Best ARIMA Configuration

Moving average order: q = 5

* AIC = 2720.7
* BIC = 2738.5

## Model Comparison

| Model | Best AIC | Best BIC |
| ----- | -------- | -------- |
| VAR   | -24.8    | -24.1    |
| ARIMA | 2720.7   | 2738.5   |

The VAR model significantly outperformed ARIMA across both evaluation metrics.

This suggests that incorporating multiple weather variables provides a substantial advantage when modelling dengue transmission patterns.

## Prediction Results

### VAR Forecast

<img width="501" height="443" alt="image" src="https://github.com/user-attachments/assets/85a7d895-5a02-4f5b-b956-d2ceb8cd39de" />


### ARIMA Forecast

<img width="341" height="439" alt="image" src="https://github.com/user-attachments/assets/6ec7c680-c35d-4f64-9ca4-82309aacd280" />


The "number" column represents the number of dengue cases predicted for the next few years for ARIMA and VAR model.									

## Evaluation on Test Data

The VAR model produced realistic forecasts and successfully captured interactions between weather variables and dengue cases.

In contrast, the ARIMA model generated implausible forecasts, including negative confidence intervals, indicating weaker suitability for this application.

The superior performance of VAR demonstrates the importance of modelling the multivariate relationships between environmental conditions and disease transmission.

## Final Conclusion

This study demonstrates that climate variables can be used effectively to forecast dengue outbreaks in Singapore.

Among the models evaluated:

* VAR consistently achieved the lowest AIC and BIC values.
* VAR generated realistic and interpretable forecasts.
* ARIMA struggled to capture the complexity of climate-driven dengue transmission.

The findings support the hypothesis that environmental factors significantly influence dengue prevalence and highlight the potential of multivariate time-series forecasting for public health applications.

While the model performed well on historical data, future performance may be influenced by evolving climate conditions, changes in mosquito populations, and other epidemiological factors. Continuous retraining with updated data would be necessary to maintain forecasting accuracy.

Overall, the Vector Auto Regression (VAR) model emerged as the most effective approach for predicting dengue outbreaks using climate variables.
