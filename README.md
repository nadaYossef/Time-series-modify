# Light Weight Vehicle Sales Analysis & Forecasting

## Overview
This project analyzes and forecasts U.S. Light Weight Vehicle Sales using time series technique. It leverages the `LTOTALNSA` dataset from FRED, covering sales data from January 1976 to May 202.

## Dataset

- **Source** [FRED - Total Vehicle Sales](https://fred.stlouisfed.org/series/LTOTALNS)
  
  ![image](https://github.com/user-attachments/assets/dc915b29-3b37-4d7c-bf49-db47b8257c6e)


- **Description** Monthly sales figures (in thousands) for light weight vehicles in the U..

- **Timeframe** January 1976 to May 201

## Installation

Ensure you have the necessary Python packages installed:

```bash
pip install numpy pandas matplotlib statsmodels
```

## Usage

1. **Load the Dataset**:

   ```python
   import pandas as pd

   df = pd.read_csv("LTOTALNSA.csv", index_col='DATE', parse_dates=True)
   ```

2. **Visualize the Data**:

   ```python
   import matplotlib.pyplot as plt

   plt.figure(figsize=(14, 4))
   plt.title('Light Weight Vehicle Sales')
   plt.plot(df)
   plt.show()
   ```

3. **Seasonal Decomposition**:

   ```python
   from statsmodels.tsa.seasonal import seasonal_decompose

   result = seasonal_decompose(df, model='additive', period=12)
   result.plot()
   plt.show()
   ```

4. **Forecasting with Holt-Winters**:

   ```python
   from statsmodels.tsa.holtwinters import ExponentialSmoothing

   model = ExponentialSmoothing(df['LTOTALNSA'], trend='add', seasonal='add', seasonal_periods=12)
   fit = model.fit()
   forecast = fit.forecast(steps=24)

   plt.figure(figsize=(14, 4))
   plt.plot(df, label='Historical')
   plt.plot(forecast, label='Forecast', color='red')
   plt.legend()
   plt.show()
   ```

## Insights & Results

- **Trend Analysis** The data exhibits a clear upward trend in vehicle sales over the decades, with notable fluctuations during economic downturn.

- **Seasonality** Sales show consistent seasonal patterns, with peaks typically occurring in spring and summer month.

- **Forecasting** The Holt-Winters model effectively captures both trend and seasonal components, providing reliable forecasts for the next two year.

## License
This project is licensed under the MIT Licens.
