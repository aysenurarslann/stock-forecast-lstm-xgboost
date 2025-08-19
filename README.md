#  Apple (AAPL) Stock Price Forecasting Project

This project uses **LSTM (Deep Learning)** and **XGBoost (Machine Learning)** models to predict the closing prices of **Apple Inc. (AAPL)**. Our goal is to forecast future prices based on historical data and compare the performance of both models.

---

## Objective
- Predict the next day’s closing price using the past 60 days of historical prices.
- Compare the performance of LSTM and XGBoost models.
- Determine the most suitable model for time series forecasting.

---

##  Data Source
- **Symbol**: `AAPL` (Apple Inc.)
- **Source**: Yahoo Finance (`yfinance`)
- **Time Period**: January 1, 2019 – January 1, 2024
- **Frequency**: Daily
- **Column Used**: `Close` (Closing Price)
- **Total Data Points**: ~1,257 days
- **Normalization**: `MinMaxScaler` (scaled to 0–1 range)

---

##  Models Used

### 1. **LSTM (Long Short-Term Memory)**
- **Type**: Deep Learning, RNN-based
- **Layers**:
  - LSTM (50 units, `return_sequences=True`)
  - LSTM (50 units, `return_sequences=False`)
  - Dense (25 units, ReLU activation)
  - Dense (1 output, price prediction)
- **Optimizer**: Adam (learning_rate=0.001)
- **Loss Function**: Mean Squared Error (MSE)
- **Epochs**: 20
- **Batch Size**: 32
- **Input Shape**: `(batch_size, 60, 1)` → 60 days of history, 1 feature

### 2. **XGBoost (Extreme Gradient Boosting)**
- **Type**: Tree-based Machine Learning
- **Parameters**:
  - `n_estimators=100`
  - `max_depth=6`
  - `learning_rate=0.1`
  - `random_state=42`
- **Input Shape**: 2D array → `(batch_size, 60)`

---

##  Technical Details
| Feature | Value |
|--------|-------|
| **Sequence Length** | 60 days |
| **Train/Test Split** | 80% / 20% |
| **Test Samples** | 240 days |
| **Normalization** | MinMaxScaler (0–1) |
| **Evaluation Metrics** | MAE, RMSE |
| **Libraries** | `yfinance`, `pandas`, `numpy`, `matplotlib`, `scikit-learn`, `tensorflow`, `xgboost` |

---

## Data Analysis and Visualization

### 1. Historical Price Chart (2019–2024)
![Apple Stock Price (2019-2024)](apple_stock_price_2019_2024.png)

> 📌 **Description**: Apple stock price started around **$34** in 2019 and rose to **$196** by 2024. Product launches, market growth, and macroeconomic factors significantly influenced the price during this period.

---

##  Model Comparison Results

### 2. LSTM vs XGBoost Prediction Comparison
![LSTM vs XGBoost Comparison](lstm_vs_xgboost_comparison.png)

> 📌 **Graph Description**:
> - **Black line**: Actual closing price
> - **Red dashed line**: LSTM prediction
> - **Blue dotted line**: XGBoost prediction
>
> LSTM better captures the overall trend, while XGBoost is less responsive to sudden price movements.

---

## Performance Metrics

| Model      | MAE (Mean Absolute Error) | RMSE (Root Mean Squared Error) |
|-----------|----------------------------|-------------------------------|
| **LSTM**  | 4.65 USD                   | 5.56 USD                      |
| **XGBoost** | 9.49 USD                 | 12.69 USD                     |

###  Interpretation:
- **LSTM** outperforms XGBoost by **nearly a factor of two** in both MAE and RMSE.
- LSTM successfully learns **long-term dependencies** (trends, momentum) in time series data.
- XGBoost, trained on raw windowed data, fails to fully capture the sequential nature of the time series.

---

##  Conclusion: Which Model is Better?

 **LSTM** is the **superior model** for this forecasting task.

>  **Why?**
> - Time series forecasting requires understanding of sequential patterns and temporal dependencies.
> - LSTM can model these dependencies through its internal memory cells.
> - XGBoost treats each input window as an independent vector and cannot inherently learn time-based relationships.

---

##  Training Process (LSTM)
### Loss Over Epochs
Epoch 1/20 - loss: 0.2023 - val_loss: 0.0513
Epoch 20/20 - loss: 0.0008 - val_loss: 0.0012



- Training loss decreases steadily.
- Validation loss drops to 0.0012 → indicates **good generalization** with **no overfitting**.

---

##  Not Financial Advice

>  This project is **purely educational**.  
> Stock prices are influenced by company news, economic data, market sentiment, and global events. This model only analyzes historical price movements.  
> 
> 📌 **Do not use this model for real-world investment decisions.**
