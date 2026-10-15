# Time series correlation List
**GPT-Q1:** <br>
*Do you find more time series correlation name?* <br>
* Autocorrelation Function (ACF)

* Partial Autocorrelation Function (PACF)

* Cross-Correlation Function (CCF)

* Lagged Cross-Correlation

* Lead–Lag Correlation

* Dynamic Correlation

* Rolling Correlation

* Moving-Window Correlation

* Time-Varying Correlation

* Detrended Cross-Correlation Analysis (DCCA)

* Detrended Fluctuation Analysis (DFA)-based correlation

* Wavelet Correlation

* Wavelet Coherence

* Spectral Correlation

* Cross-Spectral Correlation

* Magnitude-Squared Coherence

* Phase Coherence

* Circular Cross-Correlation

* Seasonal Cross-Correlation

* Partial Cross-Correlation

* Prewhitened Cross-Correlation

* Rank Cross-Correlation for Time Series

* Distance Cross-Correlation

* Quantile Cross-Correlation

* Conditional Correlation

* Multivariate Autocorrelation

* Multivariate Cross-Correlation

* Canonical Correlation for Time Series

* Cointegration-Based Long-Run Association

* Tail Dependence in Time Series

* Copula-Based Dynamic Dependence

* Local Gaussian Correlation

* Transfer Entropy

* Convergent Cross Mapping (CCM)

* Correlation Integral

* Recurrence-Based Measures of Dependence

* Time-Frequency Correlation

* Lagged Mutual Information

* Cross-Mutual Information

* Dynamic Conditional Correlation (DCC)

* Generalized Autoregressive Score (GAS) Dynamic Correlation

* BEKK-GARCH Conditional Covariance/Correlation

* Engle–Kroner Multivariate GARCH Correlation

* Pearson Correlation of Differenced Series

* Correlation of Residuals

* Correlation of Innovations

* Correlation of Forecast Errors

* Intraclass Correlation for Repeated Measures

* Agreement/Concordance Measures for Longitudinal Data

---

**GPT-Q2:** <br>
*I want to see the glucose trends and others physiological data correlation, so which one might helpful for this?*


For studying correlations between glucose trends and other physiological data (heart rate, sleep, physical activity, stress, blood pressure, etc.), these time-series methods are especially useful:

| Method                                         | Useful for                                                                                                        |
| ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| 1. Lagged Cross-Correlation                    | Finding whether heart rate, exercise, or sleep changes are associated with glucose changes minutes or hours later |
| 2. Rolling Correlation                         | Seeing how the relationship changes over days or weeks                                                            |
| 3. Dynamic Conditional Correlation (DCC)       | Estimating changing correlations between multiple time series                                                     |
| 4. Cross-Correlation Function (CCF)            | Examining relationships across different time lags                                                                |
| 5. Partial Cross-Correlation                   | Examining relationships while accounting for other variables or lags, depending on the method used                |
| 6. Spearman Rank Correlation for Time Series   | Measuring monotonic relationships when they aren't necessarily linear                                             |
| 7. Wavelet Coherence                           | Identifying relationships that vary across both time and timescale                                                |
| 8. Cross-Spectral Analysis                     | Finding shared cyclical patterns, such as daily rhythms                                                           |
| 9. Detrended Cross-Correlation Analysis (DCCA) | Examining relationships between nonstationary series with trends                                                  |
| 10. Lagged Mutual Information                  | Detecting lagged nonlinear dependencies                                                                           |
| 11. Conditional Mutual Information             | Assessing dependence while accounting for additional variables                                                    |
| 12. Granger Causality Test                     | Testing whether past values of one series improve predictions of another                                          |
| 13. Transfer Entropy                           | Measuring directed predictive information flow, including nonlinear relationships                                 |
| 14. Cointegration Analysis                     | Checking for long-run relationships between suitable nonstationary series                                         |
| 15. Correlation of Differenced Series          | Studying whether short-term changes move together rather than merely sharing a trend                              |

### My recommended starting set

For a glucose-focused project, I'd begin with these five:

* Lagged cross-correlation — when might activity or heart rate relate to later glucose changes?

* Rolling correlation — does the relationship change over time?

* Spearman correlation — is there a monotonic association?

* Wavelet coherence — do glucose and another signal share patterns at particular timescales?

* Granger causality testing — does one signal improve prediction of another?

A key consideration: glucose and physiological signals often have trends, daily rhythms, missing measurements, and different sampling frequencies. These can produce misleading correlations. Align timestamps, account for time of day and relevant confounders, and consider detrending or differencing where appropriate.

Important: correlation and predictive dependence do not establish that one physiological variable causes glucose to change. These analyses can reveal patterns, but they do not by themselves establish a medical conclusion.

---

**GPT-Q3**: <br>
*Right, I want to see just a little change of spike, for example taking 170g or more glucose and see any kinds of effectmethods

Ah, got it! You want to study small physiological changes after consuming a large amount of glucose (170 g or more) and identify how those changes relate to the glucose spike over time.

For that kind of research, I'd focus on these methods:

| Method                       | What you could investigate                                                                            |
| ---------------------------- | ----------------------------------------------------------------------------------------------------- |
| 1. Event-Triggered Analysis  | What changes occur before and after glucose consumption?                                              |
| 2. Change-Point Detection    | When does a measurable shift in a physiological signal begin?                                         |
| 3. First-Difference Analysis | Are small changes in heart rate, glucose, or other measurements occurring together?                   |
| 4. Lagged Cross-Correlation  | Does a change in heart rate, skin temperature, or another signal precede or follow a glucose spike?   |
| 5. Rolling Correlation       | Does the relationship strengthen around the glucose spike?                                            |
| 6. Anomaly Detection         | Which physiological measurements depart from their normal baseline?                                   |
| 7. Wavelet Analysis          | Can brief, subtle changes be detected at different timescales?                                        |
| 8. Distributed-Lag Models    | How are physiological measurements associated with glucose exposure over subsequent minutes or hours? |
| 9. Functional Data Analysis  | How do entire physiological response curves differ between experiments?                               |
| 10. Mixed-Effects Models     | Are the responses consistent across repeated experiments or different people?                         |

### A practical analysis design

![¿De qué nos sirve evaluar las tendencias del perfil glucémico ambulatorio? | Avances en Diabetología](https://images.openai.com/static-rsc-4/ERAAypJvNfF_9YBEnOwDfvFZNvs2qWvVvD2sS0ninPDfpBLnuMpLoRtaTzZwNkfRkPIbgykR-oghYL0ajvRKlfmhkv43sTjXgAq7NF9RaF6Rq4dDKy0Jd1-J8wZvCUSRfWRlA7QnE0GVLEWFiAMsAVnoYDq-tnAbqs0qk8hxD79LkdCqAtG3CuW0cxv_vRu9?purpose=fullsize)

1\. Establish a baseline

Record glucose and physiological measurements before the exposure.

![How to Interpret Your CGM Data - Nourished by Science](https://images.openai.com/static-rsc-4/vBp1FsOvzNHatSobOUGWXHsoJaYwzwSVPsiyIVOxXw8p8K9pS94fgaNbOjGM2atM7jgkVSlhLR2ZsR-Fo954qxzxheH-X_4TGH4Spa9SZ1rXi_Ns8bC5TnuXZcJk9qE4rC9GyIEJ6-nka3PbC8yjqtX2CrP0MyicnSe7Cx-o-TE-r9SSPuc01tJvWRTjdvrv?purpose=fullsize)

2\. Track the response

Measure the glucose rise, peak, time to peak, and recovery alongside heart rate, activity, sleep or other available signals.

![Assured Information Management and Sharing (AIMS), Emory University](https://images.openai.com/static-rsc-4/6BoUMXq0msEkVgkNAi_e5MoRUUtz1yxLF_hgyToJsjCaUQh5GuGIZ_M7eBMn7FvJMMUAtH4tATQy4fhF6-QShDjewUpuNl-Vw75lj6_uhAf_yWDGuuLNGj_t3uLdgF7dWfACjV4wV2s7hZm2FCIZGTr1WwMIj_J-iRYkX9AHyTjTyi6SP_44ZPTq6Ex3DhpP?purpose=fullsize)

3\. Detect subtle effects

Align the signals by timestamp, examine short-term changes, and test whether changes consistently occur around the glucose response.

One important safety note: 170 g of pure glucose is a very large acute glucose load. Don't deliberately consume that amount to run an experiment without appropriate medical supervision. If this concerns an actual exposure or symptoms, seek medical guidance.

One question: What physiological data do you want to correlate with glucose?

Physiological signals

Heart rate

Heart-rate variability (HRV)

Blood pressure

Skin temperature

Sweating / electrodermal activity

Respiration rate

Brain activity (EEG)

Insulin / other blood biomarkers

Other signals

How will you obtain glucose measurements?

Continuous glucose monitor (CGM)

Finger-prick measurements

Existing research dataset

Other

Find suitable methods

---

**GPT-Q4**: <br>
*I want to study subtle physiological changes associated with glucose spikes. Signals: Heart rate, Heart-rate variability (HRV), Blood pressure, Skin temperature, Sweating / electrodermal activity, Respiration rate, Brain activity (EEG), Insulin / other blood biomarkers, Other signals. Glucose data source: CGM. Recommend suitable time-series analysis methods.*

For your project, I would treat this as a multimodal physiological time-series analysis problem: use continuous glucose monitor (CGM) data to identify glucose spikes, then investigate whether subtle changes in heart rate, HRV, blood pressure, skin temperature, electrodermal activity, respiration, EEG, or blood biomarkers occur before, during, or after those spikes.

The key is to distinguish a genuine physiological response from ordinary variation, sensor noise, time-of-day effects, and changes caused by activity or stress.

### 1\. Best methods for your research

1\. Change-point detection

Detect the time when heart rate, HRV, or skin temperature begins to deviate from its baseline. Useful for finding subtle shifts rather than only large spikes.

2\. Event-triggered analysis

Align measurements around each detected glucose rise, then calculate average responses before and after the event. This is a strong first method for your question.

3\. First differences and rate of change

Analyze changes between consecutive measurements instead of only raw values. For example, determine whether HRV starts falling as glucose rises.

4\. Lagged cross-correlation

Test whether a physiological signal tends to change before or after a glucose change. Check several plausible time lags, not just simultaneous measurements.

5\. Distributed-lag regression

Estimate how glucose changes are associated with physiological measurements across a window of time, while adjusting for factors such as activity, meals, sleep, and time of day.

6\. Mixed-effects models

If you have repeated observations or multiple participants, estimate the average response while accounting for differences between people and events.

These choices are consistent with research emphasizing temporal dependence, glucose excursions, data quality, and the time-series nature of CGM measurements.

### 2\. How I would build the analysis

| Stage                 | Recommended method                                                          |
| --------------------- | --------------------------------------------------------------------------- |
| Prepare the data      | Timestamp alignment, missing-data checks, sensor-quality checks             |
| Detect glucose events | Local peak detection, excursion size and duration                           |
| Find subtle responses | Change-point detection, first differences                                   |
| Measure timing        | Lagged cross-correlation, distributed-lag models                            |
| Compare events        | Event-triggered averages and mixed-effects models                           |
| Check reliability     | Confidence intervals, sensitivity analysis, correction for multiple testing |

Important detail: CGMs measure glucose in interstitial fluid rather than directly measuring blood glucose, so sensor lag and noise matter when interpreting exact timing.

### 3\. What to prioritize by signal

* Heart rate and HRV: first differences, change-point detection, lagged correlation.

* Blood pressure: event-triggered analysis and distributed-lag regression.

* Skin temperature and sweating: change-point detection and rolling statistics.

* Respiration: lagged correlation and time-frequency analysis.

* EEG: signal-specific feature extraction, followed by event-related analysis; raw EEG samples should not simply be correlated directly with CGM readings.

* Insulin and other biomarkers: distributed-lag models, accounting for when each sample was collected.

### My strongest recommendation

Start with event-triggered analysis + change-point detection + distributed-lag regression. Together, these can help you find small changes, identify when they occur, and estimate their association with glucose dynamics.

For safety, study naturally occurring glucose excursions or existing research datasets rather than deliberately consuming 170 g or more of pure glucose. That amount is a substantial acute glucose load and should not be used as a self-experiment without appropriate medical supervision.

---

**Looking for more insight**

---

