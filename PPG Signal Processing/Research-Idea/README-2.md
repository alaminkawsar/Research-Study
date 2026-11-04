# Transition-Dependent Photoplethysmographic Recovery Dynamics
## A Multimodal Study of Physiological State Changes in Wearable PPG

**Research manuscript draft / study protocol and analysis blueprint**  
**Version:** 0.1 — 4 November 2026  
**Status:** Conceptual draft. Experimental results, participant details, ethics approval, and final statistical findings are intentionally left as placeholders.

> **Important:** This document is a research-paper scaffold, not a report of completed experiments. Do not present the proposed hypotheses, sample sizes, protocol, or expected outcomes as observed findings. Replace all bracketed fields with verified study information. The novelty assessment is provisional and requires a systematic literature search before submission.

---

## Proposed manuscript metadata

- **Working title:** Transition-Dependent Photoplethysmographic Recovery Dynamics: A Multimodal Study of Physiological State Changes in Daily Life
- **Alternative title:** Does Activity History Matter? Comparative Analysis of PPG Stabilization Following Different Activity-to-Rest Transitions
- **Short title:** PPG Recovery After State Transitions
- **Article type:** Original research article (prospective observational / controlled repeated-measures study)
- **Keywords:** photoplethysmography; PPG; transition dynamics; recovery kinetics; activity history; posture; wearable sensors; accelerometry; ECG; autonomic regulation; signal quality; multimodal monitoring

## Abstract (structured draft; complete after experiments)

**Background:** Wearable photoplethysmography (PPG) is increasingly used to monitor cardiovascular activity in daily life. PPG morphology and amplitude are affected by posture, exercise, respiration, peripheral vascular tone, and sensor–skin interaction. Many wearable analyses classify or interpret data according to the current activity or posture, potentially overlooking the influence of the physiological state immediately preceding the current state.

**Objective:** This study will investigate whether PPG recovery dynamics depend on transition history when participants arrive at a common destination state, with particular emphasis on transitions ending in sitting. It will compare the temporal response of PPG features following different activity-to-sitting transitions and assess whether multimodal signals help distinguish physiological recovery from measurement artifact.

**Methods:** [Describe participants, devices, sampling rates, protocol, transition definitions, signal processing, features, and statistical methods.] PPG-derived features will be tracked from transition onset into the destination-state period. Accelerometry will characterize movement and posture; ECG will provide an independent reference for cardiac timing; skin temperature and respiration will be included where available. Recovery will be characterized using prespecified trajectory and stabilization metrics.

**Results:** [Insert only after analysis: participant flow, number of valid transitions, feature trajectories, between-transition contrasts, uncertainty intervals, and sensitivity analyses.]

**Conclusion:** [State conclusions supported by the data only.] The study is designed to test whether transition history provides information about PPG dynamics beyond the destination activity label and whether multimodal context improves interpretation of those dynamics.

---

# 1. Introduction

## 1.1 Background

Photoplethysmography is an optical technique that measures changes in light absorption or reflection associated with pulsatile blood-volume changes in tissue. Wearable PPG enables continuous, non-invasive monitoring, but the measured waveform is not determined by cardiac activity alone. It is also influenced by vascular tone, local perfusion, temperature, respiration, posture, movement, sensor pressure, optical coupling, and device characteristics.

These influences create a central interpretation problem for long-duration recordings: two signal segments collected during the same nominal activity may not be physiologically equivalent. A person who has been sitting for twenty minutes may have a different cardiovascular and peripheral vascular state from a person who has just sat down after walking, standing, or waking from sleep.

Most activity-aware processing approaches use the current activity or movement level to describe context. This is useful, but it may omit *transition history*: the sequence of states and physiological demands immediately before the current state. The cardiovascular system does not necessarily change instantaneously when posture or activity changes. Heart rate, cardiac output, vascular tone, and peripheral blood-volume distribution can evolve over seconds or minutes. Consequently, PPG features may exhibit transient trajectories before reaching a relatively stable destination-state pattern.

This motivates the concept of **transition-dependent PPG recovery dynamics**: the time course by which PPG-derived features evolve after a transition, conditional on both the destination state and the preceding state.

## 1.2 Scientific motivation

Consider three transitions that all end in sitting:

- Standing → sitting
- Walking → sitting
- Sleeping → sitting (waking followed by sitting)

The destination posture is nominally the same, but the preceding conditions differ. Walking may involve elevated heart rate, ventilation, metabolic demand, and thermoregulatory changes. Standing involves orthostatic loading and redistribution of blood volume. Waking and sitting after sleep involve a change in arousal state, posture, and potentially sleep-stage-related autonomic conditions.

It is therefore plausible that PPG amplitude, pulse timing, pulse shape, and their variability follow different trajectories after these transitions. However, the direction and duration of these differences should not be assumed in advance. They may vary across individuals, transition intensity, temperature, sleep stage, hydration, time of day, and sensor fit.

## 1.3 Research problem

A current-state label such as `sitting` may not fully characterize the physiological context of a PPG segment. This study asks whether information about the preceding state improves the description and prediction of PPG dynamics during the period after entering a common destination state.

The study must distinguish two mechanisms:

1. **Physiological dynamics:** genuine changes in heart rate, vascular tone, perfusion, respiration, and blood-volume distribution.
2. **Measurement dynamics:** movement artifact, sensor displacement, contact-pressure change, ambient-light interference, and changes in optical coupling.

These mechanisms may occur together. A PPG feature that changes after a transition cannot automatically be interpreted as a physiological response.

## 1.4 Research aim

To characterize and compare PPG feature trajectories and stabilization times following different activity/posture transitions that end in a common destination state, and to evaluate whether multimodal physiological and motion signals improve interpretation of those trajectories.

## 1.5 Specific objectives

1. Detect and label selected activity/posture transitions using synchronized wearable sensors and protocol annotations.
2. Quantify PPG feature trajectories before and after transition onset.
3. Compare feature-specific recovery dynamics across transitions with the same destination state.
4. Estimate whether transition history explains variation beyond current posture/activity, participant identity, and measured covariates.
5. Separate, as far as the available signals permit, physiological dynamics from signal-quality degradation and sensor-motion artifacts.
6. Evaluate between-person variability and the repeatability of transition-specific response patterns.
7. Determine whether transition-aware context improves downstream PPG interpretation compared with current-state-only context.

## 1.6 Research questions

- **RQ1:** Do PPG-derived features exhibit measurable transient dynamics after a transition into a common destination state?
- **RQ2:** Do these trajectories differ according to the preceding state when the destination state is held constant?
- **RQ3:** Are transition-specific differences observed in amplitude, pulse morphology, pulse interval/heart rate, or other feature families?
- **RQ4:** How much of the observed variation is associated with movement and signal quality, and how much remains associated with physiological context?
- **RQ5:** Does adding transition history improve prediction of PPG feature trajectories or stabilization time compared with using the current activity/posture alone?
- **RQ6:** Are the effects consistent within an individual across repeated trials, and how much do they vary between individuals?

## 1.7 Hypotheses

These hypotheses are proposed for preregistration and must be refined after a pilot study.

- **H1:** PPG feature trajectories following transitions into sitting differ according to the preceding state.
- **H2:** Transition history explains additional variance in post-transition PPG features beyond destination posture and participant-specific baseline differences.
- **H3:** Different PPG feature families have different response and stabilization times; pulse-rate-related features need not recover at the same rate as amplitude or morphology features.
- **H4:** A multimodal model incorporating accelerometry, ECG-derived cardiac timing, respiration, and skin temperature will explain post-transition PPG variation better than a model using activity labels alone.
- **H5:** Transition-specific recovery characteristics show meaningful between-person variability, supporting personalized rather than exclusively population-level estimates.

**Do not assume** that walking → sitting must have the longest recovery or that sleeping → sitting must have the shortest. Those are empirical questions.

---

# 2. Related Work and Research Positioning

The following papers are particularly relevant. They establish that PPG changes with exercise recovery, posture, respiration, and daily-life context. They do not, individually, establish the exact comparative question proposed here.

## 2.1 PPG-derived vascular recovery after exercise

**Charlton et al. / Measuring Vascular Recovery Rate After Exercise**  
Open access: https://pmc.ncbi.nlm.nih.gov/articles/PMC7612924/  
PubMed: https://pubmed.ncbi.nlm.nih.gov/35782201/

This study developed PPG-derived vascular recovery rate indices using the VORTAL dataset, which included 39 healthy subjects measured before and after exercise. Thirty-one indices were extracted from PPG pulse shape, alongside heart rate. The authors found that the rate of return toward baseline differed across indices and participants. Features derived from pulse timing and the second derivative were identified as candidates for further study.

**Relevance:** This is a key precedent for treating post-exercise PPG as a time-varying recovery process rather than a static rest measurement. It also supports analyzing multiple PPG features rather than heart rate alone.

**Difference from the proposed study:** The proposed work focuses on comparing multiple transition histories that arrive at a common destination state, not only recovery after exercise.

## 2.2 PPG morphology during postural change

**Linder et al. (2006), “Using the Morphology of Photoplethysmogram Peaks to Detect Changes in Posture.”**  
Journal of Clinical Monitoring and Computing, 20, 151–158.  
DOI: https://doi.org/10.1007/s10877-006-9015-2  
PubMed: https://pubmed.ncbi.nlm.nih.gov/16688391/

The authors monitored 11 subjects during supine-to-standing transitions using finger and ear pulse oximeters. PPG peak width, instantaneous heart rate, and amplitude changed around the postural event. The study showed that PPG morphology can detect a physiological response to orthostatic stress.

**Relevance:** Supports the premise that PPG morphology responds dynamically to posture changes and that different features may respond at different times.

**Difference:** It focused on detecting a postural transition, rather than comparing post-transition recovery trajectories across different preceding activities with a common destination state.

## 2.3 Cardiovascular response time to active postural changes

**Pauls et al. (2018), “Time Course Response of the Heart and Circulatory System to Active Postural Changes.”**  
Journal of Biomechanical Engineering, 140(3).  
DOI: https://doi.org/10.1115/1.4038429  
PubMed: https://pubmed.ncbi.nlm.nih.gov/29131882/

This study examined 50 healthy subjects during supine-standing-supine transitions using impedance cardiography. It quantified early response and settling times for heart rate and cardiac output. Reported settling times were approximately 50–58 seconds under the tested conditions.

**Relevance:** Provides physiological precedent for measurable cardiovascular settling after posture changes.

**Difference:** The measured outcomes were heart rate and cardiac output, not wearable PPG morphology, and the transition protocol was not the proposed set of activity-to-sitting transitions. The reported times should not be transferred directly to PPG.

## 2.4 PPG reactivity to posture and respiration

**Nawar et al. (2025), “Elucidating the Reactivity of Reflectance-Based Core-Body Photoplethysmogram to Posture and Respiratory Changes.”**  
IEEE Sensors Journal, 25(18), 35447–35459.  
DOI: https://doi.org/10.1109/JSEN.2025.3596522  
Open access: https://pmc.ncbi.nlm.nih.gov/articles/PMC12478533/  
PubMed: https://pubmed.ncbi.nlm.nih.gov/41031393/

In 24 healthy participants, the study assessed core-body PPG signal quality and amplitude reactivity across posture and breathing protocols, comparing sternum/back PPG with finger PPG. It reported that PPG quality and amplitude reactivity depend on sensing location, wavelength, posture, and breathing pattern. The study also highlights that peripheral and core-body PPG responses can differ.

**Relevance:** Strong support for considering posture, respiration, sensor location, and signal quality when interpreting transition-related PPG changes.

**Difference:** The study evaluated responses to protocol segments and posture/breathing changes; it did not directly test the proposed transition-history comparison across multiple preceding activity states.

## 2.5 PPG acquired during daily life

**Charlton et al. (2020), “Acquiring Wearable Photoplethysmography Data in Daily Life: The PPG Diary Pilot Study.”**  
Engineering Proceedings, 2(1), 80.  
DOI: https://doi.org/10.3390/ecsa-7-08233  
Open access: https://pmc.ncbi.nlm.nih.gov/articles/PMC7610437/  
PubMed: https://pubmed.ncbi.nlm.nih.gov/33778803/

This pilot study collected wrist-worn PPG from one participant over four weeks with a diary of daily activities. It illustrated both the feasibility and practical challenges of long-term PPG acquisition, including signal availability and quality. It included illustrative PPG changes during exercise recovery and sleep onset.

**Relevance:** Supports the importance of long-duration PPG and contextual annotations, while emphasizing that high-quality signal availability can be limited in daily life.

**Difference:** It was a single-participant feasibility study and did not systematically compare transition-specific stabilization times.

## 2.6 PPG heart-rate recovery measurement validity

**“Accuracy of Heart-Rate-Recovery Parameters Assessed From a Wrist-Worn Photoplethysmography Monitor (Polar Unite)” (2023).**  
International Journal of Sports Physiology and Performance.  
DOI: https://doi.org/10.1123/ijspp.2023-0120  
PubMed: https://pubmed.ncbi.nlm.nih.gov/37917971/

This study compared wrist PPG heart-rate recovery with ECG during treadmill and cycling exercise/recovery sequences in 30 participants. It highlights that PPG-derived heart-rate recovery estimates can be affected by measurement accuracy during transitions.

**Relevance:** Supports the need for ECG as an independent reference for cardiac timing and the need to avoid treating PPG-derived heart-rate recovery as error-free.

## 2.7 Summary of the research gap

The cited literature establishes several building blocks:

- PPG-derived features can show measurable recovery after exercise.
- PPG morphology changes during postural transitions.
- Cardiovascular variables have finite response and settling times after posture changes.
- PPG signal quality and amplitude are affected by posture and breathing.
- Wearable PPG can be collected during daily life, but signal quality and contextual annotation are challenging.
- PPG heart-rate recovery can differ in accuracy from ECG during exercise/recovery transitions.

**Provisional gap statement:** In the literature identified for this draft, there is limited direct evidence from a common protocol comparing PPG feature trajectories and stabilization times across multiple distinct preceding activity/posture states while holding the destination state constant, and evaluating the incremental value of transition history and multimodal context.

This is a *provisional* gap, not a claim that no such study exists. A systematic review and database search (PubMed, IEEE Xplore, Scopus, Web of Science, Google Scholar) is required before making a definitive novelty claim.

---

# 3. Conceptual Framework

## 3.1 Core concept: transition history as context

![Conceptual framework](figures/conceptual_framework.svg)

Represent a transition as:

\[
T = (S_{\mathrm{previous}}, S_{\mathrm{destination}}, t_0)
\]

where:

- \(S_{\mathrm{previous}}\) is the preceding activity/posture/physiological state;
- \(S_{\mathrm{destination}}\) is the state entered after the transition;
- \(t_0\) is the transition onset time.

For the primary comparison, the destination state is sitting, while the preceding state varies.

The PPG feature vector at time \(t\) after transition onset can be represented as:

\[
\mathbf{y}(t) =
f(T, \mathbf{z}(t), \mathbf{q}(t), \mathbf{u}, \epsilon(t))
\]

where:

- \(\mathbf{y}(t)\): PPG-derived feature vector;
- \(T\): transition history;
- \(\mathbf{z}(t)\): measured physiological context (e.g., ECG-derived HR, respiration, temperature);
- \(\mathbf{q}(t)\): signal-quality and sensor-motion indicators;
- \(\mathbf{u}\): participant-specific characteristics;
- \(\epsilon(t)\): residual variation and measurement noise.

The purpose is not to claim that all causes can be uniquely separated. It is to test whether transition history contains reproducible explanatory or predictive information after measured context is considered.

## 3.2 Proposed transition taxonomy

### Primary transitions ending in sitting

| ID | Transition | Main considerations |
|---|---|---|
| T1 | Standing → sitting | Postural blood-volume redistribution and baroreflex response |
| T2 | Walking → sitting | Exercise cessation, HR/respiratory recovery, movement and temperature |
| T3 | Sleeping → sitting | Awakening, sleep-stage context, posture change and arousal |
| T4 | Lying supine → sitting | Postural redistribution without preceding locomotion |
| T5 | Running → sitting | Higher-intensity exercise recovery; include only if safe and protocolized |
| T6 | Stair climbing → sitting | Variable exertion, lower-limb activity and recovery |
| T7 | Prolonged sitting → standing → sitting | Repeated postural challenge; useful for repeatability |

### Additional transitions for a broader study

- Sitting → standing
- Sitting → walking
- Standing → walking
- Walking → standing
- Supine → standing
- Standing → supine
- Lying → sitting after a controlled rest period

**Recommendation:** Do not attempt to study every transition in the first paper. Use a small, well-controlled primary set and treat the others as secondary or exploratory transitions.

## 3.3 Why a common destination matters

Holding the destination state constant reduces one source of variation. If all analysed periods end in standardized sitting, then differences in the post-transition trajectories can be evaluated in relation to the preceding condition.

However, “sitting” itself must be operationally standardized:

- chair and back support;
- feet position;
- arm/hand position;
- sensor-bearing arm position;
- speaking restriction;
- room temperature;
- time allowed in the destination state;
- whether the participant is instructed to remain still.

Sitting after walking is not necessarily equivalent to sitting after sleep in terms of autonomic state, body temperature, hydration, or recent activity. These are not merely nuisance variables; they are part of the scientific question and should be measured where possible.

---

# 4. Methods (Proposed)

## 4.1 Study design

A repeated-measures multimodal study is recommended. Each participant completes multiple transition conditions on more than one occasion, where practical. Repeated trials allow within-person comparisons and reduce confounding by stable individual characteristics.

A strong design can combine two complementary components:

1. **Controlled transition protocol:** standardized and repeated transitions, with known event times and controlled destination conditions. This is best for testing the primary hypothesis.
2. **Free-living longitudinal observation:** continuous wearable recordings (e.g., 10 days) to evaluate whether the transition-aware approach remains useful in daily life. This is best for ecological validity and event discovery.

These components should not be treated as interchangeable. Controlled trials support clearer comparisons; free-living data better represent real-world conditions but have less controlled transition timing and context.

## 4.2 Participants and sample size

- Target population: [define, e.g., adults without known cardiovascular disease for an initial healthy-volunteer study].
- Planned sample size: [determine using pilot data and a power analysis].
- Inclusion criteria: [specify].
- Exclusion criteria: [specify].
- Recruitment: [specify].
- Ethics approval: [committee, approval number, date].
- Consent: written informed consent before data collection.

A pilot with approximately 10–15 participants may help estimate feasibility, event yield, within-person variability, and missingness. It should not be presented as a definitive sample-size justification. A subsequent sample size should be based on the primary endpoint, expected effect size, repeated-measures correlation, and participant-level clustering.

## 4.3 Sensor modalities

| Modality | Priority | Purpose | Important limitation |
|---|---|---|---|
| PPG | Essential | Primary waveform and feature trajectories | Sensitive to perfusion, movement, contact, temperature and device design |
| Accelerometer (3-axis) | Essential | Detect movement, posture transitions, activity intensity | Movement is not a direct measure of physiological recovery |
| Gyroscope | Useful | Improve orientation and movement characterization | May be unavailable in some wearables |
| ECG | Strongly recommended | Independent cardiac timing / HR reference | Does not validate PPG amplitude or vascular morphology |
| Skin temperature | Recommended | Peripheral thermal context | Skin temperature is not core temperature and may lag |
| Respiration | Recommended | Ventilatory context and respiratory modulation | Method and placement affect reliability |
| EDA | Optional | Arousal/sympathetic context | Not a direct measure of vascular recovery |
| Contact pressure | Valuable if available | Identify coupling/contact changes | Often unavailable in commercial wearables |

Record device model, sensor location, wavelength, sampling frequency, resolution, firmware, strap/patch tightness, and synchronization method.

### Synchronization

All streams should share a common time base or have a documented synchronization procedure. Quantify clock drift and alignment error. Transition timing should be recorded independently where possible (protocol event marker, observer annotation, or synchronized event button).

## 4.4 Transition protocol

### Primary protocol

For each participant, collect repeated trials for:

- standing → sitting;
- walking → sitting;
- lying/supine → sitting;
- sleeping → sitting, if the study includes a natural overnight/waking arm.

For each transition:

1. Record a pre-transition baseline long enough to characterize the preceding state.
2. Mark transition onset and offset.
3. Ask the participant to enter the standardized sitting posture.
4. Continue recording for a prespecified recovery observation period (e.g., 5–10 minutes for the initial protocol; refine using pilot data).
5. Record protocol deviations, speaking, arm movement, coughing, sensor adjustment, and other interruptions.
6. Repeat the transition on separate trials with adequate washout/rest, where safe and feasible.

### Specific considerations

**Standing → sitting:** Standardize duration of standing and preceding activity. This is a postural transition, not necessarily a strong exertional challenge.

**Walking → sitting:** Standardize walking speed, duration, and (if possible) workload. Record intensity using pace, perceived exertion, or heart-rate response. A self-paced walk introduces substantial heterogeneity.

**Sleeping → sitting:** Treat this as a distinct naturalistic condition. Do not forcibly wake participants solely to create a transition unless an ethics-approved sleep protocol justifies it. Record sleep duration, wake time, sleep stage if available, and time from awakening to sitting. Sleep-to-sit is not directly comparable to controlled daytime transitions without accounting for circadian time and sleep state.

**Running/stairs → sitting:** Consider these as secondary conditions. Use safe, standardized workloads and appropriate screening.

### Randomization and order

Randomize the order of daytime controlled transition conditions when possible. Sleep-related observations cannot generally be randomized in the same way. Provide adequate rest between trials to limit carry-over effects.

## 4.5 Transition event definition

Define the event time \(t_0\) before analysis. A possible operational definition is:

- onset: first sustained accelerometer/gyroscope evidence of the transition;
- offset: participant reaches the destination posture and movement falls below a predefined threshold;
- recovery window: begins at the transition offset or at a prespecified event-relative time.

Do not use PPG itself as the only transition detector if PPG is also the primary outcome, because this can create circularity. Use accelerometry, protocol markers, and independent annotation.

## 4.6 PPG preprocessing and quality control

A reproducible pipeline should include:

1. Raw data integrity checks and timestamp validation.
2. Sensor dropout and saturation detection.
3. Baseline wander and appropriate band-limited filtering, with filter settings justified for the sensor and target features.
4. Beat detection and pulse segmentation.
5. Pulse-quality assessment at beat and window levels.
6. Detection of abrupt waveform discontinuities and likely sensor displacement.
7. Motion/context annotation using accelerometry.
8. Retention of raw data and all intermediate quality flags.

Do not automatically discard all high-motion intervals. The transition itself may contain relevant physiology. Instead, report results for:
- all detected transitions;
- transitions passing a prespecified quality threshold;
- sensitivity analyses under stricter motion and quality thresholds.

Avoid filtering choices that distort pulse morphology or create artificial settling behavior. Report filter type, order, cutoff frequencies, phase handling, resampling, and edge handling.

## 4.7 Candidate PPG features

Use a limited, physiologically motivated feature set for the primary analysis. Additional features can be exploratory.

### Primary candidate features

- Pulse rate / inter-beat interval (IBI), compared with ECG-derived timing.
- AC pulse amplitude, with normalization method documented.
- Pulse amplitude relative to DC level, if supported by the sensor.
- Pulse width at a specified fraction of pulse amplitude.
- Rise time and fall time.
- Pulse area / pulse integral.
- Beat-to-beat variability of selected morphology features.

### Secondary / exploratory features

- First- and second-derivative morphology indices.
- Systolic upstroke time.
- Dicrotic notch / diastolic feature measures, only when reliably identifiable.
- Pulse shape similarity to an individual baseline template.
- Respiratory modulation of PPG amplitude and interval.
- PPG signal-quality indices.

Morphology features can be sensitive to sampling frequency, filtering, sensor site, wavelength, and pulse detection quality. Define them precisely and report the proportion of beats for which each feature is valid.

## 4.8 Defining “stabilization” and “recovery time”

This is a central methodological decision. Avoid defining recovery merely as “the signal looks stable.”

A candidate operational definition:

1. Establish a destination-state reference distribution from a standardized, sufficiently long sitting baseline collected under comparable conditions.
2. For each feature, calculate a robust reference centre (e.g., median) and scale (e.g., median absolute deviation).
3. Define a tolerance band around the reference centre using a prespecified threshold.
4. Define stabilization time as the first time the feature enters the tolerance band and remains within it for a prespecified persistence duration.
5. If the feature never enters the band within the observation period, mark it as right-censored rather than assigning an arbitrary maximum recovery time.

For feature \(j\), let \(m_j\) be the reference median and \(s_j\) a robust scale estimate. A standardized deviation may be:

\[
d_j(t) = \frac{|x_j(t)-m_j|}{s_j}
\]

A feature-specific stabilization event may be defined as \(d_j(t) \leq \tau_j\) continuously for at least \(L_j\) seconds, where \(\tau_j\) and \(L_j\) are chosen before the main analysis and justified in the protocol.

**Important:** A single stable PPG feature does not prove that the entire cardiovascular system has recovered. Use the term *PPG-feature stabilization time* rather than claiming whole-body physiological recovery.

### Complementary dynamic measures

- Initial response magnitude: difference between pre-transition and early post-transition values.
- Maximum deviation from destination reference.
- Time to peak response.
- Early slope / rate of change.
- Recovery slope.
- Area under the deviation-from-reference curve.
- Time to 50% return toward reference, if a monotonic recovery model is reasonable.
- Proportion of time within the reference tolerance band.

A feature may not return monotonically. In that case, avoid forcing a single exponential model; use nonparametric trajectories or flexible splines.

## 4.9 Multimodal contextual variables

Potential covariates:

- accelerometer magnitude and activity intensity;
- body orientation and posture;
- ECG-derived heart rate and inter-beat intervals;
- respiration rate and respiratory phase, where available;
- skin temperature and its rate of change;
- time of day and time since awakening;
- duration and intensity of preceding activity;
- sleep duration/stage (for sleep transitions);
- ambient temperature;
- sensor contact/pressure and signal-quality measures;
- participant-level variables relevant to the protocol.

The analysis should distinguish:
- variables used to define the transition;
- variables used as explanatory covariates;
- variables used for signal-quality exclusion or sensitivity analysis.

Some variables may lie on the physiological pathway between the preceding activity and PPG response. Adjusting for them changes the estimand. Therefore, report both a minimally adjusted model (estimating the overall association of transition history) and a mechanistic/context-adjusted model (examining whether the association remains after measured physiology is included).

---

# 5. Statistical Analysis Plan

## 5.1 Primary endpoint

Recommended primary endpoint:

**Within-participant difference in PPG-feature stabilization time across prespecified transitions ending in sitting.**

Select one primary PPG feature or a clearly defined primary feature family before the main study. If multiple co-primary features are used, account for multiplicity.

## 5.2 Secondary endpoints

- Transition-specific initial response magnitude.
- Difference in early and late trajectory slopes.
- Area under the absolute deviation curve.
- Feature-specific time to 50% recovery, where appropriate.
- ECG–PPG agreement for cardiac timing through the transition.
- Association between motion/quality measures and PPG feature changes.
- Between-person variability and within-person repeatability.
- Incremental predictive value of transition history.

## 5.3 Descriptive analysis

Report:
- number of participants enrolled and analysed;
- number of transitions attempted, detected, and retained;
- valid transition counts per participant and condition;
- signal-quality distributions;
- missingness and reasons for exclusion;
- participant-level and transition-level feature summaries.

Show individual trajectories, not only group averages. Group means can hide heterogeneous responses and different recovery shapes.

## 5.4 Mixed-effects modelling

Repeated observations are nested within transitions and participants. A mixed-effects model is a reasonable primary framework.

For example:

\[
y_{ijkt} = \beta_0 + \beta_1 T_{ij} + f(t) +
\beta_2[T_{ij}\times f(t)] + \boldsymbol{\gamma}^{T}\mathbf{c}_{ijkt}
+ b_{0i} + b_{1i}f(t) + \epsilon_{ijkt}
\]

where:
- \(y_{ijkt}\) is a PPG feature for participant \(i\), transition \(j\), and time \(t\);
- \(T_{ij}\) is transition type;
- \(f(t)\) is a flexible time function (e.g., spline);
- \(\mathbf{c}\) contains prespecified covariates;
- \(b_{0i}\) and \(b_{1i}\) are participant-level random effects.

Use an appropriate distribution and residual structure. PPG features may be skewed or heteroscedastic; transformation or robust methods may be needed.

## 5.5 Time-to-stabilization analysis

Stabilization time may be right-censored if a feature does not stabilize before the observation window ends. Consider survival/time-to-event methods, including mixed-effects or frailty extensions if supported by the sample size.

Do not exclude non-stabilizing transitions simply because they do not produce a finite recovery time. Their censoring is informative and should be reported.

## 5.6 Predictive comparison

Compare models using participant-wise or chronological validation:

- **Model A:** destination-state label only.
- **Model B:** destination state + transition history.
- **Model C:** transition history + accelerometry + signal-quality features.
- **Model D:** multimodal context (e.g., ECG, temperature, respiration) added where available.

Evaluate incremental performance with appropriate held-out participants or held-out trials, not random overlapping windows. Report confidence intervals and calibration where relevant.

## 5.7 Multiple comparisons and uncertainty

- Predefine primary contrasts.
- Use multiplicity correction for secondary feature/transition comparisons.
- Report effect sizes and confidence intervals, not only p-values.
- Consider bootstrap intervals clustered by participant.
- Report sensitivity to the stabilization threshold and persistence duration.

## 5.8 Missing data and quality-related selection

Signal-quality filtering can create selection bias if certain transition types systematically produce lower-quality signals. Report retention rates by transition and participant. Compare included and excluded transitions where possible. Consider inverse-probability weighting or sensitivity analyses only if justified by the data and sample size.

---

# 6. Distinguishing Physiology from Measurement Artifact

This distinction is essential to the credibility of the paper.

| Observation | Possible physiological explanation | Possible measurement explanation | Useful checks |
|---|---|---|---|
| PPG amplitude changes after sitting | Peripheral perfusion / vascular tone / blood-volume redistribution | Strap pressure or sensor displacement | ACC, pressure if available, waveform quality, repeat trials |
| Pulse interval changes | Cardiac rate response | Beat detector errors under motion | ECG comparison |
| Pulse shape changes | Vascular and hemodynamic changes | Contact geometry, motion, filtering | ECG timing, quality indices, sensor-position checks |
| PPG amplitude drifts with temperature | Thermoregulatory vasomotor response | Sensor/skin optical coupling changes | Skin temperature, contact, repeated stable trials |
| PPG becomes irregular during breathing | Respiratory modulation of stroke volume / venous return | Movement or poor beat segmentation | Respiration, ECG, quality assessment |

ECG can validate cardiac timing and help identify missed or extra PPG pulse detections. It cannot independently prove that PPG amplitude or morphology changes are physiological. For stronger vascular interpretation, consider repeated controlled trials, contact-pressure measurement, multiple sensing sites or wavelengths, and a validated reference where feasible.

A useful analysis architecture maintains separate outputs:
- `ppg_observed_quality_controlled`: observed PPG after documented artifact screening/correction;
- `physiological_context`: measured contextual variables;
- `transition_response_features`: observed feature trajectories;
- `stabilization_estimates`: estimated feature-specific stabilization times with uncertainty.

Do not describe a context-adjusted estimate as the “true PPG” or an exact counterfactual waveform.

---

# 7. Expected Contributions (Proposed, Not Results)

If supported by the data, the study could contribute:

1. **A transition-centric description of wearable PPG:** moving beyond static activity labels to include preceding-state information.
2. **A comparative characterization of PPG dynamics:** feature-specific response and stabilization profiles across transitions sharing a destination state.
3. **A multimodal analysis framework:** integrating PPG with movement, ECG timing, temperature, and respiration to interpret transient changes.
4. **Personalized recovery profiles:** quantifying individual variation in transition-related PPG responses.
5. **Practical guidance for wearable analytics:** identifying when post-transition PPG windows should be treated as transient rather than representative of a steady destination state.

The paper should only claim contributions actually demonstrated by the completed experiments.

---

# 8. Potential Figures and Tables

## Figures

1. **Conceptual overview:** different preceding states converge to a common sitting state, followed by distinct PPG trajectories.
2. **Study protocol timeline:** baseline, transition, and post-transition observation windows for each condition.
3. **Representative raw signals:** synchronized PPG, accelerometer, ECG, temperature, and respiration around a transition.
4. **Feature trajectories:** participant-level and population-level trajectories aligned to transition onset.
5. **Recovery/stabilization distributions:** per-transition estimates with uncertainty and censored observations.
6. **Multimodal model comparison:** current-state-only versus transition-aware versus multimodal model.
7. **Individual variability:** participant-specific transition profiles.

## Tables

1. Participant characteristics and sensor/device specifications.
2. Transition definitions and protocol parameters.
3. PPG feature definitions and quality criteria.
4. Number of attempted, detected, and valid transitions by participant and condition.
5. Primary transition comparisons with effect sizes and confidence intervals.
6. Sensitivity analyses across stabilization thresholds and signal-quality criteria.
7. Related-work comparison table.

---

# 9. Limitations and Threats to Validity

Anticipate and discuss the following:

- **Transition confounding:** walking, standing, and sleep differ in more than movement alone. Transition history is a bundle of physiological and behavioral differences.
- **Destination-state heterogeneity:** sitting posture, arm position, and settling behavior may vary.
- **Sleep-transition complexity:** waking includes sleep stage, circadian phase, arousal, and variable wake-to-sit delay.
- **Motion artifact:** the transition interval itself may degrade PPG quality.
- **Sensor coupling:** changes in wrist angle, strap tension, contact pressure, or local tissue geometry can alter PPG.
- **Limited ECG interpretation:** ECG supports cardiac timing validation but does not validate peripheral vascular morphology.
- **Feature dependence:** PPG amplitude and morphology are influenced by device, wavelength, site, and preprocessing.
- **Repeated-measures dependence:** many windows from one participant do not equal many independent participants.
- **Event imbalance:** some transitions may be rare in a 10-day free-living recording.
- **Generalizability:** healthy young adults, one device, or one sensor site may not represent other populations or devices.
- **Causal interpretation:** observational associations cannot establish that preceding activity itself caused a given PPG trajectory.

A particularly important limitation is that a 10-day continuous recording may provide many hours of data but relatively few clean, repeated examples of each transition. A structured protocol is likely necessary for the primary comparison.

---

# 10. Reproducibility and Data Management

Before analysis, specify:

- data dictionary and units;
- sensor synchronization procedure;
- preprocessing software and version;
- filter and beat-detection parameters;
- transition event definitions;
- quality thresholds;
- primary and secondary endpoints;
- stabilization threshold and persistence duration;
- statistical model specification;
- train/validation/test split strategy;
- exclusion criteria and missing-data handling.

Recommended project structure:

```text
project/
├── README.md
├── manuscript/
│   ├── draft.md
│   ├── references.bib
│   └── figures/
├── data/
│   ├── raw/                 # access controlled; do not publish identifiers
│   ├── processed/
│   └── metadata/
├── protocols/
│   ├── study_protocol.md
│   └── event_annotation_guide.md
├── src/
│   ├── preprocessing/
│   ├── transition_detection/
│   ├── feature_extraction/
│   ├── quality_control/
│   └── statistics/
├── results/
│   ├── tables/
│   └── figures/
└── environment/
    └── requirements.txt
```

For publication, share code and de-identified data or derived data where ethics, consent, and data-use agreements permit. Document any restrictions.

---

# 11. Suggested Work Plan

1. **Focused literature review:** search for PPG recovery kinetics, postural transition response, exercise recovery, autonomic recovery, and wearable PPG signal quality.
2. **Operational definitions:** settle transition onset/offset, destination posture, feature definitions, and stabilization criteria.
3. **Pilot data audit:** quantify the number of usable transitions, synchronization quality, motion contamination, and feature reliability.
4. **Pilot protocol:** test repeated standing→sitting, walking→sitting, and supine→sitting transitions.
5. **Primary analysis preregistration:** choose one primary feature/endpoint and specify contrasts and model.
6. **Main data collection:** collect enough repeated transitions across participants to support the planned analysis.
7. **Signal-quality analysis:** characterize retention and artifact rates by transition.
8. **Statistical analysis:** fit trajectory and stabilization models with participant-level dependence.
9. **Robustness checks:** vary quality thresholds, stabilization tolerance, and observation window.
10. **Manuscript completion:** report results transparently, include null findings, and avoid overclaiming causality or novelty.

---

# 12. Publication Positioning

## 12.1 What is likely to be insufficient?

A paper that only:
- detects activity transitions;
- plots PPG before and after activity;
- reports a mean recovery time for each activity;
- or claims that one transition is “slower” without controlling participant, workload, posture, and signal quality

may be viewed as incremental or under-controlled.

## 12.2 What would strengthen the paper?

- A clear common-destination comparison.
- Repeated within-participant trials.
- Prespecified feature-specific stabilization definitions.
- Multimodal measurement and independent ECG timing validation.
- Explicit analysis of signal quality and sensor coupling.
- Participant-level variability and uncertainty.
- Chronological or participant-wise validation.
- A reproducible protocol and analysis pipeline.
- A transparent, systematic account of related work.

## 12.3 Possible journal scope

The eventual target depends on the strength of the dataset and contribution. Potential journal *areas* include biomedical signal processing, wearable sensing, physiological measurement, digital health, and biomedical engineering. Do not choose a journal solely by impact factor. Check whether it publishes original physiological measurement studies, its indexing, peer-review standards, fees, data policies, and current author guidelines. Avoid predatory journals and guaranteed-acceptance solicitations.

---

# 13. Literature Search Strategy for Confirming Novelty

Use multiple databases and record the search date, exact query, filters, and screening decisions.

### Suggested search terms

```text
("photoplethysmography" OR PPG) AND
("recovery time" OR "recovery dynamics" OR "stabilization" OR "settling time")

("photoplethysmography" OR PPG) AND
("postural transition" OR "posture change" OR "activity transition")

("photoplethysmography" OR PPG) AND
("exercise recovery" OR "vascular recovery" OR "heart rate recovery")

("wearable" AND PPG) AND
("transition history" OR "preceding activity" OR "activity context")

(PPG OR photoplethysmography) AND
("sleep to wake" OR awakening OR "wake transition")
```

Search:
- PubMed / MEDLINE
- IEEE Xplore
- Scopus
- Web of Science
- Google Scholar

Screen titles/abstracts, then full texts. Follow references of the most relevant papers and search for papers that cite them. Record whether each paper measures:
- transition onset and post-transition time course;
- multiple preceding states;
- a common destination state;
- PPG morphology/amplitude versus HR only;
- ECG or other reference modalities;
- repeated within-person trials;
- explicit recovery/stabilization metrics.

Only after this process should the manuscript state that the exact comparison is novel or previously unstudied.

---

# 14. References

The following are verified starting references for the current draft. Add complete author lists, issue/page information, and citation formatting from the publisher or bibliographic database before submission.

1. **Measuring Vascular Recovery Rate After Exercise.** Open access: https://pmc.ncbi.nlm.nih.gov/articles/PMC7612924/ ; PubMed: https://pubmed.ncbi.nlm.nih.gov/35782201/
2. Linder, S. P., Wendelken, S. M., Wei, E., & McGrath, S. P. (2006). Using the morphology of photoplethysmogram peaks to detect changes in posture. *Journal of Clinical Monitoring and Computing, 20*, 151–158. https://doi.org/10.1007/s10877-006-9015-2
3. Pauls, J. P., Roberts, L. A., Burgess, T., Fraser, J. F., Gregory, S. D., & Tansley, G. (2018). Time course response of the heart and circulatory system to active postural changes. *Journal of Biomechanical Engineering, 140*(3). https://doi.org/10.1115/1.4038429
4. Nawar, A., Kilic, O. S., Rahman, F. N., Chen, C., Berkebile, J. A., Chan, M., Shah, A. J., & Inan, O. T. (2025). Elucidating the reactivity of reflectance-based core-body photoplethysmogram to posture and respiratory changes. *IEEE Sensors Journal, 25*(18), 35447–35459. https://doi.org/10.1109/JSEN.2025.3596522
5. Charlton, P. H., et al. (2020). Acquiring wearable photoplethysmography data in daily life: The PPG Diary pilot study. *Engineering Proceedings, 2*(1), 80. https://doi.org/10.3390/ecsa-7-08233
6. Accuracy of heart-rate-recovery parameters assessed from a wrist-worn photoplethysmography monitor (Polar Unite). (2023). *International Journal of Sports Physiology and Performance*. https://doi.org/10.1123/ijspp.2023-0120

---

# 15. Final Research Position

The strongest defensible framing is not simply that “PPG changes after activity.” That is already established.

The more focused question is:

> **When people enter the same destination state, does the preceding physiological state explain the subsequent PPG feature trajectory and feature-specific stabilization time, beyond current activity/posture and measurable signal-quality effects?**

This question is testable, relevant to continuous wearable monitoring, and naturally motivates multimodal measurement. Its publishability will depend on the rigor of the protocol, repeated observations, signal-quality controls, statistical analysis, and a completed literature review.

**Recommended first-paper scope:** Start with three transitions ending in sitting—standing→sitting, standardized walking→sitting, and supine-rest→sitting. Treat sleeping→sitting as a separate naturalistic extension because waking and circadian factors make it substantially harder to control. Add more transitions only when the primary comparison is well powered and interpretable.
