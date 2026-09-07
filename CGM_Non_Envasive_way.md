# Wearable Sensor + CGM Datasets

A curated collection of publicly available datasets that combine continuous glucose monitoring (CGM) with wearable or physiological sensor data.

This repository supports research into whether physiological signals from non‑invasive wearable sensors can be used to:

- Estimate current blood glucose
- Detect glucose rising/falling trends
- Predict future glucose levels
- Detect impending glucose spikes
- Detect possible hypoglycemia/hyperglycemia
- Understand individual physiological responses to meals and glucose excursions

Core research question
----------------------
Can physiological signals available from wearable devices provide enough information to understand or predict blood glucose behavior without directly measuring glucose?

Dataset overview
----------------
| Dataset | Participants | CGM / Glucose | Wearable / Physiological Signals | Food / Context | Access | Priority |
|---|---:|---|---|---|---:|---:|
| PhysioCGM | 10 (T1D) | Dexcom G6, ~5 min | ECG, PPG/BVP, EDA, skin temperature, accelerometer, HR, respiration | Limited | Open | ⭐⭐⭐⭐⭐ |
| BIG IDEAs | 16 | Dexcom G6, ~5 min | PPG/BVP, EDA, skin temperature, accelerometer, HR, IBI | Food + nutrition | Open | ⭐⭐⭐⭐⭐ |
| HUPA-UCM | 25 (T1D) | FreeStyle Libre 2 | HR, activity, steps, calories, sleep | Meals, carbs, insulin | Open | ⭐⭐⭐⭐ |
| D1NAMO | 29 total | Glucose/CGM | ECG, respiration, accelerometer, HR/activity | Food photos + insulin | Open | ⭐⭐⭐⭐ |
| OhioT1DM | 12 (T1D) | CGM | Fitness-band physiological data | Meals, insulin, exercise | Controlled / restricted | ⭐⭐⭐⭐ |
| T1D-UOM | 16 | CGM | Activity, sleep | Nutrition + insulin | Open | ⭐⭐⭐ |
| BrisT1D | 24 | Diabetes-device glucose data | Smartwatch data | Longitudinal context | Mixed | ⭐⭐⭐ |

Detailed datasets
-----------------
1. PhysioCGM

Best overall match for raw physiological-signal → CGM research. PhysioCGM contains synchronized physiological signals and CGM data from people with type 1 diabetes in free‑living conditions.

- Participants: 10 people with T1D, up to ~17 days per participant
- Sensors: Zephyr BioHarness (ECG 250 Hz, respiration 25 Hz, accelerometer, HR, breathing rate, posture), Empatica E4 (PPG/BVP, HR, EDA, skin temp, accelerometer)
- Ground truth: Dexcom G6 CGM (~5‑minute samples)

Potential tasks: glucose estimation, trend classification, forecasting, spike detection, personalized modeling

Resources:
- PhysioCGM paper: https://www.nature.com/articles/s41597-025-06090-6
- PhysioCGM GitHub: https://github.com/PSI-TAMU/PhysioCGM

2. BIG IDEAs Lab Glycemic Variability & Wearable Device Dataset

Well suited for wearable + CGM + nutrition research (Dexcom G6 + Empatica E4; food & nutrition labels available).

- Participants: ~16, 8–10 days each
- Signals: PPG/BVP, HR, IBI, EDA, skin temp, accelerometer
- Glucose: Dexcom G6 (~5‑min)
- Food context: amount, calories, carbs, fiber, sugar, protein, fat

Resources:
- PhysioNet BIG IDEAs dataset: https://www.physionet.org/content/big-ideas-glycemic-wearable/1.1.3/

3. HUPA‑UCM Diabetes Dataset

Combines CGM with lifestyle and wearable activity data.

- Participants: 25 people with T1D, ~14+ days
- Data: FreeStyle Libre 2, HR, steps, calories, sleep, insulin, meals, carbs

Resource:
- Mendeley Data: https://data.mendeley.com/datasets/3hbcscwz44/1

4. D1NAMO

Good for studying cardiac physiology (ECG/respiration) vs glucose.

- Participants: 20 healthy, 9 with T1D
- Signals: ECG, respiration, accelerometer, HR/activity
- Other: glucose, food photos, insulin

Resource:
- Zenodo: https://zenodo.org/records/5651217

5. OhioT1DM

A commonly used benchmark for glucose-prediction research with long recordings (~8 weeks per participant).

- Participants: 12 people with T1D
- Data: CGM, insulin pump records, fitness-band physiological data, meals, exercise

Access: restricted — data use process required

Resource:
- OhioT1DM dataset info: https://webpages.charlotte.edu/rbunescu/ohiot1dm.html

6. T1D‑UOM (Manchester CS Coordinated Diabetes Study)

Longitudinal dataset focused on lifestyle & glucose.

- Participants: 16
- Data: glucose, activity, sleep, insulin, nutrition, demographics

Resource:
- Repository: https://github.com/sharpic/ManchesterCSCoordinatedDiabetesStudy

7. BrisT1D

Longitudinal smartwatch + diabetes-device data (~6 months per participant for some subjects).

- Participants: 24 young adults with T1D
- Data: diabetes-device exports, glucose, smartwatch signals, contextual data

Resource:
- University of Bristol data portal: https://data.bris.ac.uk/data/dataset/33z5jc8fa6tob21ptrugzqog08

8. Glucose‑ML

A project aiming to standardize multiple glucose datasets into a common analysis framework; useful for building multi‑dataset corpora.

- Repo: https://github.com/Augmented-Health-Lab/Glucose-ML-Project

Unified dataset schema (suggested)
---------------------------------
Recommended common fields for ML experiments (allow missing values where not available):

- timestamp
- Physiological signals: ecg, ppg, hr, hrv, eda, skin_temperature, respiration, accelerometer_x/y/z
- Activity: steps, activity, sleep
- Nutrition: meal, carbohydrates, sugar, protein, fat, calories
- Diabetes context: insulin (type / dose / timestamp)
- Ground truth: cgm_glucose
- Derived labels: glucose_delta_5m/15m/30m/60m, glucose_trend, glucose_spike, hypoglycemia, hyperglycemia

Recommended research tasks
--------------------------
- Task 1 — Glucose state classification (Low / Normal / High)
- Task 2 — Glucose trend detection (rapidly rising, rising, stable, falling, rapidly falling)
- Task 3 — Future glucose prediction (e.g., predict CGM at t+15 or t+30 using past wearable data)
- Task 4 — Glucose spike prediction (binary label: spike within window)
- Task 5 — Glucose excursion prediction (predict ΔGlucose over upcoming window)

Experimental strategy
---------------------
Suggested progression:
1. Develop models on PhysioCGM (rich physiological signals)
2. Validate independently on BIG IDEAs (nutrition labels) and HUPA‑UCM (lifestyle)
3. Test ECG‑focused hypotheses on D1NAMO
4. Evaluate longitudinal generalization on OhioT1DM and BrisT1D

Compare population (one model for many people) vs personalized models (adapt to an individual's physiology). Subject‑independent validation is essential to avoid data leakage.

Important limitations
---------------------
- Small cohort sizes for many datasets
- Large inter‑subject variability
- Bias toward T1D populations in several datasets
- Heterogeneous CGM and wearable devices / sampling rates
- Missing data and synchronization issues
- CGM measurement lag relative to blood glucose
- Confounding (meals, exercise, stress, sleep)

Resources (expanded)
--------------------
Datasets & repositories
- PhysioCGM: https://github.com/PSI-TAMU/PhysioCGM
- BIG IDEAs (PhysioNet): https://www.physionet.org/content/big-ideas-glycemic-wearable/1.1.3/
- HUPA‑UCM (Mendeley): https://data.mendeley.com/datasets/3hbcscwz44/1
- D1NAMO (Zenodo): https://zenodo.org/records/5651217
- OhioT1DM: https://webpages.charlotte.edu/rbunescu/ohiot1dm.html
- BrisT1D: https://data.bris.ac.uk/data/dataset/33z5jc8fa6tob21ptrugzqog08
- Glucose‑ML: https://github.com/Augmented-Health-Lab/Glucose-ML-Project

Signal processing & feature extraction
- WFDB / PhysioNet tools: https://physionet.org/ (wfdb-python: https://github.com/MIT-LCP/wfdb-python)
- NeuroKit2 (physiological signal processing, HRV, EDA): https://neurokit2.readthedocs.io/
- HeartPy (PPG/HR analysis): https://github.com/paulvangentcom/heartrate_analysis_python
- BioSPPy (biosignal processing): https://biosppy.readthedocs.io/
- pyEDFlib (EDF file I/O): https://github.com/holgern/pyedflib
- tsfresh (automated time‑series feature extraction): https://tsfresh.readthedocs.io/

Time‑series & ML frameworks
- scikit‑learn: https://scikit-learn.org/
- PyTorch: https://pytorch.org/
- TensorFlow / Keras: https://www.tensorflow.org/
- tsai (deep learning for time series): https://github.com/timeseriesAI/tsai
- sktime (classical time‑series ML): https://www.sktime.org/

Evaluation / benchmarks / reproducibility
- Consider subject‑wise cross‑validation (leave‑one‑subject‑out) and report per‑subject metrics
- Metrics: MAE / RMSE for regression, AUC/precision/recall/F1 for classification, detection latency for spike detection
- Standardize preprocessing (resampling, filtering, artifact rejection, synchronization)

Ethics, privacy & licenses
- Check each dataset's license / data‑use agreement before redistribution
- Protect participant privacy; do not re‑identify individuals
- Follow institutional review and data governance for secondary analyses

Suggested baseline methods
- Classic features + gradient boosting (e.g., XGBoost / LightGBM) as interpretable baselines
- LSTM / TCN / Temporal CNN models for sequence modeling
- Hybrid models combining feature‑based and deep learning approaches

How to cite
-----------
Cite the original dataset publications or data portals. When using multiple datasets, list each dataset and its source. Example:

"Dataset: PhysioCGM — [PhysioCGM paper link]; BIG IDEAs — PhysioNet link; ..."

Next steps I can take
---------------------
- Commit this README.md to the repository (I can add it now)
- Create per‑dataset example notebooks (data loading & preprocessing templates)
- Generate a scripts/ folder with utilities for resampling, synchronization and feature extraction

If you want, I will add this README.md to the repository now.
