# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 11-05-26


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# ── 1. Load & Prepare Data ────────────────────────────────────────────────────
STOCK    = 'HDFCBANK.NS'
CSV_PATH = 'nifty50_2000_2025.csv'   # keep CSV in same folder as notebook

df = pd.read_csv(CSV_PATH)
df['Date'] = pd.to_datetime(df['Date'])

stock_df = df[df['Stock'] == STOCK].sort_values('Date').copy()
stock_df['YearMonth'] = stock_df['Date'].dt.to_period('M')

# Monthly average Close price
monthly = stock_df.groupby('YearMonth')['Close'].mean()
monthly.index = monthly.index.to_timestamp()

# ── FIRST FIVE ROWS ───────────────────────────────────────────────────────────
print("=" * 50)
print("FIRST FIVE ROWS:")
print("=" * 50)
print(monthly.head().to_frame())

# ── PLOTTING THE DATA ─────────────────────────────────────────────────────────
print("\nPLOTTING THE DATA:")
plt.figure(figsize=(14, 5))
plt.plot(monthly, color='steelblue', linewidth=1.5)
plt.title(f'{STOCK} — Monthly Avg Close Price (2000–2024)')
plt.xlabel('Date')
plt.ylabel('Close Price (₹)')
plt.grid(alpha=0.3)
plt.tight_layout()
plt.show()

# ── Decomposition (period=12 → 12 months = 1 year) ───────────────────────────
result = seasonal_decompose(monthly, model='additive', period=12)

# ── SEASONAL PLOT ─────────────────────────────────────────────────────────────
print("\nSEASONAL PLOT REPRESENTATION:")
plt.figure(figsize=(14, 4))
plt.plot(result.seasonal, color='darkorange', linewidth=1.2)
plt.title(f'{STOCK} — Seasonal Component')
plt.xlabel('Date')
plt.ylabel('Seasonality')
plt.grid(alpha=0.3)
plt.tight_layout()
plt.show()

# ── TREND PLOT ────────────────────────────────────────────────────────────────
print("\nTREND PLOT REPRESENTATION:")
plt.figure(figsize=(14, 4))
plt.plot(result.trend, color='tomato', linewidth=1.5)
plt.title(f'{STOCK} — Trend Component')
plt.xlabel('Date')
plt.ylabel('Trend (₹)')
plt.grid(alpha=0.3)
plt.tight_layout()
plt.show()

# ── RESIDUAL PLOT ─────────────────────────────────────────────────────────────
print("\nRESIDUAL REPRESENTATION:")
plt.figure(figsize=(14, 4))
plt.plot(result.resid, color='green', linewidth=1)
plt.title(f'{STOCK} — Residual Component')
plt.xlabel('Date')
plt.ylabel('Residual')
plt.grid(alpha=0.3)
plt.tight_layout()
plt.show()

```

















### OUTPUT:
FIRST FIVE ROWS:
```
==================================================
FIRST FIVE ROWS:
==================================================
                Close
YearMonth            
2000-02-01  11.551923
2000-03-01  13.150000
2000-04-01  11.367125
2000-05-01  12.426304
2000-06-01  12.466023
```



PLOTTING THE DATA:
<img width="1116" height="407" alt="image" src="https://github.com/user-attachments/assets/89e7cbb6-e2c1-4541-b46a-053387ec07bd" />


SEASONAL PLOT REPRESENTATION :
<img width="1117" height="332" alt="image" src="https://github.com/user-attachments/assets/ef2cd948-09dd-407d-9424-ba23500e3cc7" />




TREND PLOT REPRESENTATION :
<img width="1117" height="327" alt="image" src="https://github.com/user-attachments/assets/400dd39b-b71a-4e08-96d2-4162c76f3e01" />


OVERAL REPRESENTATION:
<img width="1116" height="326" alt="image" src="https://github.com/user-attachments/assets/59dc47de-a284-4b0d-afbe-c47feb5da7c9" />




### RESULT:
Thus we have created the python code for the time series analysis and decomposition.As the error is almost same over time, so it is eliminated.
