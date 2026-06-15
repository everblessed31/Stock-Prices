# 📈 Time Series Analysis of Stock Prices

## 📖 Project Overview

This project demonstrates the application of Time Series Analysis techniques to stock market data using Python. The analysis was carried out as part of an internship assignment aimed at understanding trends, seasonality, and smoothing techniques in time-dependent datasets.

The study focuses on analyzing stock closing prices over time and identifying underlying patterns through visualization, decomposition, and moving average smoothing.

## 🎯 Objectives

The objectives of this project were to:

* Analyze stock price data over time.
* Visualize stock price movements.
* Detect trends and seasonal patterns.
* Decompose the time series into trend, seasonality, and residual components.
* Apply moving average smoothing to reduce noise and reveal underlying patterns.

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Statsmodels
* Jupyter Notebook

## 📂 Dataset Description

The dataset contains historical stock market data with the following attributes:

| Column | Description         |
| ------ | ------------------- |
| symbol | Stock ticker symbol |
| date   | Trading date        |
| open   | Opening stock price |
| high   | Highest stock price |
| low    | Lowest stock price  |
| close  | Closing stock price |
| volume | Trading volume      |

For this analysis, the **Close Price** was selected as the primary variable because it represents the final trading value of the stock for each trading day.

## 🔍 Data Cleaning

### Missing Value Check

```python
df.isnull().sum()
```

Output:

```text
symbol     0
date       0
open      11
high       8
low        8
close      0
volume     0
```

### Missing Value Treatment

The missing values in the Open, High, and Low columns were handled using Forward Fill:

```python
df = df.ffill()
```

Verification:

```python
df.isnull().sum()
```

Result:

```text
symbol    0
date      0
open      0
high      0
low       0
close     0
volume    0
```

## 📊 Methodology

### Step 1: Import Libraries

```python
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
```

### Step 2: Load Dataset

```python
df = pd.read_csv("Stock Prices Data Set.csv")
```

### Step 3: Convert Date Column

```python
df['date'] = pd.to_datetime(df['date'])
```

### Step 4: Select Stock

```python
aapl = df[df['symbol'] == 'AAPL']
```

### Step 5: Set Date as Index

```python
aapl = aapl.set_index('date')
aapl = aapl.sort_index()
```

### Step 6: Plot Time Series

```python
plt.plot(aapl['close'])
```

### Step 7: Seasonal Decomposition

```python
decomposition = seasonal_decompose(
    aapl['close'],
    model='additive',
    period=252
)
```

### Step 8: Plot Decomposition

```python
decomposition.plot()
```

### Step 9: Moving Average Smoothing

```python
aapl['MA_30'] = aapl['close'].rolling(window=30).mean()
```

### Step 10: Plot Moving Average

```python
plt.plot(aapl['close'], label='Close Price')
plt.plot(aapl['MA_30'], label='30-Day Moving Average')
plt.legend()
```

## 📈 Results

### Time Series Plot

The stock closing price displayed fluctuations over time while exhibiting an overall long-term trend.

### Trend Component

The decomposition process identified the long-term direction of stock prices.

### Seasonal Component

Recurring patterns were observed and extracted through seasonal decomposition.

### Residual Component

Random variations that were not explained by trend or seasonality were isolated as residuals.

### Moving Average

The 30-day moving average successfully reduced short-term fluctuations and highlighted the broader market trend.

## 📚 Learning Outcomes

This project provided practical experience in:

* Time Series Analysis
* Data Cleaning
* Trend Detection
* Seasonal Decomposition
* Moving Average Smoothing
* Data Visualization
* Financial Data Analysis

## 👨‍💻 Author

Blessing Ogar

Aspiring Data Analyst | Data Engineer | Database Administrator

## ⭐ Internship Project

This project was completed as part of an internship program focused on developing practical machine learning and data analytics skills using Python.
