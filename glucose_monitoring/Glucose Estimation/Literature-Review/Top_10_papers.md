### Top 10 papers: Glucose estimation using wearable sensor data

I’ll focus on non-invasive or minimally invasive glucose estimation using wearable signals such as PPG, ECG, EDA/GSR, skin temperature, accelerometry, and multimodal smartwatch/wristband data, prioritizing research papers that are useful for building a model.

### Top 10 papers

Ranked by relevance to wearable-based glucose estimation, practical research value, and similarity to smartwatch/wristband/ring sensing—not strictly by citation count.

### 1\. Highly relevant

Development of Non-Invasive Continuous Glucose Prediction Models Using Multi-Modal Wearable Sensors in Free-Living Conditions (2025)

* Uses passively collected wearable data in real-world settings.

* Explores physiological, behavioral, circadian and EDA features.

* Uses the BIG IDEAs Lab dataset and ML models including XGBoost.

* [Paper (Open Access)](https://pmc.ncbi.nlm.nih.gov/articles/PMC12115526/?utm_source=chatgpt.com) PubMed Central (PMC) +1

### 2.

Noninvasive Interstitial Glucose Estimation Using Wearables and Machine Learning in Healthy Individuals and Individuals With Obesity: Observational Cohort Study (2026)

* Uses Fitbit Sense 2 and Empatica EmbracePlus.

* Multimodal wearable data with CGM ground truth.

* LSTM-based glucose estimation in real-world conditions.

* [Paper](https://mhealth.jmir.org/2026/1/e91724?utm_source=chatgpt.com) JMIR mHealth and uHealth +1

### 3.

A Multimodal Physiological Dataset for Non-Invasive Blood Glucose Estimation (PhysioCGM, 2025)

* Particularly valuable for research.

* Includes raw ECG, PPG, EDA, skin temperature and accelerometer data with CGM ground truth.

* Longitudinal ambulatory data from participants with Type 1 diabetes.

* [Paper / dataset information](https://pubmed.ncbi.nlm.nih.gov/41258162/?utm_source=chatgpt.com) PubMed

### 4.

Non-invasive Blood Glucose Monitoring Using PPG Signals with Various Deep Learning Models and Implementation Using TinyML (2025)

* PPG-based glucose estimation.

* Evaluates different deep learning architectures.

* Focuses on potential deployment on resource-constrained hardware.

* [Paper (Scientific Reports)](https://www.nature.com/articles/s41598-024-84265-8?utm_source=chatgpt.com) Nature

### 5.

Selection of Noninvasive Features in Wrist-Based Wearable Sensors to Predict Blood Glucose Concentrations Using Machine Learning Algorithms (2022)

* Multimodal wrist sensor feature selection.

* HR, skin temperature, EDA/GSR, heat flux, SpO₂, BP and environmental features.

* Tests multiple regression algorithms.

* [Paper (Open Access)](https://pmc.ncbi.nlm.nih.gov/articles/PMC9100498/?utm_source=chatgpt.com) PubMed Central (PMC)

### 6.

Intelligent Estimation of Blood Glucose Level Using Wristband PPG Signal and Physiological Parameters (2022)

* Wristband PPG with physiological parameters.

* MFCC feature extraction.

* Uses XGBoost regression and feature selection.

* [Paper](https://www.sciencedirect.com/science/article/pii/S1746809422003913?utm_source=chatgpt.com) ScienceDirect

### 7.

Noninvasive Wearables for Remote Monitoring of HbA1c and Glucose Variability: Proof of Concept (2021)

* Wrist-worn wearable data: skin temperature, EDA, HR and accelerometry.

* Investigates prediction of HbA1c and glucose variability.

* Useful for understanding wearable-based glycemic metrics beyond pointwise glucose.

* [Paper (Open Access)](https://pmc.ncbi.nlm.nih.gov/articles/PMC8208014/?utm_source=chatgpt.com) PubMed Central (PMC)

### 8.

Enhanced Blood Glucose Levels Prediction with a Smartwatch (2024)

* Combines smartwatch HR and step data with recent glucose history.

* Studies the added value of wearable signals and activity logging.

* Dataset is available on Figshare.

* [Paper (Open Access)](https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0307136&utm_source=chatgpt.com) | [Dataset](https://figshare.com/articles/dataset/Glucdict_-_Wearable_Sensors_and_CGM/25939312?utm_source=chatgpt.com) PLOS

### 9.

EMD-Based Noninvasive Blood Glucose Estimation from PPG Signals Using Machine Learning Algorithms (2024)

* Uses wrist PPG.

* Empirical Mode Decomposition (EMD) and intrinsic mode features.

* Investigates waveform-based feature engineering.

* [Paper (Open Access)](https://www.mdpi.com/2076-3417/14/4/1406?utm_source=chatgpt.com) MDPI

### 10.

The Effectiveness of Wearable Devices Using Artificial Intelligence for Blood Glucose Level Forecasting or Prediction: Systematic Review (2023)

* Review of wearable-device glucose forecasting and prediction studies.

* Covers PPG, NIR, smartwatch and wristband approaches.

* Useful for discovering additional papers and understanding gaps in the field.

* [Paper (Open Access)](https://www.jmir.org/2023/1/e40259?utm_source=chatgpt.com) jmir.org +1

### Suggested reading order for your research

If you're planning to develop your own glucose-estimation model from smartwatch, wristband or ring data, I would start with:

* Paper #3 — PhysioCGM — for the dataset and sensor-data structure.

* Paper #1 — Free-living multimodal models (2025) — for the ML pipeline and feature engineering.

* Paper #5 — Wrist-based feature selection (2022) — for selecting wearable features.

* Paper #2 — Real-world wearable validation (2026) — for more recent methodology and validation.

* Paper #4 — PPG + deep learning + TinyML — for signal-based modeling and deployment.

Note: Non-invasive glucose estimation remains an experimental research area. Reported performance can be affected by data leakage, subject-level validation, sensor conditions and study size; these papers should not be interpreted as demonstrating clinically reliable glucose measurement.

If you want, I can next compile another 10 papers specifically focused on raw PPG/ECG/EDA sensor signals, excluding papers that rely heavily on glucose history or manual activity/food logging.
