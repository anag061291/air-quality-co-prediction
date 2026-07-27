# Air Quality Prediction Using Environmental Sensor Data

## Project Overview

This project develops and evaluates predictive models for estimating carbon monoxide concentrations, CO(GT), using environmental sensor readings, weather conditions, and temporal patterns.

The analysis follows the CRISP-DM framework, covering business understanding, data exploration, preparation, modeling, evaluation, and practical reflection. The objective is to assess whether indirect and lower-cost sensor information can support air-quality monitoring.

## Business Problem

Certified pollution-monitoring equipment can be expensive to deploy and maintain at scale. This project investigates whether carbon monoxide levels can be estimated using accessible sensor measurements, environmental conditions, and time-based variables.

The main analytical question is:

> How accurately can sensor data, environmental variables, and temporal patterns predict carbon monoxide concentrations?

## Dataset

The project uses the Air Quality dataset, which contains hourly environmental and sensor observations.

- **Original observations:** 9,357
- **Variables:** 15
- **Target variable:** `CO(GT)`
- **Complete cases used for modeling:** 827

The original dataset represents missing or faulty sensor readings using `-200`. These values were converted to missing values and incomplete records were removed before modeling.

## Project Workflow

### 1. Data Understanding

- Examined dataset dimensions and variable types
- Reviewed environmental and sensor variables
- Identified nonstandard missing-value codes
- Explored correlations and temporal patterns

### 2. Data Preparation

- Replaced `-200` values with missing values
- Removed incomplete observations
- Combined date and time information
- Created hour and weekday variables
- Selected relevant sensor and environmental predictors
- Prepared the data for regression analysis

### 3. Exploratory Data Analysis

The analysis examined:

- CO concentration distributions
- Relationships between sensor readings and CO levels
- Temperature and humidity patterns
- Hourly pollution patterns
- Weekday and weekend differences
- Correlations and multicollinearity among predictors

## Models Developed

### Baseline Model

The baseline multiple linear regression model used:

- `PT08.S1(CO)`
- Temperature
- Relative humidity
- Absolute humidity

The model achieved:

- **R²:** 0.886

Although the model showed strong explanatory power, multicollinearity affected the stability and interpretation of some coefficients.

### Refined Model

Absolute humidity was removed to reduce multicollinearity. The refined model used:

- `PT08.S1(CO)`
- Temperature
- Relative humidity

The model maintained:

- **R²:** 0.886

Removing absolute humidity reduced the VIF values and improved coefficient stability without reducing explanatory performance.

### Extended Model with Hour

The hour of the day was added to capture daily pollution patterns.

- **R²:** 0.888

The improvement was small, but it demonstrated that time of day provides additional information about changes in CO levels.

### Extended Model with Weekday Effects

Weekday dummy variables were added to examine weekly patterns.

- **R²:** 0.891

This specification produced the highest in-sample fit, although the improvement over the refined model was limited.

## Out-of-Sample Evaluation

A time-based train-test split was used:

- First 80% of observations for training
- Final 20% for testing

The model achieved:

- **MAE:** 0.3874
- **RMSE:** 0.4745
- **MAPE:** 20.75%

The predictions followed the general movement of actual CO levels, although the model underestimated some extreme pollution peaks.

K-fold cross-validation was also used to assess stability across different data subsets.

## Key Findings

- `PT08.S1(CO)` was the strongest predictor of carbon monoxide concentration.
- The sensor had an approximate correlation of 0.94 with `CO(GT)`.
- Temperature and relative humidity provided statistically meaningful information.
- Removing absolute humidity reduced multicollinearity without lowering model performance.
- CO levels displayed identifiable hourly and weekday patterns.
- Pollution levels tended to be lower on weekends.
- Temporal features improved model fit, but the practical gain was relatively small.
- The refined model offered the best balance of performance, simplicity, stability, and interpretability.
- The model performed well overall but was less accurate for extreme pollution events.

## Final Model Selection

The model with hour and weekday effects achieved the highest R² of 0.891. However, the refined model without absolute humidity was selected as the preferred practical model because it maintained strong performance while offering greater simplicity, statistical stability, and interpretability.

## Tools and Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Statsmodels
- Jupyter Notebook

## Analytical Skills Demonstrated

- CRISP-DM methodology
- Data cleaning and preprocessing
- Exploratory data analysis
- Feature engineering
- Multiple linear regression
- Multicollinearity analysis using VIF
- Regression diagnostics
- Time-based train-test splitting
- Out-of-sample forecasting
- K-fold cross-validation
- Model evaluation and selection
- Environmental data interpretation

## Repository Contents

- `Final Assigment Predictive.ipynb`: Jupyter Notebook containing the complete data preparation, analysis, modeling, diagnostics, and evaluation process
- `AirQualityUCI.xlsx`: Original Air Quality dataset used for the project
- `cleaned_air_quality.csv`: Cleaned dataset prepared for modeling
- `Assigment Predictive Final Group 8.pdf`: Complete written project report
- `Final Presentation Predictive Final Group 8.pdf`: Presentation summarizing the methodology, models, results, and conclusions

## Project Limitations

- Data cleaning reduced the sample from 9,357 observations to 827 complete cases.
- The analysis is based on data collected in a specific urban environment.
- Linear regression may not fully capture nonlinear pollution patterns.
- The model underestimates some extreme CO concentration peaks.
- Additional traffic, weather, and location variables could improve prediction.

## Authors

- Ana María Gonzalez Villa
- Juan David Hernández Florez
- Liceth Katerine Forero Tusarma
- Wagner Alexander Moreno Alvarado

Master of Data Analytics  
University of Niagara Falls
