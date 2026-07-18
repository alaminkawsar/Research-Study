# Trend Analysis on Physiological Data from Wearable Devices

> A comprehensive, resource-intensive learning roadmap for analyzing wearable health data including sleep, resting heart rate (RHR), heart rate variability (HRV), physical activity, and recovery. This guide combines foundational concepts with real-world research projects, reproducible code, and practical implementations.

---

## Table of Contents

1. [Introduction & Motivation](#introduction)
2. [Learning Roadmap](#learning-roadmap)
3. [Wearable Health Metrics Explained](#wearable-health-metrics)
4. [Trend Analysis Techniques](#trend-analysis-techniques)
5. [Statistical Methods & Concepts](#statistical-methods)
6. [Foundational Research Papers & Resources](#foundational-research)
7. [Open-Source Projects & Reproducible Code](#open-source-projects)
8. [Practical Datasets](#practical-datasets)
9. [Tools & Libraries](#tools-and-libraries)
10. [Example Projects with Code](#example-projects)
11. [Learning Resources](#learning-resources)
12. [Advanced Topics](#advanced-topics)

---

# Introduction

Modern wearable devices (Apple Watch, Garmin, Fitbit, Oura Ring, WHOOP, Samsung Galaxy Watch, etc.) continuously collect physiological data that can be analyzed to discover long-term health trends.

## Key Questions

Instead of predicting isolated values, the goal is answering:

- Is my Resting Heart Rate improving over time?
- Does sleeping earlier improve recovery?
- Does walking 10,000 steps reduce RHR?
- Does exercise improve sleep quality?
- Can poor sleep predict elevated heart rate tomorrow?
- Can wearable data detect illness before symptoms appear?

These questions define **longitudinal health analytics** — the study of how health metrics change over time for individual subjects.

---

# Learning Roadmap

```
├── Foundational Statistics (1-2 weeks)
│   ├── Descriptive statistics
│   ├── Probability distributions
│   ├── Hypothesis testing
│   └── Correlation & causation
│
├── Exploratory Data Analysis (1 week)
│   ├── Data cleaning
│   ├── Handling missing data
│   ├── Visualization techniques
│   └── Outlier detection
│
├── Time Series Analysis (2-3 weeks)
│   ├── Temporal data structure
│   ├── Moving averages & smoothing
│   ├── Seasonality & trends
│   ├── ARIMA, SARIMA, Prophet
│   └── Change point detection
│
├── Signal Processing (1-2 weeks)
│   ├── Filtering (low-pass, high-pass)
│   ├── Fourier analysis
│   ├── Wavelet decomposition
│   └── Feature extraction
│
├── Longitudinal Health Analytics (2-3 weeks)
│   ├── Mixed effects models
│   ├── Correlation analysis
│   ├── Lag analysis
│   ├── Baseline estimation
│   └── Personalized insights
│
├── Digital Biomarker Discovery (1-2 weeks)
│   ├── Feature engineering
│   ├── Feature selection
│   ├── Multicollinearity assessment
│   └── Health state classification
│
└── Advanced Machine Learning (2-4 weeks)
    ├── Deep learning for time series
    ├── Recurrent neural networks (LSTM, GRU)
    ├── Transformer models
    └── Anomaly detection
```

---

# Wearable Health Metrics

## Heart & Cardiovascular Metrics

### Resting Heart Rate (RHR)
- **Definition**: Beats per minute (BPM) when at complete rest
- **Interpretation**: Lower RHR generally indicates better cardiovascular fitness
- **Typical Range**: 60-100 BPM (athletes: 40-60 BPM)
- **What it indicates**: Stress, recovery, illness, fitness level
- **Analysis approach**: 7-30 day moving average for noise reduction

### Heart Rate Variability (HRV)
- **Definition**: Variation in time intervals between consecutive heartbeats (in milliseconds)
- **Common metrics**: RMSSD, pNN50, LF/HF ratio
- **Interpretation**: Higher HRV typically indicates better parasympathetic tone and recovery
- **Why it matters**: Early indicator of stress, overtraining, or illness
- **Analysis challenge**: Highly individual and affected by circadian rhythm

### Respiratory Rate
- **Typical Range**: 12-20 breaths per minute
- **What it indicates**: Stress levels, fitness, illness
- **Collection**: Often estimated from chest movement or PPG sensors

### Blood Oxygen (SpO₂)
- **Typical Range**: 95-100%
- **What it indicates**: Respiratory health, altitude effects, sleep quality
- **Clinical concern**: Drops below 90% warrant attention

### VO₂ Max
- **Definition**: Maximum oxygen uptake during exercise (ml/kg/min)
- **What it indicates**: Aerobic fitness level
- **Estimation**: Usually calculated from HR response and activity level

---

## Sleep Metrics

### Sleep Duration
- **Recommendation**: 7-9 hours for adults
- **Variability**: ±30-60 minutes acceptable; extreme changes indicate issues
- **Trend analysis**: Look for weekly patterns and monthly trends

### Sleep Efficiency
- **Definition**: (Total Sleep Time / Time in Bed) × 100%
- **Target**: >85% considered good sleep quality
- **Interpretation**: Low efficiency may indicate sleep fragmentation or difficulty falling asleep

### Sleep Stages
- **Light Sleep**: N1 & N2 stages (50-60% of sleep)
- **Deep Sleep**: N3 stage (10-20% of sleep)
- **REM Sleep**: 20-25% of sleep
- **Trend analysis**: Percentage changes in each stage indicate recovery status

### Sleep Consistency
- **Definition**: Day-to-day variability in sleep timing and duration
- **Metric**: Standard deviation of sleep duration/bedtime over 7-30 days
- **Health indicator**: Higher consistency correlates with better health outcomes

---

## Activity & Movement Metrics

### Daily Steps
- **Benchmark**: 7,000-10,000+ steps recommended
- **Trend Analysis**: Weekly totals reveal activity patterns
- **Lag Effects**: Exercise on one day affects next day's RHR and HRV

### Active Minutes
- **Definition**: Time spent in moderate-to-vigorous intensity activity
- **Target**: 150 minutes/week of moderate activity recommended
- **Granularity**: Hourly breakdown useful for pattern recognition

### Exercise Frequency & Duration
- **Types**: Measured separately (cardio, strength, recovery)
- **Trend**: Look for patterns between exercise and recovery metrics
- **Interpretation**: More activity ≠ always better (overtraining effects)

### Calories Burned
- **Components**: Basal metabolic rate (BMR) + activity energy expenditure
- **Variability**: Highly person-dependent; use trends not absolute values
- **Correlation**: Often correlates with activity level and body weight changes

---

## Recovery & Wellness Metrics

### Recovery Score
- **Components**: Usually combines HRV, RHR, sleep quality, previous exertion
- **Scale**: 0-100 (varies by device)
- **Interpretation**: <50 = poor recovery; 50-75 = moderate; >75 = good recovery
- **Action**: Low scores suggest rest or active recovery

### Stress Score
- **Sources**: HRV, heart rate elevation, activity patterns
- **Trend analysis**: Identify stress correlates (work events, sleep, exercise)
- **Lag effects**: High stress predicts poor sleep and elevated RHR

### Readiness/Training Readiness
- **Purpose**: Recommends intensity of today's workout
- **Inputs**: Recovery, stress, sleep, recent activity
- **Use case**: Prevent overtraining by suggesting rest or reduced intensity

---

# Trend Analysis Techniques

## 1. Moving Average & Rolling Mean

**Purpose**: Remove day-to-day noise while preserving trends

```python
# 7-day moving average
df['RHR_MA7'] = df['RHR'].rolling(window=7, center=False).mean()

# 14-day moving average
df['RHR_MA14'] = df['RHR'].rolling(window=14, center=False).mean()

# 30-day moving average
df['RHR_MA30'] = df['RHR'].rolling(window=30, center=False).mean()
```

**When to use**:
- RHR trending
- HRV trending
- Sleep duration trending
- Activity pattern analysis

**Interpretation**:
- Downward trend = Improving metric
- Upward trend = Worsening or changing condition
- Inflection points = Notable changes in status

---

## 2. Exponential Moving Average (EMA)

**Purpose**: Give more weight to recent observations while still considering history

```python
# EMA with 7-day span
df['RHR_EMA'] = df['RHR'].ewm(span=7, adjust=False).mean()

# Calculate the trend (first derivative)
df['RHR_trend'] = df['RHR_EMA'].diff()
```

**Advantages over simple moving average**:
- More responsive to recent changes
- Better for identifying trend reversals
- Smoother transitions

---

## 3. Rolling Standard Deviation & Consistency

**Purpose**: Measure stability/variability of a metric over time

```python
# 7-day rolling standard deviation
df['RHR_std7'] = df['RHR'].rolling(window=7).std()

# Coefficient of Variation (normalized measure)
df['RHR_cv'] = df['RHR_std7'] / df['RHR_MA7']

# Interpret: Higher values = more variability
# Lower values = more consistent/stable
```

**Applications**:
- **Sleep Consistency**: Low std dev = regular sleep schedule (good)
- **Heart Rate Stability**: Low std dev = stable cardiovascular state (good)
- **Activity Consistency**: Identify users with variable activity patterns

---

## 4. Trend Line Fitting & Linear Regression

**Purpose**: Quantify directional change over longer periods

```python
import numpy as np
from scipy import stats

# Fit linear regression to last 30 days
x = np.arange(len(df.tail(30)))
slope, intercept, r_value, p_value, std_err = stats.linregress(x, df['RHR'].tail(30).values)

# Interpretation
if slope < 0:
    print("✓ RHR is improving (decreasing)")
elif slope > 0:
    print("✗ RHR is worsening (increasing)")
else:
    print("→ RHR is stable")
    
# Statistical significance
if p_value < 0.05:
    print(f"Trend is statistically significant (p={p_value:.3f})")
else:
    print(f"Trend is not statistically significant (p={p_value:.3f})")
```

**Interpretations**:
- **Negative slope**: Fitness improving, stress decreasing, or recovery improving
- **Positive slope**: Possible fatigue, illness, stress, or overtraining
- **Near-zero slope**: Metric is stable

---

## 5. Seasonal Decomposition

**Purpose**: Separate trend, seasonal, and residual components

```python
from statsmodels.tsa.seasonal import seasonal_decompose

# Decompose RHR into trend, seasonality, and residuals
decomposition = seasonal_decompose(df['RHR'], model='additive', period=7)
trend = decomposition.trend
seasonal = decomposition.seasonal
residual = decomposition.resid

# Visualize
import matplotlib.pyplot as plt
fig, axes = plt.subplots(4, 1, figsize=(12, 10))
df['RHR'].plot(ax=axes[0], title='Original RHR')
trend.plot(ax=axes[1], title='Trend Component')
seasonal.plot(ax=axes[2], title='Weekly Seasonal Component')
residual.plot(ax=axes[3], title='Residual (Noise)')
plt.tight_layout()
plt.show()
```

**Use cases**:
- **Weekly seasonality**: Weekday vs weekend patterns
- **Circadian rhythm**: Intraday variations in HRV
- **Long-term trends**: Separating background trend from noise

---

## 6. Change Point Detection

**Purpose**: Identify when metrics significantly change

```python
from ruptures import Pelt

# Detect change points
algo = Pelt(model="l2", min_size=3, jump=1).fit(df['RHR'].values)
changepoints = algo.predict(pen=10)

print(f"Change points detected at indices: {changepoints}")

# Visualize
import matplotlib.pyplot as plt
plt.figure(figsize=(14, 4))
plt.plot(df['RHR'].values, label='RHR')
for cp in changepoints:
    plt.axvline(x=cp, color='red', linestyle='--', alpha=0.7)
plt.legend()
plt.title('RHR with Change Points')
plt.show()
```

**Practical applications**:
- Detect when user started exercising (RHR drops)
- Detect illness (RHR/HRV suddenly changes)
- Detect lifestyle changes (sleep pattern shift)
- Identify overtraining (recovery metric decline)

---

## 7. Lag Analysis

**Purpose**: Understand delayed effects between variables

```python
import pandas as pd

# Create lagged features
df['Sleep_lag1'] = df['Sleep_Duration'].shift(1)  # Yesterday's sleep
df['Sleep_lag2'] = df['Sleep_Duration'].shift(2)  # 2 days ago
df['Activity_lag1'] = df['Steps'].shift(1)

# Calculate correlations with different lags
for lag in range(1, 8):
    df[f'Sleep_lag{lag}'] = df['Sleep_Duration'].shift(lag)
    correlation = df[f'Sleep_lag{lag}'].corr(df['RHR'])
    print(f"Correlation between {lag}-day-ago Sleep and Today's RHR: {correlation:.3f}")
```

**Common findings**:
- Yesterday's sleep → Today's RHR (stronger than same-day)
- Yesterday's exercise → Today's recovery score
- Day-before activity → Tonight's sleep quality

---

## 8. Correlation & Cross-Correlation Analysis

**Purpose**: Understand relationships between different metrics

```python
import pandas as pd
import numpy as np

# Pearson correlation
correlation = df['Sleep_Duration'].corr(df['RHR'])

# Correlation matrix for multiple variables
metrics = ['Sleep_Duration', 'RHR', 'HRV', 'Steps', 'Recovery_Score']
correlation_matrix = df[metrics].corr()

# Spearman correlation (rank-based, more robust to outliers)
spearman_corr = df['Sleep_Duration'].corr(df['RHR'], method='spearman')

# Statistical significance
from scipy.stats import pearsonr, spearmanr
r, p_value = pearsonr(df['Sleep_Duration'], df['RHR'])
print(f"Correlation: {r:.3f}, p-value: {p_value:.4f}")

# Visualization
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(8, 6))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
plt.title('Wearable Metrics Correlation Matrix')
plt.show()
```

---

# Statistical Methods

## Descriptive Statistics

```python
# Summary statistics
print(df[['RHR', 'Sleep_Duration', 'HRV']].describe())

# Percentiles for individual baseline
percentiles = df['RHR'].quantile([0.05, 0.25, 0.5, 0.75, 0.95])
print(percentiles)

# Personalized baseline (mean of historical data)
baseline_RHR = df['RHR'].mean()
baseline_std = df['RHR'].std()
```

## Correlation Analysis

- **Pearson**: Assumes linear relationship; sensitive to outliers
- **Spearman**: Rank-based; more robust; non-parametric
- **Kendall**: Alternative rank correlation; good for small samples

## Linear Regression

**Single predictor**:
```python
from sklearn.linear_model import LinearRegression

X = df[['Sleep_Duration']].values
y = df['RHR'].values

model = LinearRegression()
model.fit(X, y)

print(f"Sleep explains {model.score(X, y):.2%} of RHR variance")
print(f"For each additional hour of sleep: RHR changes by {model.coef_[0]:.2f} bpm")
```

**Multiple predictors**:
```python
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import StandardScaler

# Prepare features
features = ['Sleep_Duration', 'Steps', 'Stress_Score', 'HRV']
X = df[features].values
y = df['RHR'].values

# Standardize features for interpretability
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

model = LinearRegression()
model.fit(X_scaled, y)

# Interpret coefficients
for feature, coef in zip(features, model.coef_):
    print(f"{feature}: {coef:.3f} (standardized effect)")
```

## Mixed Effects Models

**Purpose**: Analyze repeated measures from multiple subjects while accounting for individual differences

```python
import statsmodels.formula.api as smf

# If you have data from multiple people
# model = smf.mixedlm("RHR ~ Sleep_Duration", data=df, groups=df["user_id"])
# result = model.fit()
# print(result.summary())
```

## Time Series Analysis Methods

### ARIMA (AutoRegressive Integrated Moving Average)

```python
from statsmodels.tsa.arima.model import ARIMA

# Fit ARIMA model to RHR data
model = ARIMA(df['RHR'], order=(1, 1, 1))  # (p, d, q)
result = model.fit()

# Forecast next 7 days
forecast = result.get_forecast(steps=7)
print(forecast.summary_frame())
```

### Prophet (Facebook's Time Series Forecasting)

```python
from prophet import Prophet
import pandas as pd

# Prepare data
data = df[['ds', 'RHR']].copy()
data.columns = ['ds', 'y']

# Create and fit model
model = Prophet(interval_width=0.95)
model.fit(data)

# Make future dataframe
future = model.make_future_dataframe(periods=30)
forecast = model.predict(future)

# Plot
model.plot(forecast)
plt.title('RHR Forecast')
plt.show()
```

## Anomaly Detection

```python
from sklearn.ensemble import IsolationForest

# Detect anomalies in RHR
iso_forest = IsolationForest(contamination=0.05, random_state=42)
df['anomaly'] = iso_forest.fit_predict(df[['RHR']])

# -1 indicates anomaly
anomalies = df[df['anomaly'] == -1]
print(f"Detected {len(anomalies)} anomalous days")

# Alternative: Z-score method
df['z_score'] = np.abs(stats.zscore(df['RHR']))
df['anomaly_zscore'] = df['z_score'] > 3  # 3 standard deviations
```

---

# Foundational Research Papers & Resources

## Tier 1: Must-Read Papers ⭐⭐⭐⭐⭐

### 1. Best Practices for Analyzing Large-Scale Health Data from Wearables

**Authors**: Steinhubl, Muse, Topol  
**Journal**: npj Digital Medicine  
**Link**: https://www.nature.com/articles/s41746-019-0121-1

**Why read it**: Foundational methodology for wearable health analytics

**Key concepts**:
- Why rolling averages are essential (noise reduction)
- Why daily averages are misleading (need longitudinal perspective)
- How to compare individuals (personalized baselines)
- How to perform longitudinal studies (statistical frameworks)
- Common statistical pitfalls

**Implementation notes**:
- 7-30 day rolling averages recommended
- Individual baselines required for interpretation
- Population-level inferences require careful statistical controls

---

### 2. Functional Data Analysis on Wearable Sensor Data ⭐⭐⭐⭐⭐

**Journal**: arXiv  
**Link**: https://arxiv.org/abs/2410.11562

**Key topics**:
- Functional Data Analysis (FDA) theory
- Longitudinal modeling with continuous observations
- Smoothing techniques (splines, kernels)
- Functional PCA for dimension reduction
- Circadian rhythm modeling

**What makes it different**: Most papers use standard stats; this uses advanced FDA methodology

---

### 3. All of Us Research Program: Wearable Data ⭐⭐⭐⭐⭐

**Journal**: Nature Medicine  
**Link**: https://www.nature.com/articles/s41591-026-04352-3

**Why important**: Shows how world's largest wearable dataset is structured and analyzed

**Learn**:
- Wearable feature definitions and standardization
- Longitudinal cohort design at scale
- Quality control procedures
- Data structure for research

---

## Tier 2: Important Applications & Methods ⭐⭐⭐⭐

### 4. Stanford Wearable Infection Detection ⭐⭐⭐⭐⭐

**GitHub**: https://github.com/StanfordBioinformatics/wearable-infection  
**Paper**: Published in Nature Medicine

**Why study code + paper**: Practical implementation of concepts

**Key algorithms**:
- Healthy baseline calculation
- Rolling baseline adaptation
- Z-score computation for anomalies
- Resting heart rate trend analysis
- Statistical thresholding

**Reproducible workflow**:
```
Individual Baseline Calculation
    ↓
Baseline Deviation (Z-scores)
    ↓
Change Point Detection
    ↓
Health Status Classification
    ↓
Alert Generation
```

---

### 5. Wearable-Derived Physiological Features for Disease Classification ⭐⭐⭐⭐

**GitHub**: https://github.com/xueyann/wearable-transdiagnostic-classification-allofus  
**Data**: Fitbit data from All of Us Research Program

**Demonstrates**:
- Feature engineering from raw wearable data
- Correlation matrix analysis
- Multicollinearity assessment (VIF)
- Feature selection methods
- Logistic regression for disease prediction

**Feature pipeline**:
```
Raw Metrics (RHR, HRV, Sleep, Activity, Steps)
    ↓
Calculate Derived Features (trends, variability, lags)
    ↓
Build Correlation Matrix
    ↓
Calculate VIF (Variance Inflation Factor)
    ↓
Remove Multicollinear Features
    ↓
Train Classification Model
    ↓
Validate & Interpret
```

---

### 6. Cross-Study Analysis of Wearable Datasets ⭐⭐⭐⭐

**Conference**: PMLR  
**Link**: https://proceedings.mlr.press/v248/kasl24a.html

**Key insight**: Same wearable metrics behave differently across studies

**Learn**:
- Multiple regression across populations
- Cross-study validation approaches
- Dataset bias and generalization challenges
- Population-specific vs universal biomarkers

---

## Tier 3: Specialized Topics ⭐⭐⭐

### 7. NiMBaLWear Analytics Pipeline ⭐⭐⭐⭐

**Paper**: https://link.springer.com/article/10.1186/s44247-024-00062-3

**Pipeline stages**:
```
Raw Accelerometer/PPG Data
    ↓ Signal Cleaning & Filtering
Wear Detection & Non-wear Removal
    ↓ Activity Detection
Sleep/Wake Detection
    ↓ Feature Extraction
Physiological Metrics (HRV, Sleep Stages)
    ↓ Health Metrics Computation
Longitudinal Analysis
    ↓ Personalized Insights
```

---

### 8. Reproducible Analysis Pipeline for Mobile & Wearable Data ⭐⭐⭐

**Journal**: Frontiers in Digital Health  
**Link**: https://www.frontiersin.org/articles/10.3389/fdgth.2021.769823

**Focuses on**:
- Raw sensor processing and calibration
- Segmentation into meaningful epochs
- Feature computation at multiple timescales
- Visualization best practices
- Reproducibility and documentation

---

### 9. Data Quality in Wrist-Worn Wearables ⭐⭐⭐

**ArXiv**: https://arxiv.org/abs/2401.13518

**Critical for real studies**: Data quality >> ML sophistication

**Topics**:
- Missing data patterns and imputation
- Non-wear detection algorithms
- Quality assessment metrics
- Device artifacts and noise sources
- Optimal analysis window selection

---

## Tier 4: Specialized Domains ⭐⭐

### 10. GLOBEM: Depression Detection via Wearables & Mobile Sensing ⭐⭐⭐

**GitHub**: https://github.com/UW-EXP/GLOBEM

**Learn**:
- Feature engineering for mental health
- Longitudinal behavior modeling
- Multi-modal sensor fusion
- Privacy-preserving analysis

**Repository structure to study**:
```
feature_engineering/          # How features are computed
model/                       # Model architectures
analysis/                    # Statistical validation
preprocessing/               # Data cleaning pipeline
```

---

# Open-Source Projects & Reproducible Code

## Complete Workflow Examples

### Project 1: Wearable Health Analytics Pipeline

**GitHub**: https://github.com/StanfordBioinformatics/wearable-infection

**What you can learn**:
- Complete preprocessing pipeline
- Baseline calculation methods
- Anomaly detection implementation
- Statistical testing for significance

**Directory structure**:
```
wearable-infection/
├── data/
│   ├── sample_heart_rate.csv
│   └── sample_activity.csv
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_baseline_calculation.ipynb
│   ├── 03_anomaly_detection.ipynb
│   └── 04_visualization.ipynb
├── src/
│   ├── preprocessing.py
│   ├── baseline.py
│   ├── anomaly.py
│   └── statistics.py
└── README.md
```

---

### Project 2: All of Us Wearable Feature Engineering

**GitHub**: https://github.com/xueyann/wearable-transdiagnostic-classification-allofus

**Key scripts to study**:
- `feature_engineering.py` - Computing derived features
- `correlation_analysis.py` - Feature relationships
- `multicollinearity.py` - VIF calculations
- `modeling.py` - Disease prediction

---

### Project 3: GLOBEM Platform

**GitHub**: https://github.com/UW-EXP/GLOBEM

**For learning**:
- `feature_engineering/` - Time-series feature extraction
- `model/` - LSTM and transformer implementations
- `analysis/` - Statistical validation methods

---

## Jupyter Notebooks to Study

### Recommended Notebooks

1. **Time Series Analysis Template**
   ```
   https://github.com/StanfordBioinformatics/wearable-infection/
   blob/main/notebooks/03_anomaly_detection.ipynb
   ```

2. **Feature Engineering Walkthrough**
   ```
   https://github.com/xueyann/wearable-transdiagnostic-classification-allofus/
   blob/main/notebooks/feature_engineering.ipynb
   ```

3. **Statistical Analysis Guide**
   ```
   https://github.com/StanfordBioinformatics/wearable-infection/
   blob/main/notebooks/02_baseline_calculation.ipynb
   ```

---

# Practical Datasets

## Research Datasets (Public)

### PhysioNet
**URL**: https://physionet.org/

**Datasets**:
- **ECG datasets**: Cardiac signal analysis
- **Sleep datasets**: Sleep stage classification
- **ICU data**: Hospital physiological monitoring
- **Wearable signals**: Real wearable device data

**Best for**: Learning signal processing and multi-channel analysis

---

### MIMIC-IV (Medical Information Mart for Intensive Care)
**URL**: https://physionet.org/content/mimiciv/

**Contents**:
- Hospital ICU data from thousands of patients
- Continuous monitoring data
- Detailed temporal information

**Use case**: Large-scale longitudinal analysis, disease prediction

---

### WESAD (Wearable Stress and Affect Detection)
**URL**: https://ubicomp.ics.uci.edu/datasets/wesad

**Signals included**:
- ECG (electrocardiogram)
- EDA (electrodermal activity)
- Temperature
- Accelerometer (3-axis)

**Best for**: Stress detection and affect recognition

---

### All of Us Research Program Wearable Data
**URL**: https://www.allofusresearch.org/

**Available devices**:
- Fitbit devices (most common)
- Apple Watch data (available to researchers)

**Scale**: 500,000+ participants with continuous wearable data

**Best for**: Large-scale population studies, generalization

---

### UCI Machine Learning Repository
**URL**: https://archive.ics.uci.edu/

**Search for**: "wearable", "health", "ECG", "sleep"

---

### Kaggle Datasets
**URL**: https://www.kaggle.com/datasets

**Search**: "wearable health", "fitbit", "sleep", "heart rate"

---

# Tools & Libraries

## Data Processing & Analysis

| Library | Purpose | Key Functions |
|---------|---------|---|
| **pandas** | Data manipulation | DataFrames, time series resampling |
| **numpy** | Numerical computing | Array operations, statistics |
| **polars** | Fast data processing | Arrow-based tables (faster than pandas) |
| **scipy** | Scientific computing | Stats, signal processing, optimization |

---

## Visualization

| Library | Best For | Example Use |
|---------|----------|---|
| **matplotlib** | Static plots | Publication-quality figures |
| **plotly** | Interactive plots | Dashboards, web apps |
| **seaborn** | Statistical graphics | Heatmaps, distributions |
| **bokeh** | Interactive dashboards | Real-time monitoring |

---

## Statistics & Time Series

| Library | Purpose | Key Methods |
|---------|---------|---|
| **statsmodels** | Statistical models | ARIMA, seasonal decomposition, mixed effects |
| **scipy.stats** | Statistical tests | Correlation, hypothesis testing |
| **prophet** | Time series forecasting | Trend + seasonality modeling |
| **pymc** | Bayesian statistics | Probabilistic modeling |

---

## Signal Processing

| Library | Purpose |
|---------|---------|
| **scipy.signal** | Filtering, spectral analysis |
| **pywt** | Wavelet decomposition |
| **mne** | EEG/MEG/ECG signal processing |

---

## Machine Learning & Anomaly Detection

| Library | Use Case |
|---------|----------|
| **scikit-learn** | Classification, regression, clustering |
| **xgboost** | Gradient boosting |
| **tensorflow/keras** | Deep learning |
| **pytorch** | Deep learning research |
| **pyod** | Outlier/anomaly detection |

---

## Feature Engineering

| Library | Purpose |
|---------|---------|
| **tsfresh** | Time series feature extraction |
| **featuretools** | Automated feature engineering |

---

## Time Series Specific

| Library | Purpose |
|---------|----------|
| **sktime** | Unified time series API |
| **tslearn** | Time series ML algorithms |
| **ruptures** | Change point detection |

---

# Example Projects with Code

## Project 1: Sleep vs RHR Analysis

**Research Question**: Does better sleep lower Resting Heart Rate?

### Data Structure
```python
import pandas as pd
import numpy as np

# Example data format
data = {
    'Date': pd.date_range('2024-01-01', periods=90),
    'Sleep_Duration': np.random.normal(7.5, 1.2, 90),
    'Sleep_Score': np.random.normal(75, 10, 90),
    'Sleep_Efficiency': np.random.normal(0.85, 0.08, 90),
    'RHR': np.random.normal(65, 5, 90),
    'HRV': np.random.normal(50, 15, 90),
    'Steps': np.random.normal(8000, 2000, 90),
}

df = pd.DataFrame(data)
```

### Exploratory Analysis
```python
import matplotlib.pyplot as plt
import seaborn as sns

fig, axes = plt.subplots(3, 1, figsize=(12, 10))

# Plot 1: Daily metrics
axes[0].plot(df['Date'], df['Sleep_Duration'], label='Sleep (hrs)', alpha=0.7)
axes[0].plot(df['Date'], df['Sleep_Score']/10, label='Sleep Score/10', alpha=0.7)
axes[0].set_ylabel('Sleep Metrics')
axes[0].legend()

# Plot 2: RHR daily
axes[1].plot(df['Date'], df['RHR'], label='Daily RHR', alpha=0.5)
axes[1].plot(df['Date'], df['RHR'].rolling(7).mean(), label='7-day MA', linewidth=2)
axes[1].set_ylabel('RHR (bpm)')
axes[1].legend()

# Plot 3: HRV daily
axes[2].plot(df['Date'], df['HRV'], label='Daily HRV', alpha=0.5)
axes[2].plot(df['Date'], df['HRV'].rolling(7).mean(), label='7-day MA', linewidth=2)
axes[2].set_ylabel('HRV (ms)')
axes[2].legend()

plt.tight_layout()
plt.show()
```

### Correlation Analysis
```python
# Correlation with same-day sleep
same_day_corr = df[['Sleep_Duration', 'Sleep_Score', 'RHR', 'HRV']].corr()
print("Same-day correlations:")
print(same_day_corr)

# Lag analysis: yesterday's sleep vs today's RHR
df['Sleep_lag1'] = df['Sleep_Duration'].shift(1)
df['Sleep_Score_lag1'] = df['Sleep_Score'].shift(1)

lag1_sleep_rhr = df['Sleep_lag1'].corr(df['RHR'])
lag1_sleep_efficiency = df['Sleep_Efficiency'].shift(1).corr(df['RHR'])

print(f"\nLag-1 Sleep Duration → RHR correlation: {lag1_sleep_rhr:.3f}")
print(f"Lag-1 Sleep Efficiency → RHR correlation: {lag1_sleep_efficiency:.3f}")

# Visualization
fig, ax = plt.subplots(1, 1, figsize=(10, 6))
sns.scatterplot(data=df, x='Sleep_Duration', y='RHR', alpha=0.6, ax=ax)
# Add regression line
z = np.polyfit(df['Sleep_Duration'].dropna(), df['RHR'].iloc[df['Sleep_Duration'].notna()], 1)
p = np.poly1d(z)
ax.plot(df['Sleep_Duration'].sort_values(), p(df['Sleep_Duration'].sort_values()), 
        "r--", alpha=0.8, label=f'y={z[0]:.2f}x+{z[1]:.1f}')
ax.set_xlabel('Sleep Duration (hours)')
ax.set_ylabel('Resting Heart Rate (bpm)')
ax.set_title('Sleep vs RHR Relationship')
ax.legend()
plt.show()
```

### Linear Regression Model
```python
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import StandardScaler
import statsmodels.formula.api as smf

# Univariate model
model1 = smf.ols('RHR ~ Sleep_Duration', data=df).fit()
print(model1.summary())

# Multivariate model
model2 = smf.ols('RHR ~ Sleep_Duration + Sleep_Score + Sleep_Efficiency + HRV', 
                  data=df).fit()
print(model2.summary())

# Interpretation
print("\nModel coefficients (what predicts RHR):")
for var, coef in model2.params.items():
    print(f"  {var}: {coef:.3f}")
```

### Trend Analysis
```python
# Calculate moving averages
df['Sleep_MA7'] = df['Sleep_Duration'].rolling(7).mean()
df['Sleep_MA30'] = df['Sleep_Duration'].rolling(30).mean()
df['RHR_MA7'] = df['RHR'].rolling(7).mean()
df['RHR_MA30'] = df['RHR'].rolling(30).mean()

# Fit trend line
from scipy import stats

x = np.arange(len(df))
slope_sleep, intercept_sleep, _, _, _ = stats.linregress(x, df['Sleep_Duration'])
slope_rhr, intercept_rhr, _, _, _ = stats.linregress(x, df['RHR'])

print(f"Sleep trend (slope): {slope_sleep:.4f} hours/day")
print(f"RHR trend (slope): {slope_rhr:.4f} bpm/day")

# Visualize trends
fig, axes = plt.subplots(2, 1, figsize=(12, 8))

axes[0].plot(df['Date'], df['Sleep_Duration'], alpha=0.3, label='Daily')
axes[0].plot(df['Date'], df['Sleep_MA7'], label='7-day MA', linewidth=2)
axes[0].plot(df['Date'], df['Sleep_MA30'], label='30-day MA', linewidth=2)
axes[0].set_ylabel('Sleep Duration (hours)')
axes[0].legend()
axes[0].set_title(f'Sleep Duration Trend (slope={slope_sleep:.4f} hrs/day)')

axes[1].plot(df['Date'], df['RHR'], alpha=0.3, label='Daily')
axes[1].plot(df['Date'], df['RHR_MA7'], label='7-day MA', linewidth=2)
axes[1].plot(df['Date'], df['RHR_MA30'], label='30-day MA', linewidth=2)
axes[1].set_ylabel('RHR (bpm)')
axes[1].set_xlabel('Date')
axes[1].legend()
axes[1].set_title(f'RHR Trend (slope={slope_rhr:.4f} bpm/day)')

plt.tight_layout()
plt.show()
```

---

## Project 2: Activity vs Recovery Analysis

**Research Question**: How does daily activity affect next-day recovery?

### Feature Engineering
```python
import pandas as pd
import numpy as np

# Create lagged activity features
for lag in range(1, 8):
    df[f'Steps_lag{lag}'] = df['Steps'].shift(lag)
    df[f'Active_Minutes_lag{lag}'] = df['Active_Minutes'].shift(lag)
    df[f'Calories_lag{lag}'] = df['Calories_Burned'].shift(lag)

# Create moving averages of activity
df['Steps_MA3'] = df['Steps'].rolling(3).mean()
df['Steps_MA7'] = df['Steps'].rolling(7).mean()

# Categorize activity levels
df['Activity_Level'] = pd.cut(df['Steps'], 
                               bins=[0, 5000, 10000, 15000, 25000],
                               labels=['Sedentary', 'Light', 'Moderate', 'High'])
```

### Correlation Analysis
```python
# Create lag correlation analysis
lag_correlations = {}
for lag in range(0, 8):
    df_temp = df.copy()
    if lag > 0:
        df_temp['Steps_lag'] = df_temp['Steps'].shift(lag)
    else:
        df_temp['Steps_lag'] = df_temp['Steps']
    
    corr = df_temp['Steps_lag'].corr(df_temp['Recovery_Score'])
    lag_correlations[lag] = corr

# Plot lag correlations
plt.figure(figsize=(10, 5))
lags = list(lag_correlations.keys())
corrs = list(lag_correlations.values())
plt.bar(lags, corrs)
plt.xlabel('Days of Lag')
plt.ylabel('Correlation with Recovery Score')
plt.title('Activity Lag Effects on Recovery')
plt.axhline(y=0, color='k', linestyle='-', linewidth=0.5)
plt.show()
```

### Machine Learning: Predict Recovery
```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score

# Prepare features
features = [col for col in df.columns if 'lag' in col or 'MA' in col]
X = df[features].dropna()
y = df.loc[X.index, 'Recovery_Score']

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train model
model = RandomForestRegressor(n_estimators=100, random_state=42)
model.fit(X_train, y_train)

# Evaluate
y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f"MSE: {mse:.3f}")
print(f"R² Score: {r2:.3f}")

# Feature importance
importances = pd.DataFrame({
    'Feature': features,
    'Importance': model.feature_importances_
}).sort_values('Importance', ascending=False)

print("\nTop 10 Most Important Features:")
print(importances.head(10))
```

---

## Project 3: Illness Detection via Wearables

**Research Question**: Can anomalies in wearable metrics predict illness?

### Baseline Calculation
```python
# Calculate individual healthy baseline
df['RHR_baseline'] = df['RHR'].rolling(window=30, center=False).mean()
df['HRV_baseline'] = df['HRV'].rolling(window=30, center=False).mean()

# Calculate deviation from baseline
df['RHR_deviation'] = df['RHR'] - df['RHR_baseline']
df['HRV_deviation'] = df['HRV'] - df['HRV_baseline']

# Calculate z-scores
df['RHR_zscore'] = (df['RHR'] - df['RHR'].mean()) / df['RHR'].std()
df['HRV_zscore'] = (df['HRV'] - df['HRV'].mean()) / df['HRV'].std()
```

### Anomaly Detection
```python
from sklearn.ensemble import IsolationForest
from sklearn.preprocessing import StandardScaler

# Multi-metric anomaly detection
metrics = ['RHR', 'HRV', 'Sleep_Duration', 'Respiratory_Rate']
X = df[metrics].values

# Normalize
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Train isolation forest
iso_forest = IsolationForest(contamination=0.05, random_state=42, n_estimators=100)
df['anomaly'] = iso_forest.fit_predict(X_scaled)
df['anomaly_score'] = iso_forest.score_samples(X_scaled)

# Identify anomalous days
anomalies = df[df['anomaly'] == -1][['Date', 'RHR', 'HRV', 'Sleep_Duration']]
print(f"Detected {len(anomalies)} anomalous days")
print(anomalies)
```

### Statistical Thresholding
```python
# Define thresholds for anomaly
rhr_threshold_high = df['RHR'].mean() + 2 * df['RHR'].std()
hrv_threshold_low = df['HRV'].mean() - 2 * df['HRV'].std()
sleep_threshold_low = df['Sleep_Duration'].mean() - 1.5 * df['Sleep_Duration'].std()

# Multi-metric alert
df['illness_alert'] = (
    (df['RHR'] > rhr_threshold_high) &  # High RHR
    (df['HRV'] < hrv_threshold_low) &   # Low HRV
    (df['Sleep_Duration'] < sleep_threshold_low)  # Poor sleep
)

alerts = df[df['illness_alert'] == True][['Date', 'RHR', 'HRV', 'Sleep_Duration']]
print(f"Multi-metric alerts: {len(alerts)} days")
```

### Visualization
```python
fig, axes = plt.subplots(4, 1, figsize=(14, 10))

# RHR with baselines
axes[0].plot(df['Date'], df['RHR'], alpha=0.5, label='Daily RHR')
axes[0].plot(df['Date'], df['RHR_baseline'], label='30-day Baseline', linewidth=2)
axes[0].fill_between(df['Date'], 
                      df['RHR_baseline'] - 2*df['RHR'].std(),
                      df['RHR_baseline'] + 2*df['RHR'].std(),
                      alpha=0.2, label='±2 SD')
# Highlight anomalies
anomalous = df[df['anomaly'] == -1]
axes[0].scatter(anomalous['Date'], anomalous['RHR'], color='red', s=100, label='Anomaly', zorder=5)
axes[0].set_ylabel('RHR (bpm)')
axes[0].legend()
axes[0].set_title('RHR with Anomaly Detection')

# HRV
axes[1].plot(df['Date'], df['HRV'], alpha=0.5, label='Daily HRV')
axes[1].plot(df['Date'], df['HRV_baseline'], label='30-day Baseline', linewidth=2)
axes[1].scatter(anomalous['Date'], anomalous['HRV'], color='red', s=100, zorder=5)
axes[1].set_ylabel('HRV (ms)')
axes[1].legend()

# Sleep
axes[2].bar(df['Date'], df['Sleep_Duration'], alpha=0.5, label='Sleep Duration')
axes[2].axhline(y=df['Sleep_Duration'].mean(), color='orange', label='Average')
axes[2].scatter(anomalous['Date'], anomalous['Sleep_Duration'], color='red', s=100, zorder=5)
axes[2].set_ylabel('Sleep (hours)')
axes[2].legend()

# Anomaly scores
axes[3].plot(df['Date'], df['anomaly_score'], label='Anomaly Score')
axes[3].axhline(y=0, color='black', linestyle='--', linewidth=0.5)
axes[3].scatter(anomalous['Date'], anomalous['anomaly_score'], color='red', s=100, zorder=5)
axes[3].set_ylabel('Anomaly Score')
axes[3].set_xlabel('Date')
axes[3].legend()

plt.tight_layout()
plt.show()
```

---

# Learning Resources

## Books

### Statistics & Data Science
1. **Practical Statistics for Data Scientists**
   - Statistical tests for real data
   - Practical examples over theory
   - Very readable

2. **Forecasting: Principles and Practice** (Free online)
   - https://otexts.com/fpp3/
   - Time series fundamentals
   - Prophet, ARIMA, ETS

3. **Python for Data Analysis** — Wes McKinney
   - pandas mastery
   - Data manipulation techniques

### Time Series
4. **Time Series Analysis by State Space Methods** — James Durbin & Siem Jan Koopman
   - Advanced methodology
   - State space models

5. **An Introduction to Time Series Analysis** — Paul S.P. Spin
   - Comprehensive reference

### Signal Processing
6. **The Scientist and Engineer's Guide to Digital Signal Processing** (Free online)
   - Filtering, FFT, window functions
   - Very practical

7. **Biomedical Signal Analysis** — various authors
   - ECG, EEG, EMG processing
   - Medical signal interpretation

---

## Online Courses

### Time Series Analysis
- **Coursera: Practical Time Series Analysis** — UC Davis
- **Coursera: Advanced Time Series Models** — UC Davis
- **Udemy: Time Series Analysis with Python** — Various instructors
- **edX: Time Series Forecasting** — Microsoft

### Statistics
- **Khan Academy: Statistics and Probability** (Free)
- **StatQuest with Josh Starmer** (YouTube - Free)
- **Coursera: Statistics with R** — Duke University

### Data Science & Python
- **Kaggle Learn** (Free) - Practical tutorials
- **DataCamp** - Interactive courses
- **Real Python** (Free articles)

### Machine Learning & Deep Learning
- **Coursera: Machine Learning** — Andrew Ng
- **Fast.ai** - Practical deep learning
- **DeepLearning.AI** - AI specialization

---

## Communities & Journals

### Journals for Wearable Health Research
- Nature Digital Medicine
- npj Digital Medicine
- IEEE Journal of Biomedical and Health Informatics
- JMIR mHealth and uHealth
- IEEE Transactions on Biomedical Engineering
- Sensors (MDPI)

### Communities
- r/MachineLearning (Reddit)
- r/statistics (Reddit)
- Cross Validated (StackExchange)
- Kaggle Competitions

---

# Advanced Topics

After mastering the fundamentals, explore:

## Statistical Theory
- Bayesian Statistics (PyMC, Stan)
- Causal Inference (causal-ml, DoWhy)
- Survival Analysis (lifelines)
- Generalized Estimating Equations (GEE)

## Signal Processing
- Wavelet Analysis
- Spectral Analysis (Fourier, Periodogram)
- Adaptive Filtering
- Signal Decomposition

## Digital Biomarkers
- Biomarker validation methodologies
- Clinical implementation
- Regulatory pathways (FDA validation)

## Circadian Rhythm Analysis
- Cosinor analysis
- Circadian rhythm modeling
- Chronotype classification
- Shift work health impacts

## Deep Learning for Time Series
- LSTMs (Long Short-Term Memory)
- GRUs (Gated Recurrent Units)
- Transformers & Attention mechanisms
- Temporal CNNs
- Seq2Seq models

## Personalized Analytics
- Individual effect heterogeneity
- N-of-1 trial design
- Single-case experimental design
- Idiographic vs nomothetic approaches

## Explainable AI (XAI)
- SHAP values for feature importance
- LIME for local interpretability
- Integrated Gradients
- Attention visualization

---

# Project Implementation Checklist

## Phase 1: Foundation (Weeks 1-2)
- [ ] Learn pandas data manipulation
- [ ] Understand basic statistics (mean, std, correlation)
- [ ] Create exploratory visualizations
- [ ] Set up development environment (Python, Jupyter)

## Phase 2: Analysis (Weeks 3-4)
- [ ] Implement moving averages
- [ ] Calculate trending (linear regression)
- [ ] Perform correlation analysis
- [ ] Detect anomalies (z-score, isolation forest)

## Phase 3: Modeling (Weeks 5-6)
- [ ] Train predictive models (linear regression, random forest)
- [ ] Perform time series forecasting (ARIMA, Prophet)
- [ ] Validate models (train/test split, cross-validation)
- [ ] Interpret results

## Phase 4: Advanced (Weeks 7-8)
- [ ] Implement lag analysis
- [ ] Develop personalized baselines
- [ ] Explore deep learning (LSTM)
- [ ] Create interactive visualizations

---

# Final Recommendations

## For Beginners
1. Start with **sleep vs RHR analysis** (simple, interpretable)
2. Read **Best Practices for Analyzing Large-Scale Health Data** (foundational)
3. Study **Stanford Wearable Infection Detection code** (practical implementation)
4. Build a simple **correlation analysis** dashboard

## For Intermediate Learners
1. Study **All of Us Wearable Disease Classification repository** (feature engineering)
2. Implement **anomaly detection pipeline** (practical application)
3. Learn **mixed effects models** (for longitudinal data)
4. Explore **time series forecasting** (Prophet/ARIMA)

## For Advanced Practitioners
1. Read **Functional Data Analysis on Wearable Sensor Data** (advanced statistics)
2. Study **GLOBEM platform** (deep learning + wearables)
3. Implement **Bayesian causal inference** for health effects
4. Develop **digital biomarkers** for disease detection

---

# Quick Reference: Common Wearable Metrics

| Metric | Normal Range | Good Range | Improving | Concerning |
|--------|--------------|-----------|-----------|-----------|
| **RHR** | 60-100 bpm | 50-70 bpm | Decreasing | > 100 or sudden increase |
| **HRV** | 20-200 ms | 50+ ms | Increasing | < 20 ms |
| **Sleep Duration** | 6-9 hours | 7-9 hours | Consistent | < 6 or > 10 hours |
| **Sleep Efficiency** | 80-90% | > 85% | High | < 80% |
| **Recovery Score** | 0-100 | > 75 | Stable/High | < 40 |
| **VO₂ Max** | Individual | Increasing | Improving fitness | Decreasing |
| **SpO₂** | 95-100% | > 95% | Stable | < 90% |

---

# Glossary

- **Baseline**: Individual's healthy/normal level (used as reference)
- **Chronotype**: Individual's natural sleep/wake timing preference
- **Circadian Rhythm**: ~24-hour biological cycle (sleep-wake, HRV, RHR)
- **Coefficient of Variation**: Standard deviation / mean (normalized variability)
- **Cosinor Analysis**: Fitted cosine model to detect circadian patterns
- **Digital Biomarker**: Physiological signature derived from wearable data predicting health outcome
- **EDA**: Electrodermal Activity (skin conductance)
- **HRV**: Heart Rate Variability (beat-to-beat interval variation)
- **Lag**: Time delay between two variables
- **Longitudinal**: Following same individual over time
- **Overtraining**: Exercise stress exceeding recovery capacity
- **PPG**: Photoplethysmography (optical heart rate measurement)
- **Seasonality**: Repeating patterns at fixed intervals (e.g., weekly)
- **Trend**: Directional change over time
- **RMSSD**: Root Mean Square of Successive Differences (HRV metric)
- **Z-score**: (Value - Mean) / Standard Deviation (standardized distance from mean)

---

⭐ **Long-term Goal**: Build an end-to-end wearable health analytics pipeline capable of:
1. Transforming raw physiological data into meaningful health insights
2. Generating personalized recommendations
3. Predicting health state changes before they become obvious
4. Detecting digital biomarkers for disease risk
5. Contributing to scientific understanding of human health dynamics
