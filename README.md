# Seasonality Analysis and Forecasting of SOFR-Fix
This project provides a comprehensive analysis of the Secured Overnight Financing Rate (SOFR), including an examination of its seasonal patterns and the development of forecasting models.

### What is SOFR?

The **Secured Overnight Financing Rate (SOFR)** is a benchmark interest rate that represents the cost of borrowing cash overnight, secured by U.S. Treasury securities. It is calculated as a volume-weighted median of transaction-level data from the Treasury repurchase (repo) market.

SOFR is a broad measure of the cost of borrowing cash overnight collateralized by Treasury securities. It is published by the Federal Reserve Bank of New York and is intended to be a replacement for the London Interbank Offered Rate (LIBOR).

### Key Terminologies

*   **SOFR Volume**: The total volume of transactions conducted at the SOFR rate, indicating liquidity in the overnight Treasury repo market.
*   **DTCC Tsy**: Refers to the clearing and settlement of U.S. Treasury securities transactions facilitated by the Depository Trust & Clearing Corporation (DTCC).
*   **RRP Amt (Reverse Repurchase Agreement Amount)**: The total value of reverse repurchase agreements conducted by the Federal Reserve. It's a tool for managing short-term interest rates and liquidity.
*   **TGA Balance (Treasury General Account Balance)**: The U.S. government's primary operating account at the Federal Reserve, which reflects the government's cash position.

### Seasonality Analysis

The SOFR Fix time series exhibits several notable seasonal patterns and event-driven movements:

*   **Yearly and Quarterly Patterns**: The rate shows distinct jumps at year-end (December) and quarter-ends (March, June, September). This is likely due to banks adjusting their balance sheets for regulatory reporting, which can cause temporary liquidity shortages and increase borrowing costs.
*   **Weekly Patterns**: Minor but regular fluctuations occur within each week. Slight rate increases are often seen at the beginning or end of the week, attributed to settlement conventions and liquidity management by banks.
*   **Event-Driven Volatility**:
    *   **U.S. Tax Day**: The SOFR can spike around April 15, likely due to large liquidity outflows for tax payments.
    *   **FOMC Meetings**: Federal Open Market Committee meetings can introduce slight volatility as the market anticipates potential policy changes.
    *   **Market Stress**: Sharp spikes, like the one in March 2020, often correspond to broader market stress and liquidity shortages.

<img width="1600" height="600" alt="event" src="https://github.com/user-attachments/assets/6f638909-da01-4f1a-9a32-37198720ce24" />

<img width="640" height="480" alt="Seasonality" src="https://github.com/user-attachments/assets/32e89ad1-95ed-48e4-a114-cedc4861fd27" />



### Forecasting SOFR

Two primary models were developed to forecast the SOFR Fix rate: an XGBoost model and a Neural Network model.

#### XGBoost Forecasting Model

This model uses several features to predict the SOFR. Feature importance analysis from the model highlights the following drivers:
*   **SOFR Volume**: 42.13%
*   **DTCC Tsy**: 30.68%
*   **Bloomberg GC**: 22.71%
*   **RRP Amt**: 6.13%

The model leverages these market indicators to capture the dynamics influencing the overnight rate.

#### Neural Network (LSTM) Forecasting Model

A Long Short-Term Memory (LSTM) based neural network was constructed to capture temporal dependencies in the SOFR time series while incorporating exogenous market features.

**Model Architecture**:
*   An **LSTM layer** processes the historical sequence of SOFR rates.
*   A **Dense layer** processes static exogenous features for the current day.
*   These two branches are merged using a **Concatenate** layer.
*   The final output is produced by subsequent Dense layers.

  <img width="1670" height="862" alt="image" src="https://github.com/user-attachments/assets/3d960057-7a96-422c-946b-ed3eba677478" />


**Performance Metrics**:
The model was trained and evaluated, yielding the following performance on the validation and test sets:

| Metric | Validation Set | Test Set |
| :--- | :--- | :--- |
| **Mean Absolute Error (MAE)** | 0.0530 | 0.0654 |
| **Root Mean Squared Error (RMSE)** | 0.0693 | 0.0845 |
| **Mean Absolute Percentage Error (MAPE)** | 1.02% | 1.42% |
| **R-squared (R²)** | 0.7854 | 0.9631 |

The high R² value on the test set indicates a strong predictive capability, demonstrating the model's effectiveness in forecasting the SOFR Fix.

Thank you!
