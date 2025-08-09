## 📄 Executive Summary
This interim report covers **data preprocessing** and **exploratory data analysis (EDA)** for a time series forecasting project aimed at **portfolio optimization**.  
We analyzed **Tesla (TSLA)**, **Vanguard Total Bond Market ETF (BND)**, and **S&P 500 ETF (SPY)** between **July 1, 2015** and **July 31, 2025**.

**Key Achievements:**
- Data extraction via `yfinance`
- Data cleaning & type validation
- Feature engineering (returns, volatility)
- Trend and volatility analysis
- Stationarity testing (ADF test)
- Risk metric calculation (VaR, Sharpe Ratio)

---

## 📊 Data Extraction

| Ticker | Asset Class | Role in Portfolio |
|--------|------------|-------------------|
| TSLA   | High-growth stock (Automobile Manufacturing) | Growth & high return |
| BND    | Bond ETF (U.S. investment-grade bonds) | Stability & low risk |
| SPY    | Equity ETF (S&P 500 Index) | Diversified exposure |

**Data Details:**
- **Source:** Yahoo Finance (`yfinance`)
- **Date Range:** 2015-07-01 → 2025-07-31
- **Frequency:** Daily
- **Features:** Open, High, Low, Close, Adj Close, Volume

```python
import yfinance as yf
tickers = ['TSLA', 'BND', 'SPY']
data = yf.download(tickers, start='2015-07-01', end='2025-07-31', group_by='ticker')
## 🧹 Data Cleaning & Validation
- **Missing Values:** `0` → no imputation needed  
- **Data Types:** Correct (`DatetimeIndex`, `float64`, `int64`)  
- **Index Sorting:** Already chronological  

---

## 📈 Exploratory Data Analysis (EDA)

### Adjusted Closing Price Trends
- **TSLA:** Strong growth (~$25 → ~$300), high volatility  
- **BND:** Flat to slightly declining during rate hikes  
- **SPY:** Steady growth with periodic corrections  

### Daily Returns Analysis
- **Volatility Clustering:** Most prominent in TSLA during crises  
- **BND:** Lowest volatility  
- **SPY:** Moderate volatility, spikes during macro events  

### Rolling Volatility (30-Day)
- Peaks observed in:
  - **March 2020:** Pandemic crash  
  - **2022:** Inflation & rate hikes  
  - **2024:** Election & geopolitical risks  

---

## 📉 Stationarity Testing
- **ADF Test:** Prices → *Non-stationary*  
- **Returns:** *Stationary* → suitable for ARIMA modeling  

---

## ⚠️ Risk Metrics

| Asset | 5% VaR   | Annual Return | Annual Volatility | Sharpe Ratio |
|-------|----------|---------------|-------------------|--------------|
| TSLA  | -0.055%  | 28.7%         | 42.1%             | 0.778        |
| BND   | -0.005%  | 10.2%         | 14.8%             | 0.357        |
| SPY   | -0.017%  | 2.8%          | 3.7%              | 0.794        |

---

## 🗝 Key Insights
- **Trend:** TSLA exceptional growth, BND stable, SPY steadily rising  
- **Volatility:** TSLA most volatile, especially during crises  
- **Stationarity:** Use returns for ARIMA modeling  
- **Risk:** TSLA has highest downside risk  
- **Reward:** TSLA highest risk-adjusted return  
