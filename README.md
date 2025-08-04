# Dutch TTF Natural Gas Price Forecasting

## Overview
This project focuses on forecasting front-month Dutch TTF (Title Transfer Facility) natural gas futures prices, a key benchmark for European natural gas markets. The goal is to model short-term price dynamics using time-series analysis, with applications in algorithmic trading, hedging, and risk management for energy trading firms. The project uses historical futures data (TFAc1 ticker from Investing.com) and employs statistical models like SARIMA to capture price trends and seasonality.

This repository demonstrates exploratory data analysis (EDA), time-series modeling, and model selection for forecasting TTF prices. It is a work-in-progress, with planned enhancements including trading strategy development, volatility modeling, and deployment of a simple interface.

## Project Motivation
Dutch TTF is the leading European gas price hub, widely used for trading and hedging natural gas contracts. Accurate short-term price forecasts are critical for energy trading firms to optimize trading strategies, manage risk, and inform decision-making. This project aims to:
- Analyze historical TTF front-month futures prices.
- Identify seasonal and non-seasonal patterns using statistical tools.
- Build and evaluate SARIMA models for short-term price forecasting.
- Lay the groundwork for trading signal generation and volatility modeling.

## Methodology
The project follows a structured approach to time-series forecasting:

1. **Data**:
   - **Source**: Continuous front-month TTF futures prices (TFAc1) from Investing.com, representing a rolling time series of the nearest expiring contract.
   - **Rationale**: Front-month contracts offer high liquidity, fewer gaps, and a clean proxy for market expectations.
   - **Limitation**: The dataset does not support long-term forward curve modeling (e.g., Q1 2026 prices).

2. **Exploratory Data Analysis (EDA)**:
   - Conducted full EDA, including trend and seasonality decomposition.
   - Applied Augmented Dickey-Fuller (ADF) test to confirm non-stationarity, followed by regular (d=1) and seasonal (D=1, S=365) differencing to achieve stationarity.

3. **Time-Series Analysis**:
   - Generated Autocorrelation Function (ACF) and Partial Autocorrelation Function (PACF) plots to identify significant lags.
   - Observed a strong seasonal MA(1) signature at lag 365 (ACF: -0.4982), confirming a seasonal period of 365 days.
   - Identified significant non-seasonal lags (e.g., 1, 2, 4, 5) for AR and MA terms.

4. **Model Selection**:
   - Proposed two SARIMA models based on ACF/PACF analysis:
     - SARIMA(2,1,2)(0,1,1,365): Captures significant lags at 1 and 2.
     - SARIMA(5,1,5)(0,1,1,365): Captures effects up to lag 5.
   - Planned to compare models using Akaike Information Criterion (AIC) and Bayesian Information Criterion (BIC) for optimal fit.
   - Previously trained an ARIMA(4,1,4) model and analyzed residuals using the Ljung-Box test.

5. **Current Status**:
   - SARIMA model fitting is pending due to computational constraints on local hardware (8 GB RAM, Intel i5). Planned to run on a cloud platform (e.g., Google Colab Pro, AWS).
   - ACF/PACF plots and significant lags are saved for reference.

## Results
- **EDA**: Confirmed non-stationarity of TTF prices, addressed via regular and seasonal differencing.
- **ACF/PACF Analysis**: Identified significant lags (e.g., 1, 2, 4, 5 for non-seasonal; 365 for seasonal) to guide SARIMA parameter selection.
- **ARIMA(4,1,4)**: Successfully trained and validated with residual diagnostics, serving as a baseline for SARIMA.
- **Visualizations**: ACF/PACF plots for seasonally differenced series are available in `plots/acf_pacf_seasonally_differenced.jpg`.
- **Outputs**: Significant ACF/PACF lags are saved in `outputs/significant_lags_acf_pacf_seasonally_differenced_series.txt`.

*Note*: SARIMA model results (AIC/BIC, forecasts) are pending cloud-based computation.

## Installation
To run the notebook locally, follow these steps:

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/<your-username>/dutch-ttf-price-forecasting.git
   cd dutch-ttf-price-forecasting
   ```

2. **Set Up Python Environment**:
   - Requires Python 3.9 or later.
   - Install dependencies from `requirements.txt`:
     ```bash
     pip install -r requirements.txt
     ```

3. **Obtain Data**:
   - The dataset (TFAc1 front-month futures prices) is sourced from Investing.com. Due to licensing restrictions, it is not included in this repository.
   - Users must download the data manually or use an API (if available) to fetch TTF futures prices.
   - Expected format: CSV with columns `Date` (YYYY-MM-DD) and `Price` (EUR/MWh).

4. **Run the Notebook**:
   - Place the data file in the `data/` folder.
   - Open the notebook in Jupyter:
     ```bash
     jupyter notebook notebooks/dutch_ttf_price_forecasting.ipynb
     ```
   - Update the notebook to point to your data file path.

## Dependencies
Listed in `requirements.txt`:
```
pandas
numpy
matplotlib
statsmodels
```

## Next Steps
The project is ongoing, with the following planned enhancements:
- **Run SARIMA Models**: Use a cloud platform (e.g., Google Colab Pro, AWS) to fit SARIMA(2,1,2)(0,1,1,365) and SARIMA(5,1,5)(0,1,1,365), comparing them via AIC/BIC.
- **Residual Diagnostics**: Analyze residuals of the best SARIMA model (ACF/PACF, normality, heteroskedasticity).
- **Trading Strategy**: Develop and backtest a rule-based trading strategy using SARIMA forecasts (e.g., buy/sell signals based on predicted price changes).
- **Volatility Modeling**: Implement a GARCH model to capture volatility clustering, common in energy markets.
- **Machine Learning**: Explore LSTM models for non-linear price patterns.
- **Deployment**: Build a Streamlit app to visualize forecasts and trading signals interactively.
- **Backtesting**: Evaluate prediction accuracy using a rolling or expanding window approach.

## Relevance to Energy Trading
This project demonstrates skills critical for algorithmic trading in energy markets:
- **Domain Knowledge**: Understanding of TTF futures, liquidity, and rolling contracts.
- **Quantitative Modeling**: Proficiency in time-series analysis (SARIMA, ARIMA) and statistical diagnostics.
- **Technical Skills**: Python programming with `pandas`, `numpy`, `matplotlib`, and `statsmodels`.
- **Problem-Solving**: Addressing computational limitations and proposing scalable solutions (cloud computing).
- **Practical Application**: Foundation for trading strategy development and risk management.

## Limitations
- **Incomplete SARIMA Results**: Model fitting is pending due to computational constraints.
- **Data Access**: The dataset is not included, requiring users to source TTF futures data independently.
- **Trading Strategy**: Currently, the project focuses on forecasting without explicit trading signals or backtesting.
- **Long-Term Forecasting**: Limited to front-month contracts, excluding forward curve analysis.




