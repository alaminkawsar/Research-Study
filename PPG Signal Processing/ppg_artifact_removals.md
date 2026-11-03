Worked for 42s

### Research analysis: Can we remove activity-related effects from continuous PPG signals?

Your research question is scientifically interesting and has connections to several established research areas, particularly physiological signal denoising, motion artifact removal, context-aware physiological modeling, sensor fusion, and counterfactual signal reconstruction.

I would slightly reformulate your research objective because there is an important distinction between removing noise from PPG and estimating what the PPG signal would have been under a different physical condition.

### 1\. First, understanding your research question

Suppose you collect continuous PPG data for 10 days from a wearable device.

During those 10 days, your PPG recordings contain signals from different physiological and environmental conditions:

| Context             | Possible effects on PPG                                                  |
| ------------------- | ------------------------------------------------------------------------ |
| Sleeping            | Changes in autonomic activity, heart rate, vascular tone and sleep stage |
| Sitting             | Relatively low movement, but posture and autonomic effects remain        |
| Standing            | Hydrostatic pressure and cardiovascular adjustments                      |
| Walking             | Movement artifacts and changes in cardiovascular demand                  |
| Running             | Significant movement and cardiovascular changes                          |
| Temperature changes | Peripheral vasoconstriction or vasodilation                              |
| Stress              | Changes in sympathetic activity and vascular tone                        |

Your assumption is that sleeping represents an ideal, relatively undisturbed PPG condition.

You then want to answer:

Can I estimate the PPG signal that would have been observed if the person had remained in a particular context, such as sitting, while removing the unwanted effects of other activities?

For example:

Conceptual example

OBSERVED PPG WHILE WALKING

![Frontiers | Photoplethysmogram Analysis and Applications: An Integrative Review](https://images.openai.com/static-rsc-4/yRsGl3YaRHk0AI31TaaxTEJFaORPH8U8iMff6t8TTCXiVmR3OmzxRMQ7qfmfg_VUpyUli-xdftgpNzN5vw7g3E_sCK2GnuJsQIkpxsR8AemcXSa2Rbjq8jPtNBV6c8wdQbvJsohkQ0a2cnQNLInkJqC_VXuZR1GGhnV0BXjf2V_tsojDmS5CKuIyodAeQ8vt?purpose=fullsize)

Contains physiological changes caused by walking, movement artifacts, and other influences.

Context-aware signal modeling

ESTIMATED PPG UNDER A SITTING REFERENCE CONDITION

![An Overview of the Sensors for Heart Rate Monitoring Used in Extramural Applications | MDPI](https://images.openai.com/static-rsc-4/Z7LWuHZo-bTrCk78g-GpA15wa4LvmribTy2h5in7BvVCwrGS7cb5n7OPxvK3sepZNoiREuFC_nwMKWUSexgA4O4WQQ53VpTc89t73niefjtm7gODcyoAhoq6tCaWdW7yo9CZaiAZJA2vsvIQuu6Cbf6JozcnFZVtL1y3mCMjzOlVDDqCX__q4gFA0sO1uSkk?purpose=fullsize)

An estimated counterfactual or standardized signal, not necessarily the person's actual sitting measurement.

There are actually two different research problems hidden in your question.

### Problem A: Remove measurement artifacts

You want to remove distortions caused by:

* Body movement.

* Sensor displacement.

* Skin contact pressure.

* Changes in sensor-to-skin coupling.

* Ambient light interference.

* Motion-induced changes in optical measurements.

This is generally called PPG motion artifact removal or PPG signal quality enhancement.

### Problem B: Remove context-dependent physiological variation

This is more interesting and closer to your research objective.

You want to distinguish between:

* Changes caused by the person's actual physiological state.

* Changes caused by physical activity or environmental conditions.

* Changes caused by measurement artifacts.

For example, walking increases heart rate because the cardiovascular system responds to exercise. That increase is not necessarily noise. It is a genuine physiological response.

If your goal is to estimate a person's resting or standardized cardiovascular state, you would want to remove or normalize the activity-associated component without destroying meaningful physiological information.

This is a much more difficult problem.

My interpretation: You are looking for a context-aware PPG normalization framework that estimates a standardized physiological signal using additional sensors such as accelerometer, temperature, respiration, and possibly ECG.

I would investigate this as a combination of signal processing and causal physiological modeling rather than ordinary denoising.

### 2\. The most important scientific issue: sleeping is not a perfect ground truth

I would challenge one assumption in your proposed methodology.

Sleeping can provide a useful low-motion reference condition, but it is not necessarily an ideal physiological baseline.

There are several reasons:

* Heart rate changes across sleep stages (NREM, REM).

* Autonomic nervous system activity changes during sleep.

* Peripheral vascular tone changes.

* Body temperature follows circadian patterns.

* Blood pressure and arterial properties change during sleep.

* Sleeping posture and sensor position affect the optical measurement.

One particularly relevant paper is:

Insights into vascular physiology from sleep photoplethysmography (2023).

It investigates how PPG morphology changes across sleep stages and demonstrates that deeper non-REM sleep is associated with changes in heart rate, pulse arrival time, and PPG-derived vascular characteristics.

[Read the paper on PubMed](https://pubmed.ncbi.nlm.nih.gov/37379483/?utm_source=chatgpt.com).

Another important paper is:

Determinants of photoplethysmography signal quality at the wrist (2025).

It identifies posture and sensor height relative to the heart as important determinants of wrist PPG quality. Signal quality was generally highest in the supine position and lower while sitting or standing.

[Read the research paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC12204546/?utm_source=chatgpt.com).

This suggests an important distinction:

Low-motion PPG is not necessarily equivalent to physiologically standardized PPG.

I recommend using sleep as one reference condition rather than treating every sleeping measurement as ground truth.

For example, you could establish a reference dataset using:

* Supine, awake, resting.

* Seated, awake, resting.

* Sleeping, separated by sleep stage if available.

* Standing, stationary.

These conditions would allow you to understand how much of the PPG variation is attributable to posture, activity, and physiological changes.

### 3\. Existing research areas directly related to your question

I found several research areas that are relevant. Some address only the motion-artifact problem, while others address physiological context.

Here is how I would classify them.

1\. PPG motion artifact removal

Very established research area

Accelerometer-assisted filtering and signal reconstruction.

2\. Multimodal physiological sensor fusion

Established research area

Combining PPG with temperature, ECG, respiration, EDA, and motion.

3\. Context-aware physiological modeling

Closely related to your objective

Learning how activity, posture, and environmental conditions influence PPG.

4\. Physiological signal normalization

Potentially very relevant

Standardizing physiological measurements across different contexts.

5\. Causal inference and counterfactual signal estimation

Particularly interesting research direction

Estimating what a person's PPG would have looked like under a different activity condition.

Let's examine the most important literature.

### 4\. Research papers: PPG artifact removal and reconstruction

These are some of the most relevant foundational papers for your work.

### Paper 1. Wearable Photoplethysmography for Cardiovascular Monitoring (2020)

Highly recommended starting point

Why it matters: This is a broad review of wearable PPG, including the physical sources of artifacts and techniques for removing them.

It discusses two major approaches:

* Single-channel PPG processing.

* PPG processing using an additional reference motion signal.

The second approach is particularly relevant to your idea. Accelerometers and gyroscopes can help identify motion-related components, while different PPG wavelengths can provide additional information.

It also makes an important point: sometimes rejecting low-quality segments is more reliable than attempting to reconstruct every corrupted waveform.

[Read the full paper – PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC7612541/?utm_source=chatgpt.com)

### Paper 2. Heart rate tracking in photoplethysmography signals affected by motion artifacts: a review (2021)

Why it matters: It examines the mathematical and computational techniques used to recover useful cardiovascular information from motion-corrupted PPG.

Methods discussed include:

* Adaptive filtering.

* Multiresolution signal decomposition.

* Spectral processing.

* Machine-learning-based heart-rate tracking.

The review identifies adaptive filtering and multiresolution decomposition as particularly useful approaches.

[Read the paper – Springer](https://link.springer.com/article/10.1186/s13634-020-00714-2?utm_source=chatgpt.com)

### Paper 3. Detection and Removal of Motion Artifacts in PPG Signals (2019; published in journal volume 2022)

Why it matters: This is directly relevant to developing a preprocessing pipeline for your 10-day recordings.

It investigates the detection and removal of motion artifacts in wearable PPG.

[Read the paper – Springer](https://link.springer.com/article/10.1007/s11036-019-01323-6?utm_source=chatgpt.com)

### Paper 4. Real-Time PPG Signal Conditioning with Long Short-Term Memory (LSTM) Network for Wearable Devices (2022)

Important for deep learning

This work investigates LSTM-based correction of PPG waveforms.

It evaluates the approach using PPG-DaLiA, which includes PPG, accelerometer, and ECG recordings collected during daily activities.

The general idea is particularly interesting for your research:

* Input a corrupted PPG signal.

* Provide additional motion information.

* Train a neural network to reconstruct a cleaner PPG waveform.

* Evaluate the resulting pulse-rate estimates against ECG.

[Read the paper – Sensors](https://www.mdpi.com/1424-8220/22/1/164?utm_source=chatgpt.com)

### Paper 5. Development of real-time motion artifact reduction algorithm for a wearable photoplethysmography (2007)

This is an interesting early engineering study.

It uses a three-axis accelerometer as a reference signal and an adaptive noise cancellation algorithm.

The reported distortion rate decreased from 52.34% to 3.53% in the tested frequency range of 1–2.5 Hz.

This is an example of using an independent sensor to estimate and cancel movement-associated interference.

[Read the paper – PubMed](https://pubmed.ncbi.nlm.nih.gov/18002262/?utm_source=chatgpt.com)

Important limitation: These papers primarily attempt to recover the underlying pulse signal or improve heart-rate estimation. They do not necessarily estimate the physiological PPG that would have been measured under a different activity condition.

That distinction is central to your proposed research.

### 5\. Research papers: Context, posture, and physiological effects

This research category is arguably even more relevant to your actual objective.

### Paper 6. An Experimental Study of the Effects of External Physiological Parameters on the Photoplethysmography Signals in the Context of Local Blood Pressure (2017)

This paper examines how external physiological factors influence PPG.

It considers:

* Vertical height differences.

* Body position.

* Hydrostatic pressure.

* Changes in local blood pressure.

* Autonomic nervous system responses.

* Respiration.

One important observation is that changing body position can produce changes in the PPG signal even without substantial physical movement.

[Read the full paper – PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC5375842/?utm_source=chatgpt.com)

This is particularly important because it demonstrates why simply removing accelerometer-correlated noise cannot solve your complete problem.

### Paper 7. Using the morphology of photoplethysmogram peaks to detect changes in posture (2006)

This study investigates how PPG waveform morphology changes when a person transitions from supine to standing.

It uses features such as:

* Normalized peak width.

* Instantaneous heart rate.

* Pulse amplitude.

It demonstrates that posture changes can be detected through PPG morphology.

[Read the paper – PubMed](https://pubmed.ncbi.nlm.nih.gov/16688391/?utm_source=chatgpt.com)

### Paper 8. Effect of posture on photoplethysmography signals from the posterior tibial artery in adults with and without type 2 diabetes

This is another useful study of posture-dependent PPG variation.

It compares supine, sitting, and standing measurements and reports differences in pulse amplitude, pulse intervals, and waveform morphology.

[Read the study](https://pmc.ncbi.nlm.nih.gov/articles/PMC12701066/?utm_source=chatgpt.com)

### Paper 9. Insights into vascular physiology from sleep photoplethysmography (2023)

I would specifically recommend this paper if you are planning to use sleeping PPG as a baseline.

It demonstrates that sleep stages themselves influence vascular characteristics extracted from PPG.

[Read the study](https://pubmed.ncbi.nlm.nih.gov/37379483/?utm_source=chatgpt.com)

### 6\. Can temperature and other physiological signals help make PPG cleaner?

Yes. This is one of the most promising aspects of your research.

However, different additional sensors provide different types of information. Some help identify measurement artifacts, while others help explain genuine physiological changes.

Here is how I would evaluate them.

![TDK Wearable Sensor Solutions | Sensor Solution Provider | TDK Product Center](https://images.openai.com/static-rsc-4/w6rcF0U4DV71MWyM4d-QS5d5GEgaIEsrfby4S5PJCiLLc1PBmaRdxBmCqREaz7jyZklsOezpQs1K423miF9imX-du_U2LTAdHDhr_njQxuC4YLd1KpZCnPh5k5nmvoCTJgM6hCe3YNa8WxJQntn6nffNaubbYvg8csWUb9UGFK9iXsFQS2BvQHeASnDHqaGw?purpose=fullsize)

1\. Accelerometer and gyroscope

Highest priority

Identify walking, running, hand movement, sensor displacement, and movement intensity.

Useful for motion artifact detection and adaptive filtering.

![Fitbit Sense (Carbon/Graphite)](https://images.openai.com/static-rsc-4/6kXd-2WI3d7f53GOiqGik0sa7PEf_Er4QfisK8Cwnh24ohYY1bg5XoQFhGD_6h16HGfgpSM9Xc6iguqIzKrYOn8aeUYpKyzhvhqlzuT0AJbxonRjf3mlQBZBBxotiX4qsy6nOAx7es2TarjQm208D42evfZmFZqTpsD2sY8un-zlzCuT4_3Nt1iitZkaj71c?purpose=fullsize)

2\. Skin temperature

High priority

Helps explain peripheral vasoconstriction, vasodilation, and changes in peripheral perfusion.

Particularly relevant to changes in PPG amplitude and morphology.

![ECG and Activity Sensor - EcgMove 4 - movisens GmbH](https://images.openai.com/static-rsc-4/nFcdCiTUolFO-sWn6OTn7lEKaDF_hiJTdx639JXoZ7-LhmIiJsfOL6Qsy7QVx1oTJycYPca4MyYR1I9NmzQNUuggL_uC0FLgEnaV274cpUfmtj-0bkxqMfBzY0FK20nfAqoqmlB_xXoELBAHaNlQs5cpBJmGYq8OLcU5kjJX5gpVHvo8wCDpoogfRgZVAIev?purpose=fullsize)

3\. ECG

High priority for validation

Provides an independent reference for cardiac electrical activity and heart rate.

Helps distinguish changes in actual cardiac timing from errors in PPG pulse detection.

![Wrist-Worn Sensor Validation for Heart Rate Variability and Electrodermal Activity Detection in a Stressful Driving Environment | MDPI](https://images.openai.com/static-rsc-4/RLO6w8_vWgLblJkucwQ7c08oFA4sTdDQfdI8le1A5iaexeGsgSC12rFZHxhqHonW3C65ebS0Jhi58Neq8d4BmcxYuX1VTyWMX7wazlX0QJ1Jy-KryP5hdgfrEWfuvCYzGCGpyhaPyfk8nCdqnfYB1yZataBNK-S1XJ8kvSXK5RjqdkRLqe_dmd3mz66bxPht?purpose=fullsize)

4\. Electrodermal activity (EDA) Helps identify sympathetic arousal, stress-related responses, and sweating.

Useful because physiological stress can influence peripheral circulation even without physical activity.

![NomadAir RIP Belt, Large
– Neurotronics Sensors](https://images.openai.com/static-rsc-4/rmGxJAdJj1zyTSLzWSDdzk-m1Fu-_bcGKQBhpQFVjBg3MGXzDkbSll97hvMYbAYEUSiy9yiSiYJpq5BIhZM6SKnCqdYs9iZYmZOzw01EoGlq6-tn7o-hm1rr1p8NqxDVp0Zt9_qZb-VvheAvcVqCusja_GTLhIoAx8MA2wodSH6i8cHZwwADMKBN4q33sLmX?purpose=fullsize)

5\. Respiration Helps model respiratory modulation of PPG and respiratory sinus arrhythmia.

Particularly useful when studying HRV and pulse-rate variability.

![Reliable wrist PPG monitoring by mitigating poor skin sensor contact | Scientific Reports](https://images.openai.com/static-rsc-4/jxflXsLhWWknol1J0utcwh8xftEuN9GcmLpDg3mMXs43z_e-_BDtZbVNgzRlQ94QIrKXMNk-sbYPgtu0Vzb--q5T3pUpo6Gs9S8VGaZPPpg2VQVOU7zYT43I2OFsZbcBSH2WznC5chsbAyYPyN5I_4-F2CsZ_tpyOPDFrMAfptJSnajurqKElnMqKh2phcKV?purpose=fullsize)

6\. Contact pressure Helps identify changes in sensor tightness and pressure on the skin.

Especially useful for wrist-worn PPG devices.

### Why temperature is particularly interesting

Consider two situations:

Situation A: You are sitting in a room at 24°C.

Situation B: You are sitting in a room at 15°C.

Your activity classification is identical: sitting.

However, cold exposure can cause peripheral vasoconstriction, changing blood flow near the skin surface. This can change PPG amplitude even if your activity level remains constant.

A relevant 2026 study, Differential sensitivity of impedance plethysmography and photoplethysmography sensors to temperature-induced peripheral vasoconstriction, experimentally investigated this relationship.

It found that cooling significantly reduced PPG amplitude, while the studied impedance plethysmography amplitude remained relatively stable.

[Read the study – Scientific Reports](https://www.nature.com/articles/s41598-026-36563-6?utm_source=chatgpt.com)

This supports your idea of using temperature as an explanatory variable in a PPG correction model.

However, temperature alone cannot tell you exactly how much of the PPG change is caused by temperature. It is also influenced by perfusion, sympathetic activity, sensor contact, and other variables.

### My recommended sensor combination

For your proposed research, I would prioritize the following:

| Sensor           | Main purpose                         | Priority  |
| ---------------- | ------------------------------------ | --------- |
| PPG              | Primary physiological signal         | Essential |
| Accelerometer    | Movement and motion artifact         | Essential |
| Gyroscope        | Orientation and rotational movement  | High      |
| Skin temperature | Peripheral vascular context          | High      |
| ECG              | Independent cardiac reference        | High      |
| EDA              | Sympathetic activity and stress      | Medium    |
| Respiration      | Respiratory physiological modulation | Medium    |
| Contact pressure | Sensor coupling variation            | Medium    |

You do not necessarily need to collect all these signals simultaneously. You can start with the first five.

### 7\. A particularly important research direction: Multimodal sensor fusion

This is where your proposed idea starts to become more interesting.

Instead of trying to clean PPG using only PPG, you can build a model that understands the physiological context in which the PPG was collected.

For example:

Proposed multimodal architecture

PPG

Waveform

IMU

Movement

Temperature

Thermal context

ECG / HR

Cardiac reference

Multimodal feature extraction

Temporal CNN / LSTM / Transformer

Context-aware physiological model

Activity + posture + thermal + cardiovascular context

Output A

Motion-corrected PPG

Output B

Standardized physiological PPG

The two outputs are important because they solve different problems.

* Output A attempts to reconstruct the signal without measurement artifacts.

* Output B estimates the physiological signal or features under a chosen reference condition.

I would not combine these two objectives into one black-box model initially.

### Relevant multimodal research

1\. Deep PPG: Large-Scale Heart Rate Estimation with Convolutional Neural Networks (2019)

This is particularly relevant because the authors use synchronized PPG and accelerometer signals as input to a deep learning model.

They introduce the PPG-DaLiA dataset and investigate time-frequency representations and CNN-based heart-rate estimation.

They report improvements over earlier approaches, including a 31% reduction in mean absolute error on PPG-DaLiA relative to their comparison baseline.

[Read the paper – PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC6679242/?utm_source=chatgpt.com)

2\. Machine Learning Applied to Reference Signal-Less Detection of Motion Artifacts in Photoplethysmographic Signals: A Review

This paper examines machine learning methods that detect motion-corrupted PPG without requiring a separate measured reference signal.

It is useful if you eventually want to develop a model that works with only the PPG data available from a wearable.

[Read the paper – PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC11598458/?utm_source=chatgpt.com)

3\. Human Activity Recognition: A Comparative Study to Assess the Contribution Level of Accelerometer, ECG, and PPG Signals

This research investigates combining accelerometer, ECG, and PPG features for recognizing daily activities.

It demonstrates that physiological signals can provide complementary information to inertial sensors.

[Read the paper – PubMed](https://pubmed.ncbi.nlm.nih.gov/34770303/?utm_source=chatgpt.com)

### 8\. An especially useful research resource: PPG datasets

Before developing your own algorithm, I recommend investigating publicly available multimodal datasets.

Some already contain almost exactly the signals you are interested in.

PPG-DaLiA

Best starting point

![Emotion Tracking: Mobile Electrodermal Activity (mEDA) and Facial Expressions | Department of Geography | UZH](https://images.openai.com/static-rsc-4/T_6OgvDGdLnz8VGigbvYWhP-dCa4weClXdMA63cyzyUxrWkc1kuDlpB2xGtLuyrKqmjKIh-KtxINPngPunBUMI730dStaIWySTj4EvSwZFeeYeAcK8z0mpPnbT5YPA5pA6MlH1M7h0SF2eKn_R58wJVC86mTqQZWMGakBbaUQNIJb7T4bxoWKnoxRhT1NhKo?purpose=fullsize)

Reiss et al., Deep PPG, 2019

It contains recordings from 15 participants performing eight daily activities, including sitting, walking, cycling, driving, and working.

Available signals include:

* Wrist PPG/BVP (64 Hz).

* Wrist accelerometer (32 Hz).

* Skin temperature (4 Hz).

* Electrodermal activity (4 Hz).

* Chest ECG (700 Hz).

* Chest respiration (700 Hz).

* Chest accelerometer (700 Hz).

The ECG provides an independent cardiac reference.

Access:

[Download PPG-DaLiA from UCI](https://archive.ics.uci.edu/dataset/495/ppg+dalia?utm_source=chatgpt.com)[Original dataset and publication information](https://kristofvl.github.io/usi/data_ppgdalia.html?utm_source=chatgpt.com)

WESAD

![Multi-Task Classification of Physical Activity and Acute Psychological Stress for Advanced Diabetes Treatment](https://images.openai.com/static-rsc-4/YBiAJ8yOLV8OUQEx84YI6R8yxGaOP4GJ9YBMrzbpjys7GBpbBuMSXhJXhni6fO6ZHzFTpmU7w9yO8n-s4rpHhB6gAmCN74APYWf7V_5cuXoMzdAPcdAik2Z10_wb8jHlYo8KRA18K42ALIHYDFBX7QFWhX6kQH5BDwnLiVTqV1qW2oLs-zG72idM5S_SkbOP?purpose=fullsize)

Wearable stress and affect detection dataset

Contains multimodal physiological measurements from 15 participants.

Signals include:

* BVP.

* ECG.

* Accelerometer.

* Temperature.

* EDA.

* Respiration.

* EMG.

Particularly useful for understanding how psychological stress can influence physiological signals independently of physical activity.

[WESAD dataset and resources](https://ubicomp.eti.uni-siegen.de/home/datasets/icmi18/?utm_source=chatgpt.com)

WildPPG

Interesting newer dataset

2024 preprint

A real-world dataset with continuous PPG recordings across outdoor and indoor activities.

It includes 16 participants, multiple wearable sensor locations, accelerometry, temperature, altitude, and synchronized ECG.

Particularly interesting because it addresses environmental and physiological variations under naturalistic conditions.

[Read WildPPG](https://arxiv.org/abs/2412.17540?utm_source=chatgpt.com)

GalaxyPPG

Newer multimodal resource

2025 dataset publication

A semi-naturalistic PPG dataset involving Galaxy Watch 5, Empatica E4, and Polar H10 measurements from 24 participants.

Includes PPG, ECG, acceleration, temperature, and activity/stress-related protocols.

Particularly interesting for comparing different wearable sensor configurations.

[Read the GalaxyPPG paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC12119839/?utm_source=chatgpt.com)

My recommendation: Start with PPG-DaLiA. It is particularly useful because you can investigate the relationship between PPG, activity, temperature, ECG, and respiration without collecting all the data yourself.

However, none of these datasets provides a true ground-truth waveform for what the same person would have produced at exactly the same moment under a different activity condition.

That requires a different experimental design.

### 9\. The research gap I think you should investigate: Context-conditioned PPG normalization

Now we reach the most important part of your question.

Most existing research focuses on:

* Removing motion artifacts.

* Improving heart-rate estimation.

* Detecting poor-quality PPG segments.

* Classifying activities using physiological signals.

Your objective goes a step further:

Can we estimate a person's standardized PPG signal by accounting for the physiological and environmental conditions under which it was collected?

I would formulate this as a context-conditioned signal reconstruction problem.

### 9.1 Mathematical formulation

Let:

* = observed PPG signal.

* = physical activity.

* = movement intensity.

* = skin temperature.

* = respiration.

* = ECG-derived cardiac information.

* = posture.

* = sensor contact pressure.

* = underlying cardiovascular and autonomic physiological state.

The observed PPG could be represented conceptually as:

P(t)=F(H(t),A(t),S(t),T(t),R(t),C(t))
+\\epsilon_{\\mathrm{motion}}(t)+\\epsilon(t)

This is a simplified model, not a claim that all these effects are additive or independent.

There are two components to estimate.

Component 1: Measurement artifact

\\hat P_{\\mathrm{clean}}(t)
=
P(t)-\\hat\\epsilon_{\\mathrm{motion}}(t)

This is the conventional motion artifact removal problem.

Component 2: Context-standardized physiology

Suppose you select sitting as your reference condition.

You want:

\\boxed{
\\hat P_{\\mathrm{sit}}(t)
=
E\[P(t)\\mid X(t),do(A=\\mathrm{sit})\]
}

Here, represents the available physiological and contextual information.

The notation comes from causal inference. It means estimating the outcome under an intervention that sets the activity to sitting, rather than simply selecting observations that happened while sitting.

This is a counterfactual estimation problem.

For example:

| Actual condition | Desired output                                |
| ---------------- | --------------------------------------------- |
| Walking          | Estimated sitting-reference PPG               |
| Running          | Estimated sitting-reference PPG               |
| Standing         | Estimated sitting-reference PPG               |
| Sleeping         | Estimated sitting-reference PPG               |
| Sitting          | Actual sitting PPG, after artifact correction |

There is a significant scientific limitation here.

You cannot uniquely recover the exact PPG waveform that would have occurred under sitting from one observed walking waveform.

Why?

Because the underlying cardiovascular state may also have changed. The person's heart rate, blood pressure, vascular tone, and autonomic state may be different.

You can estimate a conditional expected waveform or a standardized physiological representation, but you need additional assumptions and validation to call it a counterfactual reconstruction.

This distinction could itself become an important part of your research contribution.

### 9.2 Three possible modeling approaches

I would investigate these three approaches in order.

Approach A: Context-aware regression

Best initial experiment

Extract PPG features in fixed windows, for example 10–30 seconds.

Then model the relationship:

Y_{\\mathrm{PPG}} =
f(M,T,R,E,S,A)

Where can represent:

* Pulse amplitude.

* Pulse interval.

* Pulse width.

* Systolic rise time.

* Waveform area.

* Morphological features.

You can then estimate the expected features under your selected reference condition.

Possible models:

* Linear/multiple regression.

* Random Forest.

* XGBoost.

* Generalized additive models.

Advantage: Interpretability and easier validation.

Approach B: Multimodal deep learning

Best for waveform reconstruction

Instead of extracting features manually, provide synchronized sensor windows to a neural network.

\\hat P_{\\mathrm{reference}} =
f_\\theta(PPG,ACC,GYRO,TEMP,ECG,RESP)

Possible architectures:

* CNN for waveform patterns.

* LSTM/GRU for temporal dependencies.

* Transformer for longer-range context.

* Multimodal attention for sensor fusion.

You could have separate branches for PPG, movement, and physiological context, followed by a fusion layer.

Advantage: Can learn complex nonlinear relationships.

Limitation: Requires suitable reference targets and careful protection against learning an unrealistic reconstruction.

Approach C: Causal counterfactual modeling

Most interesting research direction

Build a model that distinguishes between:

* Activity-induced measurement artifacts.

* Activity-induced physiological responses.

* Other physiological and environmental influences.

Then estimate:

\\hat P_{A=\\mathrm{sit}}

while accounting for relevant physiological covariates.

Possible approaches include:

* Structural causal models.

* Causal representation learning.

* Conditional generative models.

* Counterfactual prediction.

* Domain adaptation.

Advantage: Closely matches your scientific question.

Limitation: Requires strong assumptions, a causal model, and preferably controlled experimental data.

### 9.3 An important methodological distinction

I would actually produce two standardized representations rather than one.

First: Motion-corrected PPG

Remove measurement artifacts while preserving actual physiological responses.

For example, if walking increases heart rate, the corrected signal should still reflect that increase.

Second: Resting-equivalent PPG features

Estimate what selected PPG features would look like under a standardized reference condition.

For example, estimate resting-equivalent pulse amplitude or waveform morphology.

These are fundamentally different outputs.

If you remove all walking-related physiological changes from the first output, you may accidentally remove genuine cardiovascular information.

### 10\. How I would design the experiment using your 10-day data

I would approach this in two phases.

### Phase 1: Investigate what your existing dataset can tell you

First, segment your continuous recordings into windows.

A reasonable starting point:

* PPG windows: 10–30 seconds.

* Accelerometer features: same synchronized windows.

* Temperature: corresponding measurements, accounting for its slower response.

* ECG: corresponding heart-rate and timing features, if available.

Then assign context labels.

| Context  | Description                                    |
| -------- | ---------------------------------------------- |
| Sleep    | Sleeping, ideally with sleep-stage information |
| Resting  | Awake, supine, minimal movement                |
| Sitting  | Awake, seated, minimal movement                |
| Standing | Stationary, upright                            |
| Walking  | Low-to-moderate activity                       |
| Running  | High activity                                  |

If you do not have reliable activity labels, you can initially derive them from accelerometer data, but validate the classification where possible.

Step 1: Establish the relationship between context and PPG.

Calculate:

* Mean pulse amplitude.

* Amplitude variability.

* Heart rate.

* Pulse interval variability.

* Systolic peak width.

* Rise time.

* Pulse area.

* Signal quality index.

Investigate whether these features change with activity, posture, and temperature.

Step 2: Investigate temperature effects independently.

For example:

PPG_{\\mathrm{amplitude}} =
f(T,\\text{activity},\\text{posture})

Check whether temperature explains additional variation after accounting for movement and posture.

Step 3: Investigate activity-related artifacts.

Measure the relationship between accelerometer features and PPG signal quality.

You can use:

* Pearson correlation.

* Cross-correlation.

* Frequency-domain coherence.

* Mutual information.

* Regression analysis.

Remember that correlation between accelerometer and PPG does not prove that the correlated component is an artifact. Both may respond to the same activity.

Step 4: Establish a baseline model.

Start with a regression model that predicts PPG features from contextual information.

For example:

\\widehat{Y}_{PPG} =
\\beta_0+\\beta_1T+\\beta_2M+
\\beta_3S+\\beta_4HR+\\beta_5R

Then investigate nonlinear models.

### Phase 2: Develop a context-normalization model

If the first phase demonstrates meaningful relationships, develop a model that estimates reference-condition PPG.

I would structure the experiment as follows:

Experimental workflow

* Data acquisition

    Collect synchronized PPG, accelerometer, gyroscope, temperature, ECG, and respiration.

* Signal synchronization

    Align sampling rates, timestamps, and physiological windows.

* Signal quality assessment

    Identify sensor displacements, poor contact, clipping, and corrupted segments.

* Activity and posture classification

    Identify sleeping, sitting, standing, walking, and running.

* Artifact correction

    Apply adaptive filtering or a learned reconstruction model.

* Physiological context modeling

    Estimate the influence of temperature, respiration, posture, and cardiovascular state.

* Reference-condition estimation

    Predict the expected PPG features under your selected reference condition.

* Independent validation

    Compare against controlled reference-condition measurements and ECG-derived references.

### A crucial improvement: Collect controlled reference measurements

If possible, conduct a small additional experiment.

For each participant:

* Record 10 minutes of supine resting PPG.

* Record 10 minutes of sitting PPG.

* Record 10 minutes of standing PPG.

* Record walking PPG.

* Repeat the conditions at different times.

* Record ECG, temperature, and accelerometer data simultaneously.

Allow sufficient recovery between activity conditions.

This provides repeated observations of the same person under different conditions.

You can then investigate within-person variation rather than relying entirely on comparisons between unrelated observations.

For a stronger study, repeat this protocol across several days and participants, and randomize the order of conditions where practical.

Why is this important?

Your existing 10-day observational data can reveal associations, but it cannot independently establish what the same physiological state would have looked like during another activity.

Controlled repeated measurements help address that identification problem.

### 11\. How should you evaluate whether your approach actually works?

This is particularly important if you intend to publish the work.

I recommend comparing four different models.

| Model    | Input                             | Objective                         |
| -------- | --------------------------------- | --------------------------------- |
| Baseline | PPG only                          | Conventional preprocessing        |
| Model A  | PPG + accelerometer               | Motion artifact correction        |
| Model B  | PPG + accelerometer + temperature | Motion and thermal context        |
| Model C  | PPG + all available sensors       | Multimodal context-aware modeling |

Evaluate them separately for the two outputs.

A. Artifact-removal evaluation

* Signal-to-noise ratio (SNR), where a valid reference is available.

* Signal quality index (SQI).

* PPG waveform reconstruction error.

* Heart-rate error against ECG.

* Pulse-rate variability error against ECG-derived HRV.

One caution: pulse-rate variability (PRV) is not always interchangeable with ECG-derived heart-rate variability (HRV), particularly during movement.

B. Context-normalization evaluation

* Difference between predicted and measured reference-condition features.

* Within-person prediction error.

* Consistency across repeated reference-condition sessions.

* Residual association with activity, posture, and temperature.

* Preservation of meaningful cardiovascular changes.

Do not use only reduced variance as evidence of improvement. A model can achieve lower variance simply by suppressing genuine physiological information.

A particularly strong experiment would test whether your model improves prediction of independently measured cardiovascular outcomes while preserving real physiological changes.

### 12\. What I believe could become your research contribution

I would avoid positioning your research as simply another PPG denoising algorithm. There is already substantial work on that.

Instead, I would investigate:

My recommended research direction

### Context-Aware Physiological Normalization of Continuous PPG Signals Using Multimodal Sensor Fusion

Central research question

Can continuous PPG recordings be transformed into a standardized physiological representation by separating motion-induced measurement artifacts from activity-, posture-, temperature-, and autonomic-dependent physiological variations?

Potential contributions

* Separate physical motion artifacts from genuine physiological changes.

* Quantify the influence of temperature, posture, and activity on PPG morphology.

* Develop a multimodal model for context-conditioned PPG reconstruction.

* Estimate standardized reference-condition PPG features.

* Evaluate whether normalization improves the consistency and reliability of cardiovascular measurements.

### Possible research paper titles

1\. Context-Aware Normalization of Continuous Photoplethysmography Signals Using Multimodal Physiological Sensor Fusion.

2\. Beyond Motion Artifact Removal: Physiological Context-Aware Reconstruction of Wearable PPG Signals.

3\. Counterfactual Photoplethysmography: Estimating Reference-State Cardiovascular Signals Under Varying Activity Conditions.

4\. Towards Activity-Invariant Photoplethysmography Using Multimodal Physiological Context Modeling.

I particularly like the second title because it distinguishes your proposed research from conventional motion-artifact removal.

### 13\. My recommended reading priority

If you only have time to study a few papers initially, read these in this order:

| Priority | Paper                                                       | What to learn                             |
| -------- | ----------------------------------------------------------- | ----------------------------------------- |
| 1        | Wearable Photoplethysmography for Cardiovascular Monitoring | Overall PPG research landscape            |
| 2        | Deep PPG (2019)                                             | Multimodal PPG and accelerometer modeling |
| 3        | External physiological parameters and PPG                   | Physical and physiological influences     |
| 4        | Determinants of PPG signal quality                          | Posture and sensor placement              |
| 5        | Insights into vascular physiology from sleep PPG            | Sleep as a physiological reference        |
| 6        | Reference signal-less motion artifact detection             | Machine learning and signal quality       |
| 7        | GalaxyPPG dataset                                           | Newer multimodal dataset research         |

Additional useful reviews include the [PPG Analysis and Applications integrative review](https://pubmed.ncbi.nlm.nih.gov/35300400/?utm_source=chatgpt.com) and the [motion artifact removal review](https://www.frontiersin.org/journals/electronics/articles/10.3389/felec.2021.685513/full?utm_source=chatgpt.com). These help establish the existing state of the art. PMC +3

### 14\. Final assessment

Here is my assessment of your original idea:

| Research question                                      | Assessment |
| ------------------------------------------------------ | ---------- |
| Can accelerometer remove movement artifacts from PPG?  |            |
| Can temperature help explain PPG variation?            |            |
| Can posture-dependent PPG changes be modeled?          |            |
| Can multiple sensors improve PPG reconstruction?       |            |
| Can sleeping PPG serve as a perfect baseline?          |            |
| Can we estimate sitting-equivalent PPG during walking? |            |
| Can we recover the exact counterfactual PPG waveform?  |            |

My strongest recommendation: Start with the distinction between artifact removal and physiological normalization. This is the foundation of your entire research.

You might discover that the best solution is not to reconstruct an entirely new PPG waveform. It may be more scientifically meaningful to produce a set of context-adjusted PPG features with uncertainty estimates.

That would preserve useful cardiovascular information while reducing unwanted contextual variation.

### 15\. Three questions that will determine the best research methodology

Before recommending a specific mathematical framework and model architecture, I would like to clarify three things about your actual data and objective.

1\. What device are you using to collect PPG?

Smartwatch / wrist wearable

Finger PPG sensor

Research-grade PPG device

Custom-built PPG sensor

Other / not sure

2\. Which signals do you currently have?

Select all that apply.

PPG

Accelerometer

Gyroscope

Skin temperature

ECG

EDA

Respiration

Blood pressure

Other

3\. What is your primary research objective?

Estimate sitting-equivalent PPG from every activity

Remove motion artifacts while preserving genuine physiological changes

Normalize PPG features to a standardized resting physiological state

Improve heart rate and HRV/PRV estimation

All of the above

Anything else about your data? (Optional)

Submit research details

With these answers, I can develop a much more concrete research proposal, including the mathematical formulation, causal assumptions, model architecture, preprocessing pipeline, experiments, and evaluation metrics for your 10-day continuous PPG research.
