
# 📈 SARIMA Time Series Forecasting - AirPassengers Dataset

## Project Overview
This project demonstrates how to build a Seasonal AutoRegressive Integrated Moving Average (SARIMA) model using the famous **AirPassengers dataset**, which records monthly totals of international airline passengers from 1949 to 1960.
The project showcases end-to-end modeling:
- Stationarity check using the ADF test
- Differencing for trend and seasonality removal
- SARIMA model construction and tuning
- Forecasting and performance evaluation using RMSE and MAPE
- Visualization of predicted vs actual passenger counts

Use this link to access the notebook in Google Colab:  
[Open Colab Notebook](https://github.com/Aishwaryachen11/SARIMA-TimeSeries-AirPassengers-Forecasting/blob/main/SARIMA_AirPassengers_Project.ipynb)

## Why SARIMA?
Time series data often exhibit both trend and seasonality. SARIMA (Seasonal ARIMA) extends ARIMA by directly modeling this seasonality.

### SARIMA Notation
SARIMA(p, d, q)(P, D, Q)[m]
- **p, d, q**: Non-seasonal ARIMA parameters
  - p = autoregressive order
  - d = differencing order (for trend removal)
  - q = moving average order
- **P, D, Q**: Seasonal components
  - P = seasonal autoregressive order
  - D = seasonal differencing order (for seasonality)
  - Q = seasonal moving average order
- **m**: Seasonal period (m=12 for monthly data with yearly seasonality)

## Stationarity Check
To model a time series effectively, it must be stationary. 
We used the **Augmented Dickey-Fuller (ADF) Test**:
- **ADF Statistic:** 0.815
- **p-value:** 0.991  
  → Since p-value > 0.05, the data is **non-stationary**

## Differencing to Induce Stationarity
To make the series stationary, we performed:
- **First-order differencing**: `ts.diff()`
- **Seasonal differencing** (period=12): `ts.diff(12)`
- **Both together**: `ts.diff().diff(12)`
This transformation stabilized the mean and seasonal patterns. A line plot confirmed the stationarity post-differencing.

## Model Building: SARIMA
We used the following tuned parameters:
python
SARIMAX(ts,
        order=(1,1,1),        # ARIMA(p,d,q)
        seasonal_order=(1,1,1,12)  # Seasonal (P,D,Q,s)
)
Fitted on the full dataset (after stationarity induced).

## Forecast vs Actual Plot
A plot comparing the predicted values to actual monthly passengers shows the model effectively captures the trend and seasonal patterns.

<img src="https://github.com/Aishwaryachen11/SARIMA-TimeSeries-AirPassengers-Forecasting/blob/main/SARIMA_Forecast%20vs%20actual.png" alt="Model Architecture" width="550"/>

## Evaluation Metrics

- **RMSE:** `15.56`  
  → Indicates average absolute deviation of 15.56 passengers

- **MAPE:** `4.57%`  
  → Only ~4.6% average prediction error — excellent for time series

## Forecast Use Cases
SARIMA is well-suited for:
- Forecasting sales, demand, or resource planning
- Modeling weather, energy, or transport data
- Any time series with clear seasonal patterns

## Future Enhancements
- Train/test split for validation on future unseen data
- Grid search for automated hyperparameter tuning
- Comparison with models like Prophet, LSTM
- Incorporating external regressors (SARIMAX)

## ✅ Conclusion
This project demonstrates how SARIMA models can forecast seasonal time series data with high accuracy using classical statistical methods.

