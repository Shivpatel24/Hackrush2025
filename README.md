# Hackrush2025

SynOCE :Climate Science Problem Statement 

Shiv Nitinkumar Patel 
23110302 


### Hourly Rainfall Prediction Using Gradient Boosting Regressor

This project implements a machine learning pipeline to predict hourly rainfall values from daily rainfall data using a Gradient Boosting Regressor (GBR). The approach leverages historical hourly rainfall patterns to redistribute daily totals into hourly estimates, which are then refined using supervised learning.

#### Data Processing
The model uses two input datasets:
- A daily rainfall dataset (`.nc` format), spatially averaged across latitude and longitude to create a single daily time series.
- An hourly rainfall ground truth dataset (`.nc` format), processed similarly to ensure alignment with the daily dataset.

To transform daily data into hourly format, the code computes the average distribution of rainfall across each hour of the day using historical data from 2022. These percentages are then used to redistribute daily rainfall totals into hourly values for both 2022 (training) and 2023 (testing).

#### Feature Engineering
Each hourly data point is enriched with the following features:
- `redistributed_tp`: The initial hourly estimate derived from daily totals
- `hour`: Hour of the day (0 to 23)
- `day`: Day of the month
- `month`: Month of the year

These features help the model capture temporal and seasonal patterns in rainfall distribution, allowing it to improve upon the initial estimates.
#### Additive Decomposition 
**Additive decomposition** helps by breaking down a time series into three distinct components: **trend**, **seasonality**, and **residuals**. This separation allows us to better understand the underlying patterns in the data:

- The **trend** shows long-term progression or direction.
- The **seasonal** component reveals repeating patterns (e.g., daily or monthly cycles).
- The **residuals** capture random noise or unexplained variation.

By isolating these elements, additive decomposition makes it easier to analyze, interpret, and model time series data more effectively.
#### Model Training
The model used is a `GradientBoostingRegressor` from scikit-learn, trained on the 2022 dataset. Key hyperparameters include:
- `n_estimators=300`
- `learning_rate=0.03`
- `max_depth=6`
- `random_state=42`

The model is trained to predict actual hourly rainfall values based on the redistributed estimates and temporal features.

#### Evaluation
Model performance is evaluated on the 2023 dataset using the following metrics:
- Root Mean Square Error (RMSE)
- Mean Absolute Error (MAE)
- Nash-Sutcliffe Efficiency (NSE)

These metrics provide a comprehensive view of the model’s predictive accuracy and its ability to replicate the observed variability in rainfall.
