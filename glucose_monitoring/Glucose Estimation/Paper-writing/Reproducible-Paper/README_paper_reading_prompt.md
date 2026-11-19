
# Wearable-Based Glucose Estimation: Literature Review & Methodological Benchmark

## Research Goal

Investigate whether reported performance of non-invasive glucose estimation models using wearable sensor data reflects genuine generalization or is potentially inflated by:

- Subject leakage
- Random epoch-level train/test splitting
- Limited temporal context
- Weak or missing baseline comparisons
- Insufficient personalization evaluation
- Lack of external validation

The objective is to critically evaluate existing studies and develop a reproducible benchmarking framework for wearable-based glucose estimation.

---

## 1. Research Questions

- **RQ1:** How much does the evaluation strategy affect reported glucose estimation performance?
- **RQ2:** Do wearable-based glucose estimation models generalize to previously unseen individuals?
- **RQ3:** Does random epoch-level splitting produce overly optimistic performance?
- **RQ4:** Does incorporating temporal context improve glucose estimation?
- **RQ5:** Do complex ML models outperform simple population-level and personalized baselines?
- **RQ6:** How much data is required for personalization or calibration?
- **RQ7:** Which wearable modalities provide meaningful incremental predictive value?

---

## 2. Literature Reading Strategy

### Level 1: Screening (All 15 Papers)

Read the following sections:

- Abstract
- Introduction
- Dataset
- Methodology
- Results
- Limitations
- Conclusion

**Goal:** Identify the dataset, experimental setup, evaluation strategy, and potential methodological weaknesses.

Target time: 15–25 minutes per paper.

### Level 2: Deep Reading (5 Core Papers)

Read carefully:

- Introduction
- Related work
- Dataset and participant information
- Data preprocessing
- Feature engineering
- Train/test splitting
- Model architecture
- Hyperparameter tuning
- Baselines
- Evaluation metrics
- Results
- Discussion
- Limitations

**Goal:** Understand the complete experimental design and determine whether reproduction is feasible.

### Level 3: Technical Inspection (Selected Papers)

Inspect when necessary:

- Source code
- Supplementary materials
- Dataset documentation
- Signal processing implementation
- Feature engineering implementation
- Hyperparameter search
- Data splitting implementation
- Statistical analysis
- Participant-level results

**Goal:** Verify methodological details and reproduce selected experiments.

---

## 3. Paper Selection

### Tier 1: Core Papers

These are the first papers to investigate deeply.

- [ ] Paper 1: Development of Non-Invasive Continuous Glucose Prediction Models Using Multi-Modal Wearable Sensors in Free-Living Conditions (2025)
- [ ] Paper 2: PhysioCGM Multimodal Physiological Dataset (2025)
- [ ] Paper 3: Noninvasive Interstitial Glucose Estimation Using Wearables and Machine Learning (2026)
- [ ] Paper 4: Enhanced Blood Glucose Levels Prediction With a Smartwatch (2024)
- [ ] Paper 5: Non-invasive Blood Glucose Monitoring Using PPG Signals and Deep Learning/TinyML (2025)

### Tier 2: Methodological Comparison

- [ ] Paper 6: Deep Sparse Capsule Network for Non-Invasive Blood Glucose Estimation Using PPG (2025)
- [ ] Paper 7: Differential Absorbance and PPG-Based Glucose Measurement Using Spatiotemporal Multimodal LSTM (2025)
- [ ] Paper 8: EMD-Based Noninvasive Glucose Estimation Using PPG (2024)
- [ ] Paper 9: Wearable Sensor System and Data Analytic Framework for Glucose Prediction (2024)
- [ ] Paper 10: Elevated Glucose Assessment Using Wearable PPG and Machine Learning (2024)

### Tier 3: Additional Literature

- [ ] Paper 11: Green Light PPG-Based Non-Invasive Glucose Estimation (2026)
- [ ] Paper 12: Wearable Finger PPG-Based Blood Glucose Monitor (2025)
- [ ] Paper 13: Personalized Wearable ML Models for Hypoglycemia Detection (2025)
- [ ] Paper 14: Glucose Estimation Using Non-Invasive Wearable Device Data (2023)
- [ ] Paper 15: Systematic Review of AI-Based Wearable Glucose Prediction (2023)

> Paper selection and publication details must be verified before finalizing the literature review. Papers should be prioritized based on data availability, relevance, methodological transparency, and reproducibility.

---

## 4. Paper Reading Checklist

### A. Dataset

- [ ] Dataset name and source
- [ ] Number of participants
- [ ] Participant demographics
- [ ] Diabetes status
- [ ] Monitoring duration
- [ ] Sampling frequency
- [ ] Wearable device
- [ ] Glucose reference device
- [ ] Dataset publicly available?
- [ ] Code publicly available?

### B. Sensors and Modalities

- [ ] PPG/BVP
- [ ] Heart rate
- [ ] HRV
- [ ] EDA/GSR
- [ ] Skin temperature
- [ ] Accelerometer
- [ ] ECG
- [ ] Other modalities

Questions:

- Which modalities are used?
- Are modalities synchronized?
- Are modalities combined or evaluated independently?
- Are ablation experiments performed?

### C. Preprocessing

- [ ] Missing data handling
- [ ] Filtering
- [ ] Signal normalization
- [ ] Outlier removal
- [ ] Synchronization
- [ ] Resampling
- [ ] Windowing
- [ ] Feature extraction

Questions:

- Is preprocessing performed before or after data splitting?
- Could preprocessing introduce information leakage?
- Are normalization statistics calculated using training data only?
- Are windows overlapping?
- Can overlapping windows cross train/test boundaries?

### D. Evaluation Protocol

Record the exact splitting strategy.

- [ ] Random sample split
- [ ] Random epoch split
- [ ] Chronological split
- [ ] Subject-independent split
- [ ] Grouped cross-validation
- [ ] Leave-one-subject-out (LOSO)
- [ ] External validation

Questions:

- Are the same participants present in training and testing?
- Are adjacent or overlapping windows split between training and testing?
- Are test periods chronologically later than training periods?
- Are preprocessing and feature selection fitted only on training data?
- Is the evaluation performed on unseen participants?
- Is the evaluation performed on unseen time periods?

### E. Model

- [ ] Linear Regression
- [ ] Ridge Regression
- [ ] Random Forest
- [ ] XGBoost
- [ ] Gradient Boosting
- [ ] LSTM
- [ ] GRU
- [ ] CNN
- [ ] TCN
- [ ] Transformer
- [ ] Other

Questions:

- Why was this model selected?
- How were hyperparameters tuned?
- Was tuning performed using training data only?
- Was feature selection performed without access to test data?
- Is the model more complex than necessary?

### F. Baselines

- [ ] Global mean prediction
- [ ] Global median prediction
- [ ] Time-of-day baseline
- [ ] Personal mean prediction
- [ ] Personal median prediction
- [ ] Demographic baseline
- [ ] Persistence baseline (when task definition permits)
- [ ] Simple linear model

Questions:

- Are simple models included?
- Are personalized baselines included?
- Is calibration data separated from evaluation data?
- Does the proposed model demonstrate meaningful improvement over simple baselines?

### G. Temporal Context

- [ ] Single-point features
- [ ] Short window
- [ ] Long window
- [ ] Multiple window lengths
- [ ] Historical wearable features
- [ ] Glucose history used
- [ ] Temporal model

Questions:

- What is the window length?
- Is temporal information preserved?
- Are trends and changes captured?
- Is temporal context compared experimentally?

### H. Metrics

- [ ] RMSE
- [ ] MAE
- [ ] MARD
- [ ] R²
- [ ] Clarke Error Grid
- [ ] Parkes Error Grid
- [ ] Bland-Altman analysis
- [ ] Per-subject metrics

Questions:

- Are multiple metrics reported?
- Are metrics calculated across all epochs or participants?
- Are results averaged across participants?
- Are confidence intervals reported?
- Is error distribution analyzed?

### I. Personalization

- [ ] No personalization
- [ ] Subject-specific model
- [ ] Calibration
- [ ] Fine-tuning
- [ ] Personalized normalization
- [ ] Personalized baseline

Questions:

- How much calibration data is required?
- Does calibration improve performance?
- Is calibration data separate from test data?
- Does personalization improve performance consistently across subjects?

### J. Potential Methodological Issues

- [ ] Possible subject leakage
- [ ] Random epoch splitting
- [ ] Temporal leakage
- [ ] Overlapping window leakage
- [ ] Weak baselines
- [ ] Missing personalized baselines
- [ ] Limited temporal context
- [ ] Insufficient participants
- [ ] Missing external validation
- [ ] Missing per-subject evaluation
- [ ] Unclear preprocessing
- [ ] Possible overfitting
- [ ] Missing confidence intervals
- [ ] Unclear reproducibility

---

## 5. Literature Comparison Table

| Paper | Year | Participants | Sensors | Window | Split | Subject Overlap | Model | Baselines | Metrics | Personalization | External Validation | Code/Data | Potential Issues |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Paper 1 | | | | | | | | | | | | |
| Paper 2 | | | | | | | | | | | | |
| Paper 3 | | | | | | | | | | | | |
| Paper 4 | | | | | | | | | | | | |
| Paper 5 | | | | | | | | | | | | |
| Paper 6 | | | | | | | | | | | | |
| Paper 7 | | | | | | | | | | | | |
| Paper 8 | | | | | | | | | | | | |
| Paper 9 | | | | | | | | | | | | |
| Paper 10 | | | | | | | | | | | | |
| Paper 11 | | | | | | | | | | | | |
| Paper 12 | | | | | | | | | | | | |
| Paper 13 | | | | | | | | | | | | |
| Paper 14 | | | | | | | | | | | | |
| Paper 15 | | | | | | | | | | | | |

---

## 6. Benchmark Experimental Plan

### Experiment E0: Random Epoch-Level Split

Objective:

Reproduce a conventional evaluation protocol used in selected papers.

- Random epoch split
- Same participants potentially present in training and testing
- Record performance

Purpose:

Establish a reference performance level, not a claim of generalization.

### Experiment E1: Subject-Independent Evaluation

Objective:

Test generalization to unseen individuals.

Methods:

- GroupKFold
- Leave-One-Subject-Out (LOSO)

Rules:

- Participants in the test set must not appear in the training set.
- Preprocessing must be fitted using training data only.
- Feature selection must be fitted using training data only.

### Experiment E2: Chronological Within-Subject Evaluation

Objective:

Test future-period generalization for individuals whose historical data is available.

Method:

- Earlier data for training
- Later data for testing
- Chronological separation

### Experiment E3: Personal Calibration

Objective:

Investigate whether a limited amount of personal data improves estimation.

Evaluate:

- Zero calibration
- Short calibration
- Moderate calibration
- Longer calibration

Calibration data must not overlap with the evaluation period.

### Experiment E4: Temporal Context

Objective:

Investigate the effect of temporal information.

Compare:

- Short-window features
- Medium-window features
- Long-window features
- Multi-scale features
- Sequence models

### Experiment E5: Baseline Comparison

Objective:

Determine whether complex models outperform simple baselines.

Compare:

- Global mean
- Global median
- Time-of-day baseline
- Personal mean
- Personal median
- Linear Regression
- Ridge Regression
- Random Forest
- XGBoost
- Temporal models

### Experiment E6: Modality Ablation

Objective:

Measure the incremental predictive value of each wearable modality.

Evaluate:

- PPG/BVP only
- HR/HRV only
- EDA only
- Temperature only
- ACC only
- PPG + HR
- Multimodal combination

---

## 7. Leakage Prevention Rules

- Split participants or time periods before model fitting.
- Never use test data for feature selection.
- Never fit normalization statistics using test data.
- Never fit imputation models using test data.
- Never tune hyperparameters on test data.
- Ensure overlapping windows do not cross split boundaries.
- Prevent future information from entering the features.
- Separate calibration data from evaluation data.
- Report the exact splitting strategy.
- Report participant overlap explicitly.

---

## 8. Statistical Analysis

Report:

- Overall RMSE
- Overall MAE
- Participant-level RMSE
- Participant-level MAE
- Median participant performance
- Confidence intervals
- Paired comparison across evaluation protocols
- Performance variation across participants

Recommended:

- Bootstrap confidence intervals at participant level
- Paired comparisons between evaluation protocols
- Effect size reporting
- Error distribution analysis

Avoid treating thousands of epochs from a small number of participants as thousands of independent subjects.

---

## 9. Expected Research Contributions

1. A systematic methodological analysis of recent wearable-based glucose estimation studies.
2. An investigation of the impact of subject leakage and random epoch splitting.
3. A subject-independent benchmarking framework.
4. A chronological evaluation framework for within-subject generalization.
5. A comparison of complex models against simple baselines.
6. An investigation of temporal context.
7. An investigation of personalization and calibration.
8. A modality ablation study.
9. Reproducible experimental protocols and recommendations for future research.

---

## 10. Proposed Research Workflow

### Phase 1: Literature Review

- [ ] Screen 15 papers
- [ ] Deeply read 5 core papers
- [ ] Build comparison table
- [ ] Identify datasets
- [ ] Identify methodological weaknesses
- [ ] Finalize research questions

### Phase 2: Dataset Preparation

- [ ] Select dataset
- [ ] Verify data access
- [ ] Understand sensor signals
- [ ] Understand glucose reference measurements
- [ ] Check sampling frequency
- [ ] Check participant structure
- [ ] Check timestamps
- [ ] Check missing data

### Phase 3: Benchmark Implementation

- [ ] Implement preprocessing
- [ ] Implement feature extraction
- [ ] Implement baseline models
- [ ] Implement random split
- [ ] Implement subject-independent split
- [ ] Implement chronological split
- [ ] Implement calibration experiments
- [ ] Implement temporal models
- [ ] Implement modality ablation

### Phase 4: Analysis

- [ ] Compare evaluation protocols
- [ ] Compare model complexity
- [ ] Analyze per-subject performance
- [ ] Analyze temporal context
- [ ] Analyze personalization
- [ ] Analyze modality contribution
- [ ] Statistical analysis

### Phase 5: Writing

- [ ] Introduction
- [ ] Related Work
- [ ] Methodological Issues in Existing Studies
- [ ] Benchmark Framework
- [ ] Experimental Setup
- [ ] Results
- [ ] Discussion
- [ ] Limitations
- [ ] Recommendations
- [ ] Conclusion

---

## 11. Working Principle

The goal is not to prove that existing models are wrong.

The goal is to determine whether reported performance remains strong under more rigorous, reproducible, and realistic evaluation protocols.

**Research focus: Generalizability, reproducibility, temporal validity, and meaningful baselines.**
