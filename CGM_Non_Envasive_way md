# Wearable Sensor + CGM Datasets

A curated collection of publicly available datasets that combine continuous glucose monitoring (CGM) with wearable or physiological sensor data.

The goal of this repository is to support research into whether physiological signals from non-invasive wearable sensors can be used to:

- Estimate current blood glucose
- Detect glucose rising/falling trends
- Predict future glucose levels
- Detect impending glucose spikes
- Detect possible hypoglycemia/hyperglycemia
- Understand individual physiological responses to meals and glucose excursions

«Core research question:
Can physiological signals available from wearable devices provide enough information to understand or predict blood glucose behavior without directly measuring glucose?»

---

Dataset Overview

Dataset| Participants| CGM / Glucose| Wearable / Physiological Signals| Food / Context| Access| Priority
PhysioCGM| 10 T1D| Dexcom G6, ~5 min| ECG, PPG/BVP, EDA, skin temperature, accelerometer, HR, respiration| Limited| Open| ⭐⭐⭐⭐⭐
BIG IDEAs| 16| Dexcom G6, ~5 min| PPG/BVP, EDA, skin temperature, accelerometer, HR, IBI| Food + nutrition| Open| ⭐⭐⭐⭐⭐
HUPA-UCM| 25 T1D| FreeStyle Libre 2| HR, activity, steps, calories, sleep| Meals, carbs, insulin| Open| ⭐⭐⭐⭐
D1NAMO| 29 total| Glucose/CGM| ECG, respiration, accelerometer, HR/activity| Food pictures + insulin| Open| ⭐⭐⭐⭐
OhioT1DM| 12 T1D| CGM| Fitness-band physiological data| Meals, insulin, exercise| Controlled| ⭐⭐⭐⭐
T1D-UOM| 16| CGM| Activity, sleep| Nutrition + insulin| Open| ⭐⭐⭐
BrisT1D| 24| Diabetes-device glucose data| Smartwatch data| Longitudinal context| Mixed| ⭐⭐⭐

---

1. PhysioCGM

Best overall match for raw physiological-signal → CGM research.

PhysioCGM contains synchronized physiological signals and CGM data collected from people with type 1 diabetes in free-living conditions.

Participants

- 10 participants with T1D
- Up to approximately 17 days of recording per participant
- Real-world/free-living conditions

Sensors

Zephyr BioHarness

- ECG — 250 Hz
- Respiration — 25 Hz
- 3-axis accelerometer
- Heart rate
- Breathing rate
- Posture
- Activity
- ECG quality/confidence

Empatica E4

- PPG/BVP
- Heart rate
- EDA
- Skin temperature
- 3-axis accelerometer

Ground truth

- Dexcom G6 CGM
- Approximately 5-minute glucose measurements

Why it is valuable

This dataset is particularly suitable for experiments such as:

ECG
PPG
EDA
Temperature
Respiration
Accelerometer
       │
       ▼
   ML Model
       │
       ▼
CGM glucose

Potential tasks:

- Glucose estimation
- Glucose trend classification
- Glucose forecasting
- Spike detection
- Personalized glucose modeling

Resources

- "PhysioCGM paper" (https://www.nature.com/articles/s41597-025-06090-6)
- "PhysioCGM GitHub repository" (https://github.com/PSI-TAMU/PhysioCGM)

---

2. BIG IDEAs Lab Glycemic Variability & Wearable Device Dataset

One of the most useful datasets for wearable + CGM + nutrition research.

The dataset contains approximately 8–10 days of monitoring per participant using a Dexcom G6 and Empatica E4.

Participants

- 16 participants
- Approximately 8–10 days each

Wearable signals

- PPG/BVP
- Heart rate
- IBI
- EDA
- Skin temperature
- 3-axis accelerometer

Glucose

- Dexcom G6
- Approximately 5-minute resolution

Context

The dataset also contains food information, including:

- Food
- Amount
- Calories
- Carbohydrates
- Fiber
- Sugar
- Protein
- Fat

Example research pipeline

Food
 │
 ▼
Physiological response
 │
 ├── HR
 ├── HRV
 ├── EDA
 ├── PPG
 ├── Temperature
 └── Activity
 │
 ▼
CGM response

This makes BIG IDEAs particularly useful for investigating:

«How does an individual's physiological response to food relate to their subsequent glucose excursion?»

Resources

- "BIG IDEAs dataset on PhysioNet" (https://www.physionet.org/content/big-ideas-glycemic-wearable/1.1.3/)

---

3. HUPA-UCM Diabetes Dataset

HUPA-UCM combines CGM data with wearable activity and lifestyle information.

Participants

- 25 people with T1D
- Approximately 14+ days of data

Data

- FreeStyle Libre 2 CGM
- Heart rate
- Steps
- Calories
- Sleep duration
- Sleep quality
- Insulin
- Meals
- Carbohydrate intake

Example

Sleep
  +
Activity
  +
Heart rate
  +
Carbohydrates
  +
Insulin
       │
       ▼
     CGM
       │
       ▼
Glucose response

This dataset is especially useful for lifestyle and behavioral glucose modeling.

Resource

- "HUPA-UCM dataset" (https://data.mendeley.com/datasets/3hbcscwz44/1)

---

4. D1NAMO

D1NAMO is particularly interesting for studying the relationship between cardiac physiology and glucose.

Participants

- 20 healthy participants
- 9 participants with T1D

Physiological signals

- ECG
- Respiration
- Accelerometer
- Heart rate/activity

Other data

- Glucose
- Food photographs
- Insulin information

Potential research question

ECG ─────────┐
             │
Respiration ─┤
             ├──► Glucose prediction
Activity ────┘

It is especially useful for investigating whether changes in cardiac/autonomic physiology correlate with glucose excursions.

Resource

- "D1NAMO on Zenodo" (https://zenodo.org/records/5651217)

---

5. OhioT1DM

OhioT1DM is one of the better-known datasets for glucose prediction research.

Participants

- 12 people with T1D
- Approximately 8 weeks per participant

Data

- CGM
- Insulin pump
- Physiological fitness-band data
- Meals
- Exercise
- Other self-reported events

Potential applications

- Glucose forecasting
- Insulin-aware glucose prediction
- Meal-aware glucose modeling
- Time-series prediction
- Personalized models

Access

Access is currently more restricted than PhysioCGM or BIG IDEAs and requires a data-use process.

Resource

- "OhioT1DM dataset information" (https://webpages.charlotte.edu/rbunescu/ohiot1dm.html)

---

6. T1D-UOM

T1D-UOM is a longitudinal dataset from the University of Manchester.

Participants

- 16 people

Data

- Glucose
- Activity
- Sleep
- Insulin
- Nutrition
- Demographics

Best suited for

- Lifestyle/glucose modeling
- Longitudinal analysis
- Sleep vs glucose
- Activity vs glucose
- Nutrition vs glucose

Resource

- "Manchester CS Coordinated Diabetes Study" (https://github.com/sharpic/ManchesterCSCoordinatedDiabetesStudy)

---

7. BrisT1D

BrisT1D provides a relatively long longitudinal view of people living with T1D.

Participants

- 24 young adults with T1D
- Approximately 6 months of monitoring

Data

- Diabetes-device data
- Glucose
- Smartwatch data
- Longitudinal behavioral/contextual information

Some raw-device data have additional access restrictions.

Best suited for

- Long-term glucose modeling
- Personalized models
- Behavioral modeling
- Smartwatch + diabetes-device research

Resource

- "BrisT1D dataset — University of Bristol" (https://data.bris.ac.uk/data/dataset/33z5jc8fa6tob21ptrugzqog08)

---

8. Glucose-ML

"Glucose-ML" (https://github.com/Augmented-Health-Lab/Glucose-ML-Project) is not simply another dataset. It is particularly interesting because it aims to provide a standardized framework for working with multiple glucose datasets.

The project includes datasets such as:

AZT1D
BIG IDEAs
BrisT1D
CGMacros
D1NAMO
HUPA-UCM
Park 2025
PhysioCGM
Shanghai
T1D-UOM
UCH T1DM
OhioT1DM
...

This could significantly reduce the effort required to create a multi-dataset glucose research corpus.

---

Proposed Unified Dataset Schema

For machine-learning experiments, the datasets should ideally be transformed into a common schema.

A possible structure:

timestamp

# Physiological signals
ecg
ppg
hr
hrv
eda
skin_temperature
respiration
accelerometer_x
accelerometer_y
accelerometer_z

# Activity
steps
activity
sleep

# Nutrition
meal
carbohydrates
sugar
protein
fat
calories

# Diabetes context
insulin

# Ground truth
cgm_glucose

# Derived labels
glucose_delta_5m
glucose_delta_15m
glucose_delta_30m
glucose_delta_60m

glucose_trend
glucose_spike
hypoglycemia
hyperglycemia

Not every dataset contains every field. The unified representation should therefore allow missing values.

---

Recommended Research Tasks

Task 1 — Glucose State Classification

Instead of predicting an exact glucose number:

Wearable signals
       │
       ▼
┌──────────────────┐
│ Low              │
│ Normal           │
│ High             │
└──────────────────┘

This may be easier and potentially more robust than exact glucose estimation.

---

Task 2 — Glucose Trend Detection

Predict whether glucose is:

↗ Rapidly rising
↗ Rising
→ Stable
↘ Falling
↘ Rapidly falling

This is particularly relevant for wearable applications.

---

Task 3 — Future Glucose Prediction

Use historical wearable data to predict future glucose:

t-30       t-15        t       t+15       t+30
 │           │          │         │          │
 └───────────┴──────────┘         │          │
       wearable signals            │          │
                                  ▼
                          predicted glucose

For example:

Input:
30 minutes of wearable data

Target:
CGM glucose 15 minutes in the future

---

Task 4 — Glucose Spike Prediction

This is perhaps the most interesting task for the original research question.

Instead of asking:

«"What is my glucose?"»

ask:

«"Is my glucose about to spike?"»

For example:

Input:
30 minutes of wearable signals

Label:

1 → glucose increases > X mg/dL
    during the following 30 minutes

0 → otherwise

The model becomes:

ECG
PPG
EDA
HR/HRV
Temperature
Respiration
Activity
       │
       ▼
   ML model
       │
       ▼
"Glucose spike
 likely soon"

---

Task 5 — Glucose Excursion Prediction

Predict the magnitude of the upcoming change:

ΔGlucose =
Glucose(t + 30 min) - Glucose(t)

The model therefore answers:

«"How much is glucose likely to change over the next 30 minutes?"»

rather than attempting to estimate the absolute glucose concentration.

---

Recommended Experimental Strategy

A sensible progression would be:

                    ┌─────────────────┐
                    │  PhysioCGM      │
                    └────────┬────────┘
                             │
                    Model development
                             │
                             ▼
                    ┌─────────────────┐
                    │   BIG IDEAs     │
                    └────────┬────────┘
                             │
                    Independent testing
                             │
                             ▼
                    ┌─────────────────┐
                    │   HUPA-UCM      │
                    └────────┬────────┘
                             │
                     Lifestyle model
                             │
                             ▼
                    ┌─────────────────┐
                    │    D1NAMO       │
                    └─────────────────┘
                       ECG validation

The most important comparison is:

Population model

People A + B + C + D + ...
              ↓
          One model
              ↓
       New person

versus:

Personalized model

Person A
  ↓
Learn individual physiology
  ↓
Predict Person A glucose

The second approach may be substantially more promising because physiological responses differ considerably between individuals.

---

Important Limitations

These datasets should not be interpreted as proving that wearable signals can measure glucose non-invasively.

CGM remains the ground-truth/reference signal.

The research question is instead:

«Do non-glucose physiological signals contain enough information to infer or predict glucose dynamics?»

Important limitations include:

- Small participant numbers in many datasets
- Large individual differences
- T1D-heavy populations
- Different CGM devices
- Different wearable devices
- Different sampling rates
- Missing data
- Sensor synchronization problems
- CGM measurement lag relative to blood glucose
- Confounding from meals, exercise, stress and sleep
- Potential subject leakage during ML evaluation

Therefore, subject-independent validation is essential.

---

Priority Recommendation

If starting this project from scratch:

Priority| Dataset| Primary reason
🥇| PhysioCGM| Richest raw physiological signals + CGM
🥈| BIG IDEAs| Wearable + CGM + detailed nutrition
🥉| HUPA-UCM| More participants + lifestyle data
4| D1NAMO| ECG/respiration-focused research
5| OhioT1DM| Longitudinal glucose prediction
6| BrisT1D| Long-term smartwatch/diabetes data
7| T1D-UOM| Lifestyle and longitudinal analysis

---

Key Research Hypothesis

The central hypothesis for this project can be stated as:

«Changes in glucose concentration may produce measurable changes in cardiovascular, autonomic, electrodermal, respiratory, thermal and behavioral signals that can be detected by wearable sensors.»

Rather than attempting to replace CGM immediately, the first goal should be to determine whether these signals can reliably predict:

1. Glucose direction
2. Rate of glucose change
3. Upcoming glucose excursions
4. Magnitude of glucose excursions
5. Potential hypo/hyperglycemic events

Only after demonstrating these relationships should exact glucose estimation be attempted.

---

Useful Starting Points

- PhysioCGM: https://github.com/PSI-TAMU/PhysioCGM
- BIG IDEAs: https://www.physionet.org/content/big-ideas-glycemic-wearable/1.1.3/
- HUPA-UCM: https://data.mendeley.com/datasets/3hbcscwz44/1
- D1NAMO: https://zenodo.org/records/5651217
- OhioT1DM: https://webpages.charlotte.edu/rbunescu/ohiot1dm.html
- T1D-UOM: https://github.com/sharpic/ManchesterCSCoordinatedDiabetesStudy
- BrisT1D: https://data.bris.ac.uk/data/dataset/33z5jc8fa6tob21ptrugzqog08
- Glucose-ML: https://github.com/Augmented-Health-Lab/Glucose-ML-Project
