# 🚕 Maximizing Taxi Driver Revenue

Analyzing NYC Yellow Taxi trip data to uncover how payment methods influence fare amounts — using hypothesis testing and linear regression to derive actionable revenue strategies.

---

## 📌 Problem Statement

In the competitive taxi industry, understanding the relationship between **payment type and fare amount** is key to optimizing driver earnings. This project investigates:

- Do credit card users pay significantly higher fares than cash users?
- Can data-driven insights guide payment policy recommendations for drivers?

---

## 🎯 Objective

- Conduct a **hypothesis test** to determine if payment method significantly impacts fare amount
- Build a **linear regression model** to predict fare amount from trip duration
- Derive **actionable recommendations** for revenue maximization

---

## 📂 Dataset

**NYC Yellow Taxi Trip Data — January 2020**  
Source: [Kaggle](https://www.kaggle.com/datasets/microize/newyork-yellow-taxi-trip-data-2020-2019)

Key columns used:

| Column | Description |
|---|---|
| `tpep_pickup_datetime` | Trip start timestamp |
| `tpep_dropoff_datetime` | Trip end timestamp |
| `fare_amount` | Fare charged (USD) |
| `trip_distance` | Distance travelled (miles) |
| `payment_type` | 1 = Card, 2 = Cash |
| `passenger_count` | Number of passengers |

---

## 🔧 Pipeline

### 1. Preprocessing
- Parsed datetime columns → derived `duration` (minutes)
- Subset to relevant columns; dropped nulls (<2% missing) and duplicates
- Filtered: `payment_type` ∈ {Card, Cash}, `passenger_count` ∈ [1, 5]
- Removed zero/negative values for fare, distance, duration
- **IQR-based outlier removal** on `fare_amount`, `trip_distance`, `duration`

### 2. Exploratory Data Analysis
- Distribution of fare amount and trip distance by payment type
- Payment type preference (pie chart)
- Impact of passenger count on payment type (stacked bar chart)
- Group-level descriptive stats (mean, std) by payment type

### 3. Hypothesis Testing

| | |
|---|---|
| **H₀** | No difference in mean fare between Card and Cash users |
| **H₁** | Significant difference exists |
| **Test Used** | Welch's t-test (fare not normally distributed — confirmed via QQ plot) |
| **Result** | t-stat ≈ 169.21, p ≈ 0.0 → **Reject H₀** |

✅ Card payments are associated with significantly higher fares than cash.

### 4. Linear Regression

- **X:** Trip duration (minutes)  
- **Y:** Fare amount (USD)  
- 80/20 train-test split

| Metric | Train | Test |
|---|---|---|
| MSE | High | High |
| R² | ~2% | ~1.7% |

⚠️ Trip duration alone is a weak predictor — multi-feature modeling needed.

---

## 📊 Key Findings

1. **Card users pay significantly more** than cash users (statistically proven)
2. **Trip duration has minimal predictive power** for fare amount (R² ≈ 2%)
3. Stronger predictors likely include **trip distance, pickup time, and location zones**

---

## 💡 Recommendations

- **Encourage card payments** — associated with higher fare amounts
- **Target peak hours** (late evenings) for higher demand and revenue
- **Focus on high-density zones** (airports, downtown) for frequent shorter trips
- **Extend the model** with trip distance, time of day, and pickup/dropoff zones

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| `pandas`, `numpy` | Data processing |
| `matplotlib`, `seaborn` | Visualization |
| `scipy.stats` | Hypothesis testing (Welch's t-test) |
| `statsmodels` | QQ plot / normality check |
| `scikit-learn` | Linear regression, train-test split |

---



---

## 📁 Project Structure

```
maximizing-taxi-driver-revenue/
│
├── data/                          # Place dataset here (not tracked)
├── maximizing_taxi_driver_revenue.py  # Main analysis script
├── requirements.txt
└── README.md
```

---

## 📋 Requirements

```
pandas
numpy
matplotlib
seaborn
scipy
statsmodels
scikit-learn
```

---


