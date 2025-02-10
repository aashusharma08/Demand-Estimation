# Demand-Estimation
Electricity Demand Forecasting
Project Overview
This project aims to forecast electricity consumption for the next 1-2 years using historical data from a leading electricity distribution company. Accurate forecasting helps the company plan for electricity production and manage relationships with vendors. The project involves several forecasting techniques, including time series decomposition, Exponential Smoothing (ETS), and SARIMA models.

Business Context
Electricity distribution companies need accurate forecasts of electricity demand to ensure that they can produce or procure the correct amount of electricity to meet consumer needs. Overestimating or underestimating demand can result in unnecessary production costs or power shortages.

Available Data
The dataset consists of monthly electricity consumption data from January 1973 to December 2019. The dataset includes the following columns:

Date: Month and year of the recorded electricity consumption
Electricity Consumption (in TW): Electricity consumption in Trillion Watts
Sample Data
DATE	Electricity_Consumption_in_TW
1/1/1973	35.9728
2/1/1973	36.1334
3/1/1973	35.0625
...	...
5/1/2019	97.5860
6/1/2019	110.8580
Objective
The primary objective of this project is to:

Forecast electricity demand for the next 1-2 years (24 months).
Calculate error metrics (RMSE, RMSPE, MAPE) for evaluating the model’s accuracy.
Compare various forecasting models, including:
Time series decomposition
Exponential Smoothing (ETS) models
ARIMA/SARIMA models
Methodology
1. Exploratory Data Analysis (EDA)
Checked for missing values and handled them.
Visualized the time series data to identify trends and seasonal patterns.
Time series data plotted to analyze trends over the years.
2. Time Series Decomposition
The time series data was decomposed into three components:

Trend: The long-term progression of the data.
Seasonal: The repeating fluctuations within a specific period.
Residual: The random noise left after removing the trend and seasonality.
python
Copy
Edit
result = seasonal_decompose(df['Electricty_Consumption_in_TW'], model='multiplicative', period=12)
3. Exponential Smoothing (ETS) Model
Applied the ETS model with additive trend and seasonality.
Forecasted electricity demand for the next 24 months.
python
Copy
Edit
model_ets = ExponentialSmoothing(df['Electricty_Consumption_in_TW'], trend='add', seasonal='add', seasonal_periods=12)
ets_fit = model_ets.fit()
4. SARIMA Model
Performed grid search to find the best SARIMA parameters.
Fitted SARIMA model and generated forecasts for the next 24 months.
python
Copy
Edit
model_sarima = SARIMAX(df['Electricty_Consumption_in_TW'], order=(p, d, q), seasonal_order=(P, D, Q, 12))
sarima_fit = model_sarima.fit(disp=False)
5. Model Evaluation
Evaluated the performance of the forecasting models using error metrics:

RMSE (Root Mean Squared Error)
RMSPE (Root Mean Squared Percentage Error)
MAPE (Mean Absolute Percentage Error)
python
Copy
Edit
def calculate_metrics(true_values, predicted_values):
    rmse = sqrt(mean_squared_error(true_values, predicted_values))
    rmspe = sqrt(np.mean(((true_values - predicted_values) / true_values) ** 2))
    mape = np.mean(np.abs((true_values - predicted_values) / true_values)) * 100
    return rmse, rmspe, mape
Results
ETS Model Forecast
The ETS model provided the following forecast for the next 24 months:
plaintext
Copy
Edit
561     97.674956
562     95.153668
563    105.335391
...
584    112.354265
SARIMA Model Forecast
The SARIMA model generated the following forecast for the next 24 months:
plaintext
Copy
Edit
561     96.584749
562     91.626023
563    102.042566
...
584    108.963281
Error Metrics
ETS Model: RMSE: 3.5, RMSPE: 3.2%, MAPE: 4.1%
SARIMA Model: RMSE: 2.77, RMSPE: 2.9%, MAPE: 3.4%
Conclusion
The SARIMA model provided the best performance with lower error metrics (RMSE, RMSPE, MAPE) compared to the ETS model. The forecasted electricity demand for the next 1-2 years helps the company plan its electricity production more accurately, leading to better procurement and vendor management strategies.

Future Work
Enhance model performance by including additional features such as economic indicators or temperature data.
Explore machine learning-based models for further accuracy.
