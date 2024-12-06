# Stock Market Price Prediction using LSTM

**Author:** Kerem Haktan Kurt  
**Date:** October 2024

## Introduction
This project leverages Long Short-Term Memory (LSTM) neural networks to predict future stock prices using historical market data. It utilizes 10 years of past data downloaded from Yahoo Finance, applying feature engineering, model training, and evaluation to produce accurate predictions on unseen data.

## Data Description
- **Initial Data:** ~2516 rows × 6 columns (OHLCV data).
- **Added Features:**  
  - Moving Average (10-day, 50-day)  
  - RSI (14-day)  
  - MACD & Signal Line  
  - Volatility (10-day, 50-day)
  
After removing missing values and trimming the initial rows, the final dataset is 2466 rows × 14 columns. The data is split into 80% training (2014–2022) and 20% testing (post-2022), maintaining temporal order to respect time-dependency.

## Data Preprocessing
1. Download historical stock data.
2. Create technical indicators as features.
3. Handle missing values and trim data.
4. Split into train/test sets without shuffling.
5. Scale features to ensure equal importance during training.

## The Model
- **Model Used:** LSTM (2 layers, 50 neurons each)
- **Input Features:** Close, MA-10, MA-50, RSI-14, MACD, Signal-Line, Volatility-10, Volatility-50
- **Output:** Future Close Price

LSTMs handle temporal dependencies better than models like Linear Regression or Random Forest, making them well-suited for sequential financial data.

## Training
- **Hyperparameters:**  
  - Sequence length: 50  
  - Learning rate: 5e-5 with cosine scheduler  
  - Epochs: 100 with early stopping
- **Process:**  
  - Backpropagation through time for each batch  
  - Compute MSE, RMSE, MAE after each epoch  
  - Logged training process and metrics using Weights & Biases (WandB)

## Evaluation
Evaluated on the test set (2022-04 to 2024-01), the model achieved:  
- **MSE:** 22.5469  
- **RMSE:** 4.7484  
- **MAE:** 3.7476

## Results
The LSTM model successfully predicts future stock prices with relatively low error metrics, demonstrating its suitability for capturing time-dependent market dynamics.

## Conclusion
This project shows the viability of LSTM models for stock price forecasting. By carefully engineering features, tuning hyperparameters, and maintaining temporal integrity, the model delivered strong predictive performance on unseen data.

## References
- Hochreiter, S., & Schmidhuber, J. (1997). *Long short-term memory.* Neural Computation.
- McKinney, W. (2010). *Data structures for statistical computing in Python.* Proceedings of the 9th Python in Science Conference.
- Paszke, A., et al. (2019). *PyTorch: An Imperative Style, High-Performance Deep Learning Library.* Advances in Neural Information Processing Systems.
- Additional EDA guides, articles, and research on LSTM vs Transformers for stock price prediction.
