# Asset Performance and Risk Analysis

## This Python Notebook contains code the performs a quantitative analysis of the a variety of portfolios for comparison
The majority of the data used in analysis is contained in the "Resources" folder. This data is contained in various .csv files. Additionally a Custom Portfolio is analyzed. This data is gathered through Yahoo Finance and was pulled from the internet using
`price_data = web.get_data_yahoo(ticker, start='2015-03-03', end='2019-04-23')`

## Code and Dependencies
This code is to be run on 
`Python 3.7.13`

The following Python Libraries were also imported and used

`import pandas as pd`

`import numpy as np`

`import datetime as dt`

`import seaborn as sns`

`from pathlib import Path`

`import pandas_datareader as web`

`%matplotlib inline`

## Metrics Analyzed
So far in the course, we have learned a variety of tools for assessing the performance of financial assets. Including Daily Returns, Daily Volatility, Anualized Volatility, Correlation, Beta, and Sharpe Ratio.

### Daily Returns
Daily Returns is determined by calculating the percent change of the closing price of an asset from day to day.

`# Calculate Daily Returns`

`sp500_df['Daily Returns'] = sp500_df['Close'].pct_change()
sp500_df`

### Daily Volatility
Daily Volitility is determined by calculating the standard deviation on the dataframe. This is an indication of the size of fluctuation of an asset price on a daily basis.

`# Calculate the daily standard deviations of all portfolios`

`daily_std = combined_returns.std()`

### Annualized Volatility
Similar to daily volatility, but also accounts for 252 days of trading in a year.

`# Calculate the annualized standard deviation (252 trading days)`

`annualized_std = daily_std * np.sqrt(252)`

### Correlation
Correlation shows how closely different assets move together. A correlation of 1 indicates that the assets move together, a correlation of 0 means there is no identifiable relationship, and a correlation of -1 means the assets move in opposing directions.

`# Calculate the correlation`

`returns_correlation = combined_returns.corr()`

### Beta
Beta is determined by dividing the covariance of an asset (to the market) by the variance of the market. It indicate the risk of an asset relative to the overall market

`# Calculate covariance of a single portfolio`

`algo1_covariance = combined_returns['Algo 1'].cov(combined_returns['S&P 500'])`

`# Calculate variance of S&P 500`

`sp_variance = combined_returns['S&P 500'].var()`

`# Computing Beta`

`algo1_beta = algo1_covariance / sp_variance`

### Sharpe Ratio
Sharpe Ratio is a way of determining the relative reward of an asset after risk has been accounted for.

`# Calculate the Sharpe Ratios`

`sharpe_ratios = ((updated_returns_df.mean() - updated_returns_df['rf_rate'].mean()) * 252) / (updated_returns_df.std() * np.sqrt(252))`