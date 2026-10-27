### Deep-search results: public datasets for glucose-related smartwatch waveforms

Yes. I found several publicly available datasets that can support your research. The strongest match is the BIG IDEAs Lab dataset, because it combines raw wrist PPG waveforms, other wearable signals, and food logs. PhysioCGM is another strong option for studying physiological signals alongside glucose fluctuations.

The important distinction is that you want to observe what sensor signals do after eating or consuming glucose, not necessarily predict glucose concentration. I therefore evaluated datasets on whether they provide:

* Raw PPG or other physiological waveforms, not just summary statistics.

* Meal timestamps or food logs.

* Continuous recordings before and after eating.

* Public access and usable licensing.

### 1\. Best-matching datasets

![Emotion Tracking: Mobile Electrodermal Activity (mEDA) and Facial Expressions | Department of Geography | UZH](https://images.openai.com/static-rsc-4/T_6OgvDGdLnz8VGigbvYWhP-dCa4weClXdMA63cyzyUxrWkc1kuDlpB2xGtLuyrKqmjKIh-KtxINPngPunBUMI730dStaIWySTj4EvSwZFeeYeAcK8z0mpPnbT5YPA5pA6MlH1M7h0SF2eKn_R58wJVC86mTqQZWMGakBbaUQNIJb7T4bxoWKnoxRhT1NhKo?purpose=fullsize)

Top match

1\. BIG IDEAs Lab Glycemic Variability and Wearable Device Data

PhysioNet · Version 1.1.3 · Updated April 2026

[Access dataset](https://physionet.org/content/big-ideas-glycemic-wearable/1.1.3/?utm_source=chatgpt.com)

16 participants · Approximately 8–10 days each

This dataset includes wrist-worn Empatica E4 recordings, food logs, and continuous glucose monitor data. Participants wore the devices during everyday life and received a standardized breakfast every other day.

Available signals

* Raw blood-volume pulse (BVP/PPG): 64 Hz

* Heart rate and interbeat intervals

* Electrodermal activity (EDA): 4 Hz

* Skin temperature: 4 Hz

* Three-axis accelerometry: 32 Hz

* Food logs and glucose readings

Access: Open. License: Open Data Commons Attribution License 1.0.

Why it fits: You can align the raw PPG waveform and other signals to meal times, plot changes before and after eating, and compare different meals or repeated breakfasts. You can ignore the glucose readings if you don't want to analyze glucose concentration.

![Wrist-Worn Sensor Validation for Heart Rate Variability and Electrodermal Activity Detection in a Stressful Driving Environment | MDPI](https://images.openai.com/static-rsc-4/RLO6w8_vWgLblJkucwQ7c08oFA4sTdDQfdI8le1A5iaexeGsgSC12rFZHxhqHonW3C65ebS0Jhi58Neq8d4BmcxYuX1VTyWMX7wazlX0QJ1Jy-KryP5hdgfrEWfuvCYzGCGpyhaPyfk8nCdqnfYB1yZataBNK-S1XJ8kvSXK5RjqdkRLqe_dmd3mz66bxPht?purpose=fullsize)

2\. PhysioCGM: A Multimodal Physiological Dataset for Non-Invasive Blood Glucose Estimation

Scientific Data · 2025

[Access dataset](https://springernature.figshare.com/articles/dataset/PhysioCGM_a_multimodal_physiological_dataset_for_non-invasive_blood_glucose_estimation/28136294?utm_source=chatgpt.com)

10 participants with type 1 diabetes · Up to 17 days

This dataset combines wearable physiological recordings with continuous glucose monitoring in real-world settings.

Available signals

* Wrist PPG/BVP and EDA

* Wrist skin temperature and accelerometry

* Raw ECG and respiratory signals from a chest-worn device

* Continuous glucose monitor readings

Why it fits: It provides multiple synchronized physiological signals that can be plotted as time series. You can examine whether waveform characteristics vary around glucose excursions.

Limitation: The population has type 1 diabetes, and the data are collected during everyday life rather than a controlled glucose-consumption experiment. The dataset description does not establish that every meal has a reliable timestamp.

Access: Public Figshare dataset. License: CC0 1.0.

![CGMacros: a pilot scientific dataset for personalized nutrition and diet monitoring | Scientific Data](https://images.openai.com/static-rsc-4/5yK4lLbyHz96q62spbc83eO2PNwTkHbHG8O2iGrRYZyW2Ry8hlNOKBQ4i7zrAw9J0GDWTYb2T9GxjKx3cZdUl-JGxmvwJ6ewgT36ZrxyBJReFzraydYJIdwNV6EhNN5Ga9JfR-9D98wiAMRNy50InsZ_kk-DdZVgD-XCAlykjEHY04hw8ka9OswvHAZfXNfw?purpose=fullsize)

3\. CGMacros: A Scientific Dataset for Personalized Nutrition and Diet Monitoring

PhysioNet · Version 1.0.0 · 2025

[Access dataset](https://physionet.org/content/cgmacros/1.0.0/?utm_source=chatgpt.com)

45 participants · Approximately 10 days each

Participants wore continuous glucose monitors and fitness trackers while recording meals and food photographs. The dataset includes people without diabetes, people with prediabetes, and people with type 2 diabetes.

Available signals and context

* Heart rate and activity-tracker measurements

* Continuous glucose readings

* Meal timestamps, macronutrients, and food photographs

Why it fits: It gives you meal-linked physiological data and nutritional context for comparing post-meal trends.

Limitation: The main files report readings at one-minute intervals. This is useful for heart-rate trends, but it is not a raw, high-frequency PPG waveform dataset.

Access: Public. License: CC BY-NC-SA 4.0 (non-commercial, share-alike).

![Quantifying Spatiotemporal Characteristics of Urban Wetland Soundscapes and Their Associative Pathways Regulating Restorative Benefits](https://images.openai.com/static-rsc-4/Qh6rkGr1QdDxubE6P7zjqKfG2kY01l2dFAgkfpz1I806c04n6z3d2EqCWQl9mnQDRcWOU2posR4DBOGoE06JZhyb_dS436pmqDnPYQDkkXXsDQ4D5Mmy-NmZQg8YM7wJYVUEb7XqaIdHY86AsA0WETgjt-C1f7338mjHrkZxpWdwmmZYH4o4GvvVbNMsFCNJ?purpose=fullsize)

4\. WIMID — Wrist IMU Meals and Intakes Dataset

Zenodo · Published January 2026

[Access dataset](https://zenodo.org/records/18176217?utm_source=chatgpt.com)

11 participants · Approximately 528 hours · 159 meals

This dataset contains wrist-worn accelerometer and gyroscope recordings during everyday activities, with periods of eating and non-eating.

Why it fits: It may help you identify eating periods and investigate how wrist movement changes during meals.

Limitation: It has no PPG or skin-temperature signal, so it cannot directly answer your physiological-waveform question. The repository currently labels access as restricted, so confirm access eligibility before relying on it.

### 2\. Additional datasets worth considering

These are useful if you want more raw sensor data or meal annotations, but each is missing a key element.

![Assessing Drivers’ Physiological Responses Using Consumer Grade Devices | MDPI](https://images.openai.com/static-rsc-4/x-d02nMc7r_La3RbL_XaK8IAz9piwa70ooYjDlgb7w94Cos4v1Q2OIhgzKS3mkvidhu918q7ClnG8xN3rGQJkng1v7jMFI-cuPgw2YxRYl2u7LMnOx6lc-QsDCJc6V1Dkwjvk9TO8tJKZgbNF20Nrz-SAuhleKauAxuSrmb83jY3M1OiGM9CZZFm6IzlDdT8?purpose=fullsize)

5\. IMU50 — High-Frequency Wrist-Worn Multimodal Dataset

2026 · 50 participants · Five continuous days

[Read dataset paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC13571289/?utm_source=chatgpt.com)

Contains raw dual-channel PPG at 25 Hz, accelerometer and gyroscope data at 128 Hz, and wrist temperature recorded every minute.

Useful for: Learning how to process raw wrist waveforms and study ordinary day-to-day physiological variation.

Missing: Specific meal timestamps and controlled glucose-consumption labels.

![Smartwatch-Based Eating Detection: Data Selection for Machine Learning from Imbalanced Data with Imperfect Labels](https://images.openai.com/static-rsc-4/4c2VcXDWTyiaUM-VDzLmRuqHTHOSgvaRosr1azAqrJwFsIKoLzvEznuL4FiP5CkqQNqjat9SSPcSKtmS4Y462qKdHPQVjJFlJ-qc_xJR71Co0Ytsj2A9tz3sPgIdwSPXh49q47b2NMDYKYjMOeh3q6f-2jtOpyVJ-v3nR_crC4N27RYwp2Cej34YRNOLmz39?purpose=fullsize)

6\. Free-living Food Intake Cycle (FreeFIC)

6 participants · 16 sessions · Approximately 77 hours

[Access dataset](https://mug.ee.auth.gr/free-food-intake-cycle-detection/?utm_source=chatgpt.com)

Provides smartwatch accelerometer and gyroscope signals at 100 Hz, with annotated meal start and end times.

Useful for: Studying meal-event alignment and developing analysis methods around eating periods.

Missing: PPG, heart rate, skin temperature, and glucose measurements.

![Machine Learning-Based Respiration Rate and Blood Oxygen Saturation Estimation Using Photoplethysmogram Signals](https://images.openai.com/static-rsc-4/y01qmfQrkvf-PlFSDj5Rf-xC37JE5BY4a8cFm7EeoV-fKN3MneLJayvCW64qWb2HbCAb3v7GVXl7lmoujbDWgsTzL8bSNGeE6PBj5F6kGzoVKQPMkIqRJGMekQiuc_wW_veFEgVsJ5CwqjcHOVghnsiRamL0_mG29Hq_kZ5vPqn7GQ3oyqK1cD1-nfWKphFm?purpose=fullsize)

7\. Open PPG Dataset for Non-Invasive Blood Glucose Monitoring

Zenodo · 24 volunteers · 125 signal samples

[Access dataset](https://zenodo.org/records/21978226?utm_source=chatgpt.com)

Contains raw optical PPG signals, accelerometry, and reference blood glucose measurements. The PPG was collected using a multichannel finger sensor, rather than a wrist smartwatch.

Useful for: Examining waveform morphology across different glucose measurements.

Missing: Clearly established longitudinal meal-linked wearable recordings. It should not be treated as a post-meal time-series dataset without confirming the sample protocol.

### 3\. Comparison against your exact requirements

| Dataset                  | Raw PPG            | Meal information                   | Longitudinal data | Controlled glucose intake                |
| ------------------------ | ------------------ | ---------------------------------- | ----------------- | ---------------------------------------- |
| BIG IDEAs Lab            | Yes                | Food logs, standardized breakfasts | Yes               | Partial: repeated standardized breakfast |
| PhysioCGM                | Yes                | Meal timestamps not established    | Yes               | No                                       |
| CGMacros                 | No raw PPG         | Detailed meal logs                 | Yes               | No; free-living meals                    |
| WIMID                    | No                 | Annotated eating periods           | Yes               | No                                       |
| IMU50                    | Yes                | No meal labels                     | Yes               | No                                       |
| FreeFIC                  | No                 | Annotated meal periods             | Multiple sessions | No                                       |
| Open PPG glucose dataset | Yes, finger sensor | Not established                    | Limited samples   | Not established                          |

The table distinguishes a dataset that contains meal information from one that explicitly controls the amount and timing of glucose consumption. Those are not equivalent.

### 4\. My recommendation for your research

### Start with BIG IDEAs Lab, then consider PhysioCGM

Recommended workflow

* Download the [BIG IDEAs Lab dataset, version 1.1.3](https://physionet.org/content/big-ideas-glycemic-wearable/1.1.3/?utm_source=chatgpt.com).

* Load the raw BVP/PPG, heart-rate, EDA, temperature, accelerometer, and food-log files for a participant.

* Identify meal times and extract signal windows, for example 30 minutes before and 120 minutes after each meal.

* Plot the raw PPG waveform, pulse amplitude and morphology, heart rate, interbeat intervals, EDA, and temperature against elapsed time.

* Compare the post-meal changes with baseline and with non-meal periods. Account for movement, time of day, and repeated observations.

One critical caveat: the BIG IDEAs study includes standardized breakfasts, but it does not establish a controlled glucose-only challenge for every participant. You can study changes following meals, but you cannot confidently attribute those changes to glucose alone.

If you specifically want to compare the effects of pure glucose, sucrose, and other carbohydrates, I did not identify a publicly available dataset in this search that clearly combines a controlled ingestion protocol, meal timestamps, and raw wrist PPG waveforms for that exact comparison.

Bottom line: BIG IDEAs Lab is the closest overall match to your requirements; PhysioCGM is a useful complementary dataset. Neither should be assumed to prove that glucose causes a particular waveform change.
