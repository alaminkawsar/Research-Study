### Research review: Can we estimate a PPG baseline conditioned on activity?

Yes, there are well-established methods for parts of this problem. However, I found an important distinction in the literature:

* PPG baseline-wander correction: estimates and removes slow drift in the waveform.

* Motion-artifact detection and removal: identifies unreliable PPG segments or suppresses motion-related contamination.

* Activity-aware signal-quality assessment: evaluates whether PPG is suitable for extracting features under different movement levels.

* Activity-conditioned physiological baseline prediction: predicts what a participant's PPG features would have been under comparable conditions without a glucose challenge.

The first three are established research areas. The fourth is the closest match to your research idea, but it is a different problem, and I would not claim there is one universally accepted, established method for solving it specifically for glucose estimation.

I searched for research on PPG baseline correction, motion artifacts, wrist-worn PPG quality assessment, and glucose-estimation models. Below are the most relevant papers, with links and an assessment of how each could support your project.

### 1\. The most useful foundational paper

![Frontiers | Photoplethysmogram Analysis and Applications: An Integrative Review](https://images.openai.com/static-rsc-4/yRsGl3YaRHk0AI31TaaxTEJFaORPH8U8iMff6t8TTCXiVmR3OmzxRMQ7qfmfg_VUpyUli-xdftgpNzN5vw7g3E_sCK2GnuJsQIkpxsR8AemcXSa2Rbjq8jPtNBV6c8wdQbvJsohkQ0a2cnQNLInkJqC_VXuZR1GGhnV0BXjf2V_tsojDmS5CKuIyodAeQ8vt?purpose=fullsize)

### Photoplethysmogram Analysis and Applications: An Integrative Review

2022 · Review paper · Frontiers in Physiology

Authors: Integrative review of PPG generation, waveform analysis, noise, and signal processing.

Read the paper: [Full text and DOI](https://doi.org/10.3389/fphys.2021.808451?utm_source=chatgpt.com) · [PubMed record](https://pubmed.ncbi.nlm.nih.gov/35300400/?utm_source=chatgpt.com)

This is the first paper I would read because it organizes the main PPG signal-processing challenges. The review covers baseline wandering, motion artifacts, hypoperfusion, preprocessing, and signal-quality assessment. It also discusses baseline estimation and subtraction using filtering, interpolation, wavelet decomposition, and adaptive filtering. PMC +1

### What it means for your project

The paper establishes that PPG baseline variation is not just random sensor noise. It can reflect respiration, sympathetic nervous system activity, and thermoregulation, among other factors.

It also explains methods that estimate a slowly varying waveform baseline and subtract it from the measured signal.

However, this kind of baseline is the low-frequency component of the waveform. It is not the same as predicting a participant's expected PPG feature vector at a given activity level.

That distinction is essential for your research.

### 2\. Research papers on activity and motion

![Wrist Photoplethysmography Signal Quality Assessment for Reliable Heart Rate Estimate and Morphological Analysis](https://images.openai.com/static-rsc-4/AtWXGLLtGQtasvGfXeyngrRKCM8a-Bnc27sxr9mwbxD3xPewZ0B_Yw8mMtJQ_el7kk0paFUjXHZC-H7lBoqvQEH7U5WazqF466rEZ3wT6Q5mczEWu52p5hfQzx4JQdWM-fPuubYOl7q_NYLwKATn_VbBE6yY1Xz5iGRjPt1tqZiuXOWQSVMtWQYNjE8CgDYx?purpose=fullsize)

Paper 2 — Wrist PPG signal quality assessment

2022 · Sensors · DOI: 10.3390/s22155831

[Read the full paper](https://doi.org/10.3390/s22155831?utm_source=chatgpt.com)

The authors recorded wrist PPG from 31 participants over 24 hours and used accelerometer-derived activity levels to assess signal quality. They developed classifiers for identifying pulses suitable for heart-rate estimation and more detailed morphological analysis. PMC +1

Why it matters: this provides a concrete precedent for conditioning PPG quality assessment on activity. You could adopt similar activity strata to determine which recordings are reliable enough for your glucose-feature analysis.

Limitation: it identifies good-quality signals; it does not predict the counterfactual PPG baseline without glucose intake.

![Detection and Removal of Motion Artifacts in PPG Signals | Mobile Networks and Applications | Springer Nature Link](https://images.openai.com/static-rsc-4/wYfL0ygiruYecwB4iEDk9Cv_awzp-xVIUHSrojDtgwn-18vlLHQR4rs7CtmnivvBEC-M3yQR3qDCw4HSMc6D7iwfXLBzUH76Dkn0DaZz-moGtGyRV9ed74GkEsWeqarxUUvT2KCIR6VEHLKSCU2WwnjhS3sKasegPAuosJ_EHXwv9BJP9RrV47HKmt_wCnIz?purpose=fullsize)

Paper 3 — Detection and Removal of Motion Artifacts in PPG Signals

Pollreisz & TaheriNejad · Published online 2019; journal issue 2022

[Read the open-access paper](https://doi.org/10.1007/s11036-019-01323-6?utm_source=chatgpt.com)

This review compares techniques that detect or suppress motion artifacts, including statistical methods, signal decomposition, synthetic motion references, and accelerometer-assisted adaptive filtering. Springer Nature Link +1

Why it matters: it helps you choose a preprocessing pipeline and understand when accelerometer data can support artifact reduction.

Limitation: motion artifacts and genuine physiological responses can overlap in frequency and morphology. Removing one does not guarantee that the remaining waveform is glucose-specific.

![Wearable Photoplethysmographic Sensors—Past and Present | MDPI](https://images.openai.com/static-rsc-4/rBBrn_kDpm5YVIHWLixT4MDqua0J9WODapL77E9Sa7X0stu_ijltOyUd9_R06kZ6KN8iJ6ztXSjFC36anEtXYLYmOZoGLc2emOrNDnjQa7WHqa0-MenkxfYu_YAhEjcPcO-txLCtmKRxIrgg6kVpRI1gBHjIKqjJBQ_nvCb_71svxFm4h9ypQgn-4gYrrC5y?purpose=fullsize)

Paper 4 — Artifacts in wearable photoplethysmographs during daily life motions and their reduction with least mean square based active noise cancellation method

Han & Kim · Computers in Biology and Medicine, 2012

[Read the paper](https://doi.org/10.1016/j.compbiomed.2011.12.005?utm_source=chatgpt.com)

This study analyzes motion-related distortion during activities such as typing, wrist movements, walking, and running. It uses accelerometer data as a reference for adaptive noise cancellation. PubMed +1

Why it matters: it supports the idea of using a synchronized motion reference to account for part of the movement-related signal contamination.

Limitation: the method targets motion artifacts, not the full set of physiological changes associated with activity.

![Frontiers | Motion Artifact Removal Techniques for Wearable EEG and PPG Sensor Systems](https://images.openai.com/static-rsc-4/bFY6REUEg6UYpbrYY23tPKMeVRFXmjrkrojypvOKVuDtUDeu3XHX96tM4WKYeslkdYbMC3Hf9X5l_Ya9e_hH_0mGFns6jMdh3CaeR5yYE_AMcxMge4odjP-y2fWZlWzLC3iK4t1bcEXKgAMVMajumOMo4fy0ArC6dV0nYw8D9gMh6OZaerql9qtMVRGWu8Ap?purpose=fullsize)

Paper 5 — Machine Learning Applied to Reference Signal-Less Detection of Motion Artifacts in Photoplethysmographic Signals: A Review

Sensors, 2024 · DOI: 10.3390/s24227193

[Read the full review](https://doi.org/10.3390/s24227193?utm_source=chatgpt.com)

This review examines machine-learning methods that classify PPG segments as reliable or unreliable without requiring an external motion-reference signal. PMC

Why it matters: if your wrist sensor does not expose accelerometer data, this is a useful starting point for signal-quality screening.

Limitation: a quality classifier cannot establish whether a clean signal change was caused by glucose, autonomic responses, or temperature.

### 3\. The closest glucose-specific research

This is the part of the literature that is especially relevant to your proposed approach.

### Paper 6 — Using Machine learning to predict blood glucose level based on Photoplethysmography

Jian, Lo, Chuang & Kuo · Measurement, September 2025

DOI: 10.1016/j.measurement.2025.117421

[Read the paper](https://doi.org/10.1016/j.measurement.2025.117421?utm_source=chatgpt.com)

This study uses PPG signal-quality assessment, baseline correction, and time- and frequency-domain features for glucose prediction. Its reported results include a random-forest model with and MARD of 5.15% on a modified composite dataset. ScienceDirect +1

Why it matters: it is directly related to PPG glucose estimation and demonstrates that baseline correction has already been considered in this research area.

Important caution: these reported results do not establish that activity-conditioned counterfactual baseline prediction works, nor do they establish clinical accuracy for your proposed method. The dataset construction and independent validation conditions need to be examined before comparing reported numbers.

### Paper 7 — Improving non-invasive glucose estimation with monthly calibrated photoplethysmography and implicit HbA1c

Research article · 2025

[Read the full paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC12738703/?utm_source=chatgpt.com)

This study investigates personalization through a pretest measurement, paired PPG inputs, and models informed by an inferred HbA1c-related feature. Its method uses a personal pretest as a reference for subsequent PPG-based estimates. PubMed Central (PMC) +1

Why it matters: it is conceptually closer to your idea than ordinary waveform detrending because it investigates how a person's reference measurement can help a model adapt its glucose predictions.

Important distinction: the pretest is used for personalized calibration; it is not specifically an activity-conditioned estimate of what PPG would have looked like without glucose intake.

### Paper 8 — Improving the Accuracy of Continuous Blood Glucose Measurement Using Personalized Calibration and Machine Learning

2023 · Research article

[Read the full paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC10416969/?utm_source=chatgpt.com)

This work explores personalized glucose prediction using multisensor information, including activity, posture, heart rate, skin temperature, and acceleration-related features. PubMed Central (PMC)

Why it matters: it supports the general strategy of incorporating contextual variables into glucose-estimation models rather than expecting PPG alone to explain every change.

Limitation: incorporating context into a prediction model is not equivalent to removing the effects of context from the PPG representation.

### 4\. Which established method is best for your baseline model?

Here is how I would rank the methods for your specific research objective.

Method A — Activity-stratified baseline estimation

Best first experiment

Build a reference feature distribution from the same participant's pre-intake recordings, separated into activity and posture categories.

For example, estimate the participant's baseline feature mean while standing and compare it with post-intake PPG recorded while standing.

\\widehat z_{0,i,a}=
\\frac{1}{N_{i,a}}\\sum_j z_{i,a,j}

This is simple, interpretable, and establishes whether personalized subtraction helps at all. It is a proposed application of standard statistical methods, not a uniquely established glucose-specific algorithm.

Method B — Conditional regression

Predict baseline features using activity, posture, heart rate, temperature, and other available covariates.

\\widehat z_{0,i,t}=g_\\phi(a_{i,t},c_{i,t},b_i)

Start with linear regression or generalized additive models, then compare random forest or gradient boosting.

This is a natural next step when a single average baseline cannot represent different physiological conditions.

Method C — Learned conditional baseline

Use a neural network to predict the expected PPG feature representation from contextual variables and personal baseline data.

This is more flexible but needs substantially more representative data and careful validation. It should be attempted only after simpler baselines have been tested.

Method D — Waveform baseline-wander correction

Use high-pass filtering, moving-average detrending, spline interpolation, or wavelet-based methods to estimate and remove slow baseline drift.

This is appropriate for cleaning the PPG waveform before extracting features. It should be considered a separate preprocessing stage rather than your main glucose-baseline model. PMC +1

### 5\. A critical issue: matching activity is not enough

Suppose you have two recordings:

* Pre-intake PPG: standing, heart rate 70 bpm, skin temperature 32°C.

* Post-intake PPG: standing, heart rate 85 bpm, skin temperature 34°C.

Both recordings belong to the same activity category, but their physiological conditions differ.

You have two reasonable options:

* Adjust for measured covariates: include heart rate, temperature and other available contextual information in your baseline model.

* Use matched-condition comparisons: compare only observations with sufficiently similar contextual measurements, and quantify how much data this excludes.

However, be careful about treating heart rate and temperature as nuisance variables. A glucose challenge might itself affect autonomic activity or peripheral perfusion. Adjusting for these variables could remove part of a genuine glucose-associated response. I would therefore compare models with and without these adjustments.

### 6\. My recommended literature-based experiment

I would combine the established techniques into the following experimental pipeline.

Raw wrist PPG + accelerometer

Signal preprocessing and quality assessment

Baseline-wander correction, artifact flags and reliable-window selection

Shared feature extraction

Morphology, amplitude, timing and frequency-domain features

Personal baseline

Pre-intake recordings

Current observation

Post-intake recording

Activity-conditioned residual

r_t=z_t-\\widehat z_{0,t}

Compare glucose estimators

Raw features vs. personal baseline subtraction vs. conditional baseline subtraction

The key comparison is whether the residual-based estimator improves on a raw-feature model on held-out participants. Evaluate both absolute glucose estimation and change from baseline. Use participant-level train/test separation and matched control sessions so that the model cannot succeed simply by learning the passage of time.

### 7\. The papers I would prioritize reading

If you have limited time, read these in this order:

* [Photoplethysmogram Analysis and Applications: An Integrative Review (2022)](https://doi.org/10.3389/fphys.2021.808451?utm_source=chatgpt.com) — foundational signal-processing concepts.

* [Wrist Photoplethysmography Signal Quality Assessment (2022)](https://doi.org/10.3390/s22155831?utm_source=chatgpt.com) — activity-stratified wrist PPG quality assessment.

* [Detection and Removal of Motion Artifacts in PPG Signals](https://doi.org/10.1007/s11036-019-01323-6?utm_source=chatgpt.com) — methods for motion contamination.

* [Using Machine Learning to Predict Blood Glucose Level Based on PPG (2025)](https://doi.org/10.1016/j.measurement.2025.117421?utm_source=chatgpt.com) — glucose-specific signal processing.

* [Improving Non-Invasive Glucose Estimation with Monthly Calibrated PPG](https://pmc.ncbi.nlm.nih.gov/articles/PMC12738703/?utm_source=chatgpt.com) — personalized reference measurements and paired PPG modeling.

My conclusion: the literature provides established building blocks, but I have not identified a validated, standard method that specifically predicts the same participant's counterfactual PPG feature vector under the same activity, without a glucose challenge, and then uses its residual for glucose estimation.

That gap could be a meaningful research contribution. I would position your work as an activity- and context-conditioned personalized baseline correction method for PPG-based glucose estimation, and experimentally establish whether it provides an advantage over ordinary PPG preprocessing and existing personalized calibration approaches.
