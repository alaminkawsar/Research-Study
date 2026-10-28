# Personalized Photoplethysmography (PPG) Baseline Estimation

## A Research-Oriented Review of Signal Quality, Artifact Detection, Denoising, and Robust Reference-Waveform Construction

**Document type:** Research-oriented technical README\
**Prepared:** 28 October 2026\
**Scope:** Optical PPG sensing for health-related research, with
emphasis on personalized baseline estimation.

------------------------------------------------------------------------

## Abstract

Photoplethysmography (PPG) is a non-invasive optical technique that
measures changes in light absorption and/or scattering associated with
pulsatile changes in peripheral blood volume. PPG is widely used in
wearable heart-rate monitoring and contributes to applications such as
pulse-rate variability, oxygen saturation estimation, respiratory
monitoring, and exploratory cardiovascular assessment. However, recorded
PPG is affected by motion, sensor--skin coupling, ambient light, tissue
optics, peripheral perfusion, temperature, hardware noise, sampling, and
signal-processing choices.

This README synthesizes a practical research framework for estimating a
person's high-quality, repeatable PPG reference waveform and
physiological baseline. It distinguishes true physiological variation
from measurement artifacts, reviews established classes of
signal-quality assessment and artifact-reduction methods, and proposes a
reproducible pipeline combining standardized acquisition, integrity
checks, signal-quality indices (SQIs), conservative preprocessing,
beat-level template matching, optional reference-sensor-assisted
cancellation, and robust personalized template estimation. It also
outlines validation criteria, experimental design, reporting
recommendations, and limitations.

A central conclusion is that a universally "ideal" PPG waveform cannot
generally be recovered from a single corrupted recording. Some artifacts
overlap with the physiological signal, while some external factors
genuinely change peripheral blood flow. Therefore, the defensible goal
is not to claim perfect recovery, but to estimate a **high-quality,
condition-specific personal reference**, quantify uncertainty, and
explicitly identify recordings that cannot be corrected reliably.

**Keywords:** photoplethysmography; PPG; signal quality index; motion
artifact; adaptive filtering; pulse morphology; personalized baseline;
template matching; wearable sensors; signal reconstruction.

------------------------------------------------------------------------

## 1. Research question and objectives

### 1.1 Core research question

Can a person's clean underlying PPG waveform be estimated by detecting
and reducing measurement interference while preserving genuine
individual cardiovascular characteristics?

### 1.2 Practical research objective

Develop a method that:

1.  identifies high-quality portions of raw PPG;
2.  detects artifacts and recording failures;
3.  corrects only disturbances for which a defensible correction is
    available;
4.  rejects or flags irrecoverable segments rather than fabricating
    plausible-looking waveforms;
5.  constructs a personalized reference waveform from reliable beats;
6.  estimates person-specific baseline features and their natural
    variability;
7.  validates the result across sessions and against independent
    reference measurements.

### 1.3 Terminology: "ideal" versus "high-quality baseline"

An **ideal PPG signal** unaffected by every external or physiological
factor is generally not observable directly. A recorded signal combines
pulsatile blood-volume changes, non-pulsatile tissue and optical
contributions, sensor characteristics, environmental interference, and
noise. Multiple underlying signals can produce similar observed
recordings, so perfect reconstruction is not guaranteed.

For this project, use the following operational definitions:

-   **High-quality PPG segment:** a segment that passes pre-specified
    integrity and quality checks and is suitable for the intended
    analysis.
-   **Personalized reference waveform:** a robust estimate of the
    person's typical pulse morphology under a defined measurement
    protocol.
-   **Personalized physiological baseline:** a distribution of
    person-specific metrics---such as pulse rate, pulse amplitude, pulse
    intervals, and morphology---under specified resting or other
    standardized conditions.
-   **Artifact correction:** an estimate of and reduction in a
    disturbance using a method and assumptions that can be evaluated.
-   **Artifact rejection:** exclusion or flagging of segments that
    cannot be trusted for the intended measurement.

A baseline is conditional on the measurement site, device, wavelength,
sensor fit, posture, activity, temperature, time of day, and
physiological state. It should not be treated as a universal immutable
waveform.

------------------------------------------------------------------------

## 2. How PPG is formed and why it varies

PPG sensors illuminate tissue using one or more wavelengths and detect
changes in returned or transmitted light. The pulsatile component is
associated with cardiac-cycle-related changes in local blood volume. The
measured signal also includes slowly varying optical and tissue
components, device effects, and noise.

A useful conceptual model is:

``` text
Observed PPG
    = pulsatile physiological component
    + non-pulsatile tissue / optical component
    + physiological modulation
    + motion and contact artifacts
    + ambient-light interference
    + electronic and sampling noise
    + processing / transmission errors
```

This is a conceptual decomposition, not an assertion that all components
are linearly additive or independently identifiable. In real recordings,
components can interact: movement may change contact pressure and
perfusion, while exercise changes both heart rate and motion.

### 2.1 Physiological variation versus measurement artifact

**Genuine physiological variation** may include changes in heart rate,
respiration-related modulation, vascular tone, peripheral perfusion,
pulse amplitude, and cardiac rhythm. These changes may be the target of
the study.

**Measurement artifacts** include sensor displacement, optical leakage,
saturation, missing samples, electronic interference, and motion-induced
disturbances that obscure the pulse.

**Mixed effects** occur when a condition changes both physiology and
measurement quality. Exercise, for example, can increase heart rate and
perfusion while also producing motion, sweating, and changing sensor
contact.

The distinction matters because blindly removing every deviation from a
template can suppress meaningful physiology.

------------------------------------------------------------------------

## 3. Factors that affect PPG signal quality

### 3.1 Motion-related artifacts

-   Walking, running, cycling, exercise, and other body movements
-   Wrist, finger, hand, or arm movement
-   Sensor sliding or displacement relative to skin
-   Changes in contact pressure during movement
-   Muscle contraction, tremor, and repetitive motion
-   External vibration and mechanical shock
-   Movement with a frequency close to the cardiac pulse frequency

**Potential effects:** baseline shifts, waveform distortion, false
peaks, missed beats, altered pulse amplitude, and erroneous HR or
HRV/PRV estimates.

**Research notes:** synchronized accelerometer or gyroscope data can
provide a useful motion reference, but motion sensors do not measure all
sources of PPG corruption. Movement can also alter real blood flow.

### 3.2 Sensor placement and skin contact

-   Loose or excessively tight attachment
-   Incorrect sensor orientation or anatomical placement
-   Changing sensor-to-skin distance
-   Contact-pressure variation
-   Poor optical coupling
-   Curved or uneven measurement surfaces
-   Hair, sweat, dirt, tattoos, or other material at the interface
-   Differences between finger, wrist, ear, forehead, and other sites

**Potential effects:** changes in optical coupling, local perfusion,
pulse amplitude, morphology, and motion sensitivity.

### 3.3 Ambient light and optical interference

-   Direct sunlight
-   Indoor fluorescent or LED lighting
-   Periodic lighting flicker
-   Infrared sources and changing environmental illumination
-   Light leakage around the sensor housing
-   Reflections from nearby surfaces

**Potential effects:** background-light variation, periodic
interference, reduced dynamic range, and detector saturation.

### 3.4 Physiological and cardiovascular factors

-   Heart-rate changes and irregular rhythms
-   Peripheral vasoconstriction and vasodilation
-   Blood pressure and vascular-tone changes
-   Respiration-related modulation
-   Exercise and recovery
-   Stress and autonomic nervous system activity
-   Skin and ambient temperature
-   Hydration and peripheral perfusion
-   Age-related vascular differences
-   Edema and other changes in local tissue

**Potential effects:** genuine changes in amplitude, morphology, timing,
and beat-to-beat variation. These should not automatically be classified
as noise.

### 3.5 Skin and tissue characteristics

-   Skin pigmentation and melanin concentration
-   Tissue thickness and composition
-   Subcutaneous tissue and measurement-site anatomy
-   Local perfusion
-   Scars, tattoos, skin lesions, and hair
-   Differences in optical wavelength and sensor geometry

**Potential effects:** changes in absorption, scattering, penetration
depth, and the pulsatile signal's strength. The effect depends on the
sensor's optical design and should be evaluated across the intended
population.

### 3.6 Hardware and electronic noise

-   Photodiode shot noise
-   Electronic thermal noise
-   Amplifier noise, offsets, and drift
-   Low signal-to-noise ratio (SNR)
-   Analog-to-digital converter (ADC) quantization
-   Inadequate sampling rate
-   LED intensity instability
-   Saturation and clipping
-   Power-supply or electromagnetic interference
-   Clock jitter, packet loss, and communication errors

**Potential effects:** random fluctuations, waveform distortion, missing
samples, clipping, and unreliable pulse detection.

### 3.7 Environment and activity

-   Ambient temperature and humidity
-   Sweating and moisture
-   Posture changes, including lying, sitting, and standing
-   Exercise and recovery
-   Altitude-related physiological responses
-   Mechanical vibration

These factors may influence the sensor, physiology, or both.

### 3.8 Signal-processing and algorithmic factors

-   Incorrect or overly aggressive filter settings
-   Poor beat detection and fiducial-point localization
-   Baseline correction that removes slow physiological information
-   Aliasing and inappropriate resampling
-   Poor motion cancellation
-   Window length and segmentation choices
-   Normalization that removes meaningful amplitude information
-   Model overfitting and population/device mismatch
-   Missing-data handling and data-transmission errors

A smooth waveform is not necessarily an accurate waveform. Processing
choices must be documented and validated against the target use.

------------------------------------------------------------------------

## 4. Established method families

No single technique is optimal for all PPG devices, environments, and
health targets. A defensible system usually combines quality assessment,
conservative processing, and selective correction.

### 4.1 Signal Quality Indices (SQIs) and segment rejection

**Purpose:** identify windows or beats that are suitable for analysis
before attempting reconstruction.

Potential quality indicators include:

-   Pulse morphology and shape consistency
-   Agreement between independent beat detectors
-   Pulse-template correlation
-   Skewness and other waveform statistics
-   Pulse amplitude and perfusion-related indicators
-   Plausibility of pulse intervals
-   Clipping, flat-line, dropout, and missing-sample detection
-   Accelerometer-derived movement features
-   Cross-channel agreement, if multiple optical channels are available

**Advantages:** protects downstream estimates from severely corrupted
data; makes quality and coverage measurable.

**Limitations:** SQIs are task- and device-dependent. A pulse may be
unusual but physiologically real. Thresholds should be calibrated and
validated, not assumed universal.

**Recommendation:** use a combination of integrity checks and quality
features, with a third category for uncertain segments rather than
forcing every segment into "good" or "bad."

### 4.2 Accelerometer-assisted adaptive filtering

Common methods include:

-   Least Mean Squares (LMS)
-   Normalized LMS (NLMS)
-   Recursive Least Squares (RLS)
-   Motion-reference cancellation using accelerometer or gyroscope
    channels

The motion sensor provides a reference signal. An adaptive filter
estimates the portion of PPG correlated with that reference, and the
estimated component is subtracted.

**Advantages:** useful for wearable recordings where motion is a major
disturbance and a synchronized reference channel is available.

**Limitations:** accelerometers do not capture all optical artifacts;
real physiology may correlate with movement; cancellation can remove
pulse information or distort morphology.

**Recommendation:** compare filtered and unfiltered signals, quantify
waveform distortion, and do not assume that greater attenuation means
greater physiological accuracy.

### 4.3 Beat-level template matching

A personalized pulse template can be used to identify beats that differ
substantially from the person's accepted pulse morphology.

Typical procedure:

1.  Detect candidate beats.
2.  Align beats to a consistent fiducial point.
3.  Normalize beat duration for morphology comparisons.
4.  Compare each beat with a reference template.
5.  Combine template similarity with amplitude, interval, and
    signal-integrity checks.
6.  Reject or flag low-confidence beats.
7.  Update the template only with accepted beats and suitable
    safeguards.

**Advantages:** individualized, interpretable, and directly useful for
personalized baseline construction.

**Limitations:** genuine morphology can change with respiration,
posture, vascular tone, exercise, and illness. A rigid template can
reject valid physiology. An adaptive template can also drift toward
corrupted data if updates are not quality-controlled.

**Recommendation:** use a robust initial template, conservative update
rules, and a separate uncertainty score. Preserve raw data and original
beat timestamps.

### 4.4 Wavelet denoising and signal decomposition

Methods include:

-   Discrete wavelet transform and wavelet denoising
-   Empirical Mode Decomposition (EMD)
-   Ensemble EMD (EEMD)
-   Variational Mode Decomposition (VMD)

These methods represent the signal as components at different scales or
modes, then suppress components judged to be noise.

**Advantages:** can handle nonstationary signals and transient
disturbances.

**Limitations:** physiological and artifact components can overlap in
frequency or timescale. Mode selection can be subjective, and
decomposition can distort pulse shape.

**Recommendation:** define component-selection rules in advance and
validate morphology, timing, and target-metric error. Do not label a
component as noise based on frequency alone.

### 4.5 Conventional filtering and baseline correction

A bandpass filter can suppress frequencies outside a target range.
Butterworth filters are commonly used; an example band sometimes
considered for adult pulse monitoring is approximately 0.5--10 Hz.

This is an example, **not a universal prescription**. The appropriate
range depends on sampling rate, expected heart rate, target variable,
sensor, and the need to preserve pulse morphology or slower respiratory
and vascular modulation.

Important implementation decisions include:

-   Filter type and order
-   Cutoff frequencies
-   Causal versus zero-phase filtering
-   Edge handling and transient exclusion
-   Whether the data are processed offline or in real time

Filtering cannot separate noise from physiology when they occupy
overlapping bands. Excessive filtering may produce misleadingly smooth
signals.

### 4.6 Multichannel and multisensor fusion

Possible additional measurements:

-   Multiple optical wavelengths
-   Multiple photodiodes or spatially separated optical channels
-   Accelerometer and gyroscope
-   ECG
-   Skin temperature
-   Contact pressure or force
-   Environmental illumination

Independent information can improve artifact detection and help
distinguish movement, contact, and optical interference.

ECG can validate cardiac timing, but ECG and PPG are not identical
measurements: ECG records cardiac electrical activity, while PPG records
peripheral optical changes. ECG therefore cannot by itself provide the
exact ideal optical waveform.

### 4.7 Reference-signal-less artifact detection

If no accelerometer or external reference is available,
signal-processing features and machine-learning models can identify
likely artifacts using PPG alone.

This may be useful for low-cost devices, but the problem is less
identifiable: a waveform anomaly can reflect either artifact or genuine
physiology. Evaluation should include multiple participants, sessions,
activity conditions, and independent quality labels where possible.

### 4.8 A combined strategy

The recommended order is:

1.  Detect data-integrity failures.
2.  Apply conservative preprocessing.
3.  Estimate signal quality.
4.  Correct artifacts only where a justified reference or model exists.
5.  Reassess quality after correction.
6.  Reject or flag unrecoverable segments.
7.  Construct the personalized template from high-quality beats.
8.  Validate the template and quantify uncertainty.

This is a proposed research framework assembled from established method
families. It is not claimed to be a universally validated, off-the-shelf
algorithm.

------------------------------------------------------------------------

## 5. Proposed end-to-end research pipeline

``` text
┌───────────────────────────────────────────────────────────┐
│ 1. STANDARDIZED DATA ACQUISITION                           │
│ Raw PPG + timestamps + optional IMU, ECG, temperature,     │
│ pressure and ambient-light measurements                    │
└──────────────────────────────┬────────────────────────────┘
                               ▼
┌───────────────────────────────────────────────────────────┐
│ 2. DATA-INTEGRITY CHECKS                                   │
│ Missing samples, clipping, saturation, dropouts,           │
│ synchronization errors and sensor-contact failures        │
└──────────────────────────────┬────────────────────────────┘
                               ▼
┌───────────────────────────────────────────────────────────┐
│ 3. CONSERVATIVE PREPROCESSING                              │
│ Appropriate filtering, baseline handling and synchronization│
└──────────────────────────────┬────────────────────────────┘
                               ▼
┌───────────────────────────────────────────────────────────┐
│ 4. SIGNAL QUALITY / ARTIFACT DETECTION                    │
│ Morphology + pulse detection + motion + amplitude +        │
│ interval plausibility + integrity features                │
└──────────────────────────────┬────────────────────────────┘
                               ▼
                    ┌──────────────────┐
                    │ Quality decision │
                    └────────┬─────────┘
                       ┌─────┴──────┐
                       ▼            ▼
              ┌─────────────┐ ┌──────────────────┐
              │ UNRELIABLE  │ │ HIGH QUALITY     │
              │ Flag/reject │ │ Retain candidate │
              │ or reacquire│ │ beats            │
              └─────────────┘ └────────┬─────────┘
                                       ▼
┌───────────────────────────────────────────────────────────┐
│ 5. OPTIONAL ARTIFACT CORRECTION                           │
│ Adaptive cancellation, decomposition or other justified  │
│ correction; then repeat quality checks                    │
└──────────────────────────────┬────────────────────────────┘
                               ▼
┌───────────────────────────────────────────────────────────┐
│ 6. PERSONALIZED TEMPLATE CONSTRUCTION                     │
│ Beat alignment → duration normalization → robust median   │
│ template → variability envelope → guarded updates         │
└──────────────────────────────┬────────────────────────────┘
                               ▼
┌───────────────────────────────────────────────────────────┐
│ 7. BASELINE FEATURE ESTIMATION                             │
│ Pulse rate, pulse intervals, amplitude, morphology and     │
│ within-person variability under defined conditions        │
└──────────────────────────────┬────────────────────────────┘
                               ▼
┌───────────────────────────────────────────────────────────┐
│ 8. VALIDATION AND UNCERTAINTY                              │
│ Reference comparison, repeated sessions, robustness,      │
│ confidence and usable-data coverage                       │
└───────────────────────────────────────────────────────────┘
```

### 5.1 Data acquisition protocol

For an initial study:

-   Define the target use (e.g., heart rate, PRV, pulse morphology, or
    artifact detection).
-   Standardize anatomical site, device, wavelength, orientation,
    attachment, and recording settings.
-   Use a consistent acclimatization and resting period for the resting
    baseline.
-   Record several repeated sessions, ideally on different occasions.
-   Record posture, activity, ambient conditions, and relevant protocol
    metadata.
-   If possible, synchronize an accelerometer and ECG reference.
-   Retain the raw signal unchanged, with timestamps and device
    metadata.
-   Use ethics-approved procedures and appropriate informed consent.

Do not deliberately induce unsafe physiological states. For movement
studies, use safe, pre-specified tasks and stop criteria.

### 5.2 Data-integrity checks

Detect and mark:

-   Missing or duplicated samples
-   Flat-line intervals
-   ADC or photodetector saturation
-   Clipping
-   Large discontinuities
-   Clock drift and synchronization errors
-   Sensor disconnection or contact failure

These problems are often better handled through rejection or
reacquisition than through denoising.

### 5.3 Preprocessing

Apply filtering and baseline handling only after documenting the
sampling rate and target feature. For morphology or HRV/PRV analysis,
preserve original timestamps and avoid transformations that alter beat
intervals without accounting for that effect.

### 5.4 Quality assessment

Use overlapping windows (e.g., 5--10 seconds as an initial experimental
choice, not a universal optimum) and/or beat-level decisions. Combine
several quality indicators rather than relying on a single threshold.

Record:

-   Quality score
-   Rejection reason
-   Motion level
-   Clipping/dropout flags
-   Beat-detection confidence
-   Whether correction was applied
-   Quality before and after correction

### 5.5 Personalized template estimation

For each accepted beat:

1.  Identify a consistent fiducial point, such as pulse onset, using a
    defined detector.
2.  Align the beat to the fiducial.
3.  Resample to a common normalized phase or duration for shape
    comparison.
4.  Apply an explicitly documented normalization strategy.
5.  Estimate the pointwise median waveform.
6.  Calculate an uncertainty envelope, such as pointwise interquartile
    range.
7.  Check whether template quality and morphology are stable across
    sessions.

**Keep amplitude and timing information separately.** Normalized beats
are useful for shape comparison but do not preserve absolute optical
amplitude or actual beat duration.

### 5.6 Baseline feature distributions

Do not store only a single template. Store distributions and context for
relevant features, for example:

-   Pulse rate and its variability
-   Pulse interval / PRV features, with clear definitions
-   Raw or calibrated pulse amplitude
-   Normalized morphology features
-   Beat-to-beat template similarity
-   Quality score and valid-data coverage
-   Posture, activity, sensor site, and session metadata

A personalized baseline should include expected variation, not just a
single "ideal" value.

------------------------------------------------------------------------

## 6. Validation plan

A waveform that looks clean is not proof that it is physiologically
accurate. Validation should be designed around the research target.

### 6.1 Morphological fidelity

Possible metrics:

-   Correlation with an independent high-quality reference waveform
-   Root Mean Square Error (RMSE), where signals are meaningfully
    aligned and scaled
-   Dynamic Time Warping (DTW) distance, with appropriate safeguards
-   Fiducial-point timing error
-   Pulse amplitude error
-   Pulse-width or morphology-feature error

Correlation can remain high despite amplitude bias, and RMSE can be
misleading if alignment or scaling differs. Report complementary
metrics.

### 6.2 Physiological validity

-   Compare pulse timing against synchronized ECG-derived R-peaks when
    appropriate.
-   Evaluate beat detection sensitivity, positive predictive value, and
    timing error.
-   For HRV/PRV work, explicitly evaluate interval errors and the
    intended HRV/PRV features.
-   For SpO₂, use an appropriate validated reference method and
    protocol; ordinary PPG waveform similarity is not sufficient.
-   For blood-pressure estimation, use a suitable reference and study
    design; a clean waveform alone does not validate blood pressure.

### 6.3 Repeatability

Construct separate templates from repeated sessions. Compare:

-   Morphology similarity
-   Feature distributions
-   Within-session versus between-session variation
-   Stability under the same protocol
-   Changes associated with different conditions

Large differences should prompt investigation rather than automatic
averaging.

### 6.4 Robustness and correction benefit

Compare raw, filtered, artifact-corrected, and rejected-segment
approaches. Test controlled conditions separately and in combination.

Report both accuracy and **coverage**: a method may achieve high
accuracy by rejecting most of the data. Both the accepted-data
performance and the fraction of usable recordings are essential.

### 6.5 Data leakage and evaluation design

For machine-learning methods, split data by participant and, where
relevant, by session. Avoid allowing beats from the same recording to
appear in both training and test sets if the intended claim is
generalization to unseen people. For personalized models, clearly
separate the enrollment/calibration data from later evaluation sessions.

------------------------------------------------------------------------

## 7. Recommended experimental comparisons

A useful initial study could compare the following pipelines on the same
recordings:

  -----------------------------------------------------------------------
  Pipeline                Processing strategy     Main question
  ----------------------- ----------------------- -----------------------
  A                       Raw signal with         What is the unprocessed
                          integrity checks        performance?

  B                       Conventional filtering  How much does basic
                                                  preprocessing help?

  C                       Filtering + SQI         Does selective use of
                          rejection               reliable segments
                                                  improve results?

  D                       Filtering +             Does personalized
                          beat-template quality   morphology improve
                          assessment              selection?

  E                       Motion-reference        Does reference-guided
                          adaptive filtering +    correction improve
                          SQI                     motion robustness?

  F                       Decomposition-based     Does nonstationary
                          denoising + SQI         denoising add benefit?

  G                       Combined pipeline +     Does the integrated
                          personalized baseline   framework improve
                                                  accuracy,
                                                  repeatability, and
                                                  usable coverage?
  -----------------------------------------------------------------------

Pre-register or document thresholds and tune them only on
training/validation data. Compare the methods on held-out participants
or sessions and report confidence intervals where feasible.

------------------------------------------------------------------------

## 8. Important cautions

1.  **No universal clean-signal oracle exists.** The true optical
    waveform is not normally available for every noisy recording.
2.  **Filtering is not equivalent to artifact removal.** Noise and
    physiology can overlap in frequency and timing.
3.  **A template is not ground truth.** It is a model of typical
    morphology under specific conditions.
4.  **Personalization can overfit.** A template can learn artifacts or
    reject genuine physiological changes if updates are uncontrolled.
5.  **Baseline is conditional.** Resting baseline, exercise baseline,
    and baseline under cold conditions should not automatically be
    merged.
6.  **Cross-device amplitude comparison is difficult.** LED power, gain,
    wavelength, geometry, and skin coupling affect the raw optical
    signal.
7.  **PPG-derived PRV is not always equivalent to ECG-derived HRV.**
    Pulse arrival and peripheral vascular effects matter.
8.  **Do not over-normalize.** Normalization can conceal amplitude
    differences that may be scientifically meaningful.
9.  **Report rejected data.** A method that rejects difficult segments
    should report rejection rates and performance on accepted data.
10. **Avoid unsupported medical claims.** Improved signal quality alone
    does not establish clinical accuracy or diagnostic validity.

------------------------------------------------------------------------

## 9. Suggested outputs for a research implementation

A reproducible software implementation should produce at least:

``` text
research_output/
├── README.md
├── data_dictionary.md
├── protocol/
│   ├── acquisition_protocol.md
│   └── quality_thresholds.md
├── results/
│   ├── signal_quality_summary.csv
│   ├── rejected_segments.csv
│   ├── baseline_features.csv
│   ├── template_waveforms.csv
│   └── validation_metrics.csv
└── figures/
    ├── raw_vs_processed_ppg.png
    ├── quality_score_timeline.png
    ├── personalized_template_and_variability.png
    └── cross_session_baseline_comparison.png
```

Recommended per-segment metadata include participant pseudonym, session
ID, device and channel, sampling rate, timestamps, activity/posture
labels, quality score, artifact labels, processing method, and
inclusion/exclusion reason. Use appropriate privacy and data-governance
controls.

------------------------------------------------------------------------

## 10. Selected literature and further reading

The following sources are starting points for a literature review.
Verify bibliographic details, publication status, methods, and relevance
before citing them in a formal manuscript.

1.  **Wearable Photoplethysmography for Cardiovascular Monitoring.**
    Review of wearable PPG, measurement limitations, motion artifacts,
    and cardiovascular monitoring.\
    https://pmc.ncbi.nlm.nih.gov/articles/PMC7612541/

2.  **Machine Learning Applied to Reference Signal-Less Detection of
    Motion Artifacts in Photoplethysmographic Signals: A Review.**
    Relevant to PPG-only artifact detection when no independent motion
    reference is available.\
    https://pmc.ncbi.nlm.nih.gov/articles/PMC11598458/

3.  **Pulse-based photoplethysmography quality assessment improves
    wearable seizure detection performance.** A 2026 study relevant to
    pulse-level quality assessment and template-based approaches; its
    application is specific and should not be assumed to validate a
    universal baseline method.\
    https://onlinelibrary.wiley.com/doi/full/10.1002/epi4.70242

4.  **Heart rate tracking in photoplethysmography signals affected by
    motion artifacts: a review.** Review of approaches to heart-rate
    tracking under motion.\
    https://link.springer.com/article/10.1186/s13634-020-00714-2

5.  **Photoplethysmogram Analysis and Applications: An Integrative
    Review.** Background on PPG waveform analysis, processing, and
    applications.\
    https://pmc.ncbi.nlm.nih.gov/articles/PMC8920970/

6.  **A Survey of Photoplethysmography and Imaging Photoplethysmography
    Quality Assessment Methods.** Useful for SQI and quality-assessment
    methodology.\
    https://www.mdpi.com/2076-3417/12/19/9582

7.  **Sources of Inaccuracy in Photoplethysmography for Continuous
    Cardiovascular Monitoring.** Discusses factors contributing to PPG
    measurement error.\
    https://pmc.ncbi.nlm.nih.gov/articles/PMC8073123/

8.  **Determinants of photoplethysmography signal quality at the
    wrist.** Relevant to wrist-worn PPG measurement conditions and
    signal quality.\
    https://journals.plos.org/digitalhealth/article?id=10.1371/journal.pdig.0000585

These sources cover complementary topics; they should not be interpreted
as proving that one specific combination of methods is best for every
PPG research setting.

------------------------------------------------------------------------

## 11. Recommended research direction

A defensible research title is:

> **Personalized PPG Baseline Estimation Through Signal Quality
> Assessment, Artifact Rejection, and Robust Pulse Morphology Modeling**

The contribution should be more than a new filter. The system should
determine which segments are trustworthy, which disturbances can be
corrected, which segments should be rejected, and how confidently a
person's reference waveform can be estimated.

A strong first implementation would compare:

1.  conservative filtering;
2.  SQI-based rejection;
3.  personalized beat-template matching;
4.  accelerometer-assisted adaptive filtering, if motion reference data
    are available; and
5.  the combined approach.

Evaluate morphology, target-parameter accuracy, repeatability across
sessions, robustness, and usable-data coverage. Keep the raw recordings,
quality decisions, processed waveforms, and uncertainty measures so
results can be audited and reproduced.

### Final takeaway

The realistic scientific target is not an unknowable waveform free of
every influence. It is a **validated, personalized, condition-specific
high-quality PPG reference, accompanied by uncertainty estimates and
explicit limits on when the signal can be trusted**.
