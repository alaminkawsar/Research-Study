# Heart Sound Intelligence: PCG Analysis, Visualization, Feature Engineering & Research Roadmap

> A research-oriented guide to analyzing heart sounds (phonocardiograms
> / PCGs), extracting acoustic and cardiac-cycle features, visualizing
> recordings, developing machine-learning systems, and identifying
> future research opportunities.

**Project scope:** audio-based heart sound research, with optional ECG,
PPG, demographic, clinical, and imaging data when available.\
**Primary input:** recorded heart sounds (`.wav`, `.m4a`, `.flac`,
etc.).\
**Intended users:** students, biomedical engineers, data scientists,
clinicians, and research teams.

------------------------------------------------------------------------

## Table of contents

1.  [Project overview](#1-project-overview)
2.  [What a heart-sound recording can and cannot tell
    us](#2-what-a-heart-sound-recording-can-and-cannot-tell-us)
3.  [Potential research problems](#3-potential-research-problems)
4.  [Audio visualization: waveform, PCG, spectrogram, ECG-style views,
    and
    video](#4-audio-visualization-waveform-pcg-spectrogram-ecg-style-views-and-video)
5.  [Comprehensive feature-extraction
    catalogue](#5-comprehensive-feature-extraction-catalogue)
6.  [Biomarkers and patient-level
    variables](#6-biomarkers-and-patient-level-variables)
7.  [Recommended end-to-end research
    pipeline](#7-recommended-end-to-end-research-pipeline)
8.  [Machine-learning and deep-learning
    directions](#8-machine-learning-and-deep-learning-directions)
9.  [Datasets and data strategy](#9-datasets-and-data-strategy)
10. [Evaluation, validation, and
    reproducibility](#10-evaluation-validation-and-reproducibility)
11. [Potential future work and novel research
    directions](#11-potential-future-work-and-novel-research-directions)
12. [Suggested project milestones](#12-suggested-project-milestones)
13. [Example project structure](#13-example-project-structure)
14. [Tools and Python ecosystem](#14-tools-and-python-ecosystem)
15. [Clinical, ethical, and technical
    limitations](#15-clinical-ethical-and-technical-limitations)
16. [Selected references and
    resources](#16-selected-references-and-resources)

------------------------------------------------------------------------

## 1. Project overview

A phonocardiogram (PCG) is a time-varying acoustic signal recorded from
the chest. It contains the familiar first and second heart sounds (S1
and S2), and may contain additional sounds, murmurs, clicks, snaps, and
other acoustic events. PCG analysis combines digital signal processing,
physiology-informed interpretation, and statistical learning.

A complete research system can perform the following tasks:

-   Import, inspect, and validate audio recordings.
-   Assess signal quality and identify unusable or noisy segments.
-   Suppress noise while preserving clinically relevant acoustic
    content.
-   Detect cardiac cycles and segment S1, systole, S2, and diastole.
-   Extract time-domain, frequency-domain, time-frequency, cepstral, and
    morphology features.
-   Visualize the recording as a waveform, PCG trace, spectrogram,
    scalogram, or synchronized media.
-   Estimate acoustic cycle timing and cautiously derive an approximate
    beat rate when beat detection is reliable.
-   Screen for murmurs or abnormal acoustic patterns using labeled
    datasets.
-   Combine PCG with ECG, PPG, demographic, and clinical information
    when those measurements are actually available.
-   Produce transparent research outputs, uncertainty estimates, and
    reproducible reports.

### Core distinction

A PCG is an **acoustic/mechanical** measurement. An ECG is an
**electrical** measurement. A PCG waveform can be plotted and animated
in an ECG-like layout, but converting PCG audio into an ECG does not
recover the heart's electrical waveform. A true ECG requires ECG
electrodes or a validated ECG data source.

------------------------------------------------------------------------

## 2. What a heart-sound recording can and cannot tell us

### 2.1 Directly observable from PCG

Depending on recording quality, sensor, placement, and duration, PCG can
support measurement or estimation of:

-   S1 and S2 acoustic events.
-   Cardiac-cycle timing and approximate cycle-to-cycle intervals.
-   Systolic and diastolic acoustic intervals after reliable
    segmentation.
-   Heart-sound amplitude, energy, duration, and spectral content.
-   Murmur presence and acoustic descriptors.
-   Additional sound events such as suspected S3/S4, clicks, or snaps.
-   Differences between auscultation locations when multiple sites are
    recorded.
-   Signal quality, noise, clipping, and recording artifacts.

These are signal-derived observations. Their physiological
interpretation requires caution and, for clinical conclusions, expert
review.

### 2.2 Not directly measured by PCG alone

A single heart-sound recording does **not** directly measure:

-   Electrical intervals or morphology such as PR interval, QRS
    duration, or QT/QTc.
-   Oxygen saturation (SpO2).
-   Blood pressure.
-   Blood glucose, cholesterol, troponin, BNP/NT-proBNP, or other blood
    biomarkers.
-   Ejection fraction, chamber volumes, or valve anatomy.
-   Cardiac output or intracardiac pressure.
-   A definitive diagnosis of coronary artery disease, heart failure,
    arrhythmia, or a specific valve lesion.

Such variables require their own validated sensors, laboratory tests,
imaging, clinical examination, or reference diagnosis. A model may
investigate statistical associations with PCG, but it must not present
an unmeasured quantity as if it were directly observed.

------------------------------------------------------------------------

## 3. Potential research problems

The following is a research opportunity map, not a list of conditions
that can all be diagnosed from audio. The most defensible PCG tasks are
sound-event detection, segmentation, murmur characterization, and
screening against clinically established labels.

### 3.1 Signal quality and acquisition problems

1.  Automatic recording-quality classification: usable, degraded, or
    unusable.
2.  Detection of clipping, saturation, dropouts, and microphone
    overload.
3.  Detection of stethoscope movement and contact artifacts.
4.  Detection of speech, breathing, bowel sounds, environmental noise,
    and handling noise.
5.  Robust denoising that preserves S1, S2, murmurs, and transient
    events.
6.  Automatic identification of recording location or sensor type, where
    labels exist.
7.  Detection of incorrect sensor placement or weak chest contact.
8.  Estimation of signal-to-noise ratio and confidence in downstream
    predictions.
9.  Comparison of smartphone microphones, electronic stethoscopes, and
    contact sensors.
10. Calibration and normalization across devices and recording sessions.

### 3.2 Cardiac-cycle and event detection

1.  S1 detection and localization.
2.  S2 detection and localization.
3.  Systolic interval estimation.
4.  Diastolic interval estimation.
5.  Full cardiac-cycle segmentation.
6.  Beat-to-beat interval estimation.
7.  Approximate heart-rate estimation from reliable cycle detections.
8.  Detection of missed, duplicated, or uncertain cycle detections.
9.  Detection of extra heart sounds and transient events.
10. Detection of split S1 or split S2 patterns where the recording
    supports it.
11. Detection and characterization of clicks, opening snaps, and other
    acoustic events.
12. Cycle-level variability and rhythm irregularity screening.
13. Comparison of cycle timing across auscultation sites.
14. Automatic segmentation confidence scoring.

**Caution:** A PCG-derived rate is not interchangeable with ECG-derived
heart rate. S1/S2 sub-events can be mistaken for separate beats;
validate cycle detection against expert annotations or synchronized
ECG/PPG.

### 3.3 Murmur and valve-related research

Potential tasks include:

-   Murmur presence/absence/uncertain classification.
-   Murmur timing: systolic, diastolic, continuous, or uncertain.
-   Murmur timing subtype: early, mid, or late systolic/diastolic when
    annotations support it.
-   Murmur shape: crescendo, decrescendo, crescendo-decrescendo,
    plateau, or other annotated pattern.
-   Murmur pitch/frequency-band characterization.
-   Murmur quality descriptors such as blowing, harsh, or musical, if
    clinically annotated.
-   Murmur grade estimation, only when reliable expert grading is
    available.
-   Murmur localization by auscultation site.
-   Murmur duration and proportion of the cardiac cycle.
-   Murmur segmentation and event boundary detection.
-   Murmur screening with a referral/uncertain option.

Potential associated clinical conditions to investigate **only with
suitable clinical labels**:

  -----------------------------------------------------------------------
  Condition / phenotype   Possible PCG research   Important limitation
                          task                    
  ----------------------- ----------------------- -----------------------
  Aortic stenosis         Murmur screening or     PCG alone cannot
                          severity association    establish valve area or
                                                  severity

  Aortic regurgitation    Diastolic murmur        Requires clinical/echo
                          characterization        confirmation

  Mitral regurgitation    Systolic murmur         Does not quantify
                          screening               regurgitation reliably
                                                  by itself

  Mitral stenosis         Diastolic murmur        Requires clinical/echo
                          screening               confirmation

  Mitral valve prolapse   Acoustic phenotype      Not a definitive
                          association             diagnostic test

  Pulmonary stenosis      Murmur screening        Requires reference
                                                  diagnosis

  Pulmonary regurgitation Murmur screening        Requires reference
                                                  diagnosis

  Tricuspid regurgitation Murmur screening        Requires reference
                                                  diagnosis

  Ventricular septal      Murmur screening in an  Requires clinical/echo
  defect                  appropriate cohort      confirmation

  Atrial septal defect    Explore acoustic        Many cases may not have
                          associations            a distinctive murmur

  Patent ductus           Continuous-murmur       Requires clinical/echo
  arteriosus              screening               confirmation

  Other congenital heart  Broad abnormal-sound    Broad labels can hide
  disease                 screening               multiple disease
                                                  mechanisms
  -----------------------------------------------------------------------

Avoid claiming that a model can distinguish all these diseases unless
the dataset contains adequate numbers of patients with each
independently confirmed diagnosis.

### 3.4 Other cardiac and cardiopulmonary research questions

These are possible research targets, but many need ECG,
echocardiography, clinical records, or other modalities:

-   S3/S4 detection and association with ventricular filling or
    stiffness.
-   Acoustic patterns associated with heart failure phenotypes.
-   PCG changes before/after an intervention or treatment.
-   Valve-prosthesis sound characterization and longitudinal change.
-   Post-operative or post-procedure acoustic monitoring.
-   Pulmonary hypertension association studies using PCG plus clinical
    reference data.
-   Cardiomyopathy phenotype association studies with imaging/clinical
    labels.
-   Congenital heart disease screening in pediatric cohorts.
-   Cardiorespiratory sound separation and joint heart/lung sound
    analysis.
-   Heart sound changes with posture, exercise, respiration, or
    activity.
-   Longitudinal acoustic change detection.

### 3.5 Patient-level variables and demographic subgroup research

Potential metadata or subgroup variables include:

-   Age and age group.
-   Sex or gender, using the source dataset's exact definition.
-   Height, weight, and body-mass index (BMI), if recorded.
-   Pediatric versus adult population.
-   Pregnancy status, where ethically and clinically appropriate and
    available.
-   Auscultation location (aortic, pulmonary, tricuspid, mitral, other).
-   Body position and activity state.
-   Recording device, sensor, operator, site, and environment.
-   Relevant symptoms, medical history, medications, and clinical
    outcome labels.

These variables are not necessarily inferable from the audio. They
should be treated as metadata supplied by a valid source. Investigate
subgroup performance and fairness rather than assuming demographic
attributes can be predicted from PCG.

### 3.6 Biomarker and physiological association studies

A PCG-focused project can study whether acoustic features are associated
with independently measured biomarkers. Examples include:

  -----------------------------------------------------------------------
  Variable                Actual measurement      Possible PCG research
                          source                  question
  ----------------------- ----------------------- -----------------------
  Heart rate              ECG, PPG, or validated  How closely does PCG
                          beat reference          cycle rate agree?

  HRV metrics             Preferably ECG NN       Does PCG-derived timing
                          intervals; validated    agree under controlled
                          PPG alternatives        conditions?

  Blood pressure          Cuff or validated       Is there a reproducible
                          continuous BP device    association with PCG
                                                  features?

  SpO2                    Pulse oximeter          Do PCG features add
                                                  predictive information
                                                  in a multimodal model?

  BNP / NT-proBNP         Laboratory assay        Are acoustic patterns
                                                  associated with
                                                  heart-failure status or
                                                  biomarker levels?

  Troponin                Laboratory assay        Do PCG features add
                                                  value to a clinically
                                                  defined acute-care
                                                  model?

  Lipids / glucose /      Laboratory assay        Are there cohort-level
  HbA1c                                           associations after
                                                  confounder adjustment?

  Ejection fraction       Echocardiography or     Can PCG features
                          validated imaging       support an association
                                                  model, not replace
                                                  imaging?

  Valve area /            Echocardiography        Can murmur features
  regurgitation grade                             correlate with
                                                  independently graded
                                                  valve disease?

  Respiratory rate        Respiratory sensor or   Can synchronized audio
                          validated reference     support joint
                                                  cardiorespiratory
                                                  analysis?
  -----------------------------------------------------------------------

**Research rule:** A correlation is not proof that PCG measures the
biomarker. Report the reference measurement, timing, confounders,
missingness, and uncertainty. Avoid using a model's output as a
substitute for the reference test.

### 3.7 Screening and decision-support problems

1.  Normal / abnormal / uncertain screening.
2.  Murmur referral prioritization.
3.  Quality-aware abstention: return "cannot assess" for poor
    recordings.
4.  Multi-site screening and site-level evidence aggregation.
5.  Longitudinal change alerts.
6.  Clinician-facing decision support with evidence and uncertainty.
7.  Pediatric screening workflows.
8.  Low-resource and remote-care screening workflows.
9.  Human-in-the-loop review prioritization.
10. Triage support evaluated for sensitivity, specificity, and clinical
    consequences.

------------------------------------------------------------------------

## 4. Audio visualization: waveform, PCG, spectrogram, ECG-style views, and video

### 4.1 Recommended visual representations

  -----------------------------------------------------------------------
  View                    What it displays        Research use
  ----------------------- ----------------------- -----------------------
  Raw waveform            Amplitude versus time   Inspect cycles,
                                                  transients, clipping,
                                                  and pauses

  Filtered PCG waveform   Amplitude after a       Highlight a frequency
                          documented filter       range or reduce
                                                  interference

  Envelope plot           Smoothed                Candidate event and
                          amplitude/energy        cycle detection

  Spectrogram (STFT)      Frequency versus time,  Murmur and transient
                          color = energy          frequency analysis

  Log-mel spectrogram     Perceptually spaced     CNN input
                          frequency bands         representation

  MFCC plot               Cepstral coefficients   Compact acoustic
                          over time               feature representation

  Wavelet scalogram       Time-frequency detail   Non-stationary
                          at multiple scales      transient analysis

  Hilbert/envelope view   Signal amplitude        S1/S2 candidate
                          envelope                localization

  Segmented PCG           S1, systole, S2,        Cycle timing and
                          diastole labels         segmentation validation

  Cycle-aligned plot      Multiple cycles aligned Compare beat morphology
                          to S1 or another        
                          landmark                

  Frequency spectrum /    Average power versus    Dominant bands and
  PSD                     frequency               noise characterization

  3D spectrogram          Time, frequency, and    Exploratory
                          magnitude               presentation; usually
                                                  less useful than 2D

  PCG with ECG overlay    Synchronized acoustic   Electromechanical
                          and electrical traces   timing research, if
                                                  both sensors exist
  -----------------------------------------------------------------------

### 4.2 ECG-style graphical display

You can render PCG as a scrolling trace with a grid, time axis,
amplitude axis, labels, and moving cursor---visually similar to an ECG
monitor. Label it **PCG waveform**, not ECG.

A genuine synchronized ECG + PCG display is possible when both
recordings are collected simultaneously with a shared clock or reliable
synchronization markers. This enables studies of:

-   ECG R-peak to S1 timing (pre-ejection period-related research, with
    careful definitions).
-   Electrical-to-acoustic timing.
-   Beat matching between ECG and PCG.
-   Electromechanical delay and its variability.
-   Joint event detection.

Do not infer an ECG waveform by transforming PCG audio.

### 4.3 Turning audio into a graphical video

A video can be generated from the audio for demonstration, education,
annotation, or review. A practical video layout may contain:

1.  A scrolling PCG waveform.
2.  A synchronized spectrogram.
3.  Current timestamp and elapsed time.
4.  Detected S1/S2 markers, if validated.
5.  A PCG amplitude/envelope panel.
6.  Optional ECG/PPG panels only if those signals were separately
    recorded.
7.  Audio playback synchronized to the visual cursor.
8.  A legend and a visible "research visualization---not a diagnosis"
    notice.

Possible output formats:

-   Static PNG figures for papers.
-   SVG figures for scalable publication graphics.
-   Animated GIF for quick previews.
-   MP4 for synchronized waveform playback.
-   Interactive HTML dashboard for zoom, pan, filtering, and annotation.

**Important:** Video conversion changes the presentation, not the
underlying information. It does not create new physiological
measurements.

### 4.4 Suggested visualization workflow

1.  Decode the original file and preserve the original sample rate.
2.  Convert to mono only when appropriate; preserve stereo channels if
    they contain meaningful sensor information.
3.  Plot the raw waveform.
4.  Plot the filtered waveform separately and document filter settings.
5.  Generate a spectrogram and/or scalogram.
6.  Add event markers only after detection and validation.
7.  Align all plots to the same time axis.
8.  Export high-resolution figures and, if needed, render a video.
9.  Retain the original audio and metadata so the visualization is
    reproducible.

### 4.5 Example Python snippets

Install a typical scientific audio stack:

``` bash
pip install numpy scipy matplotlib librosa soundfile pandas
```

Load and plot a waveform:

``` python
import librosa
import librosa.display
import matplotlib.pyplot as plt
import numpy as np

audio_path = "heart_sound.wav"
signal, sr = librosa.load(audio_path, sr=None, mono=True)
time = np.arange(len(signal)) / sr

plt.figure(figsize=(14, 3))
plt.plot(time, signal, linewidth=0.5)
plt.xlabel("Time (seconds)")
plt.ylabel("Amplitude")
plt.title("Phonocardiogram (PCG) waveform")
plt.tight_layout()
plt.show()
```

Generate a spectrogram:

``` python
import librosa
import librosa.display
import matplotlib.pyplot as plt
import numpy as np

S = librosa.stft(signal, n_fft=1024, hop_length=128)
S_db = librosa.amplitude_to_db(np.abs(S), ref=np.max)

plt.figure(figsize=(14, 5))
librosa.display.specshow(
    S_db, sr=sr, hop_length=128,
    x_axis="time", y_axis="hz"
)
plt.ylim(0, min(1500, sr / 2))
plt.colorbar(format="%+2.0f dB")
plt.title("PCG spectrogram")
plt.tight_layout()
plt.show()
```

For research figures, record the FFT size, hop length, window, frequency
limits, normalization, and filter settings.

------------------------------------------------------------------------

## 5. Comprehensive feature-extraction catalogue

Feature extraction should be designed around the research question. Not
every feature is useful for every task, and features should be computed
only on signal segments where they are meaningful.

### 5.1 Signal and recording metadata

-   Sampling frequency.
-   Number of channels.
-   Recording duration.
-   Bit depth and encoding.
-   Peak amplitude and peak level (dBFS).
-   RMS amplitude and RMS level.
-   Dynamic range.
-   Clipping/saturation ratio.
-   DC offset.
-   Missing-sample/dropout count.
-   Channel correlation and channel balance.
-   Recording location and sensor type (metadata).
-   Recording session, device, and operator (metadata).
-   Signal-to-noise ratio estimate, with method documented.
-   Usable-recording duration and usable-segment ratio.

### 5.2 Time-domain statistical features

-   Mean and median.
-   Variance and standard deviation.
-   Minimum and maximum.
-   Peak-to-peak amplitude.
-   Root mean square (RMS).
-   Mean absolute value.
-   Mean absolute deviation.
-   Median absolute deviation.
-   Skewness.
-   Kurtosis.
-   Crest factor.
-   Shape factor.
-   Impulse factor.
-   Clearance factor.
-   Zero-crossing rate.
-   Waveform length.
-   Signal energy.
-   Short-time energy.
-   Short-time variance.
-   Envelope mean, variance, and percentiles.
-   Amplitude quantiles.
-   Interquartile range.
-   Autocorrelation peak values and lags.
-   Sample entropy and approximate entropy.
-   Permutation entropy.
-   Hjorth activity, mobility, and complexity.
-   Fractal dimension estimates (method-dependent).

### 5.3 Cardiac-event and cycle features

When S1/S2 segmentation is available or reliably estimated:

-   S1 onset, offset, duration, and peak amplitude.
-   S2 onset, offset, duration, and peak amplitude.
-   S1-to-S2 interval.
-   S2-to-next-S1 interval.
-   Systolic duration.
-   Diastolic duration.
-   Total cycle duration.
-   S1/S2 energy ratio.
-   S1/S2 amplitude ratio.
-   S1/S2 spectral centroid and bandwidth.
-   Cycle-to-cycle duration variability.
-   Cycle-to-cycle amplitude variability.
-   Beat interval median, standard deviation, and robust spread.
-   Approximate acoustic beat rate.
-   Detection confidence and missed-cycle rate.
-   Split-sound timing features, if annotated and supported by signal
    quality.
-   Additional sound event count, duration, and timing.
-   Murmur duration and fraction of systole/diastole.
-   Event-level signal-to-noise ratio.

Do not equate a standard deviation of PCG cycle intervals with clinical
ECG HRV without validating beat correspondence and the interval
definition.

### 5.4 Frequency-domain features

Compute from an explicitly defined segment or window:

-   Power spectral density (PSD).
-   Dominant frequency.
-   Peak frequency.
-   Spectral centroid.
-   Spectral bandwidth.
-   Spectral rolloff (e.g., 85%, 90%, 95%).
-   Spectral flatness.
-   Spectral entropy.
-   Spectral flux.
-   Spectral slope.
-   Spectral spread.
-   Spectral skewness and kurtosis.
-   Band power and relative band power.
-   Low-/high-frequency energy ratios.
-   Harmonic-to-noise ratio (where meaningful).
-   Harmonicity and inharmonicity descriptors.
-   Frequency-band energy ratios.
-   Resonance or peak-band descriptors.
-   Median frequency.
-   Mean frequency.
-   Frequency variance.

Frequency bands should be selected and justified for the sensor,
sampling rate, and research question. Avoid treating one universal band
boundary as clinically definitive.

### 5.5 Time-frequency features

-   Short-time Fourier transform (STFT).
-   Spectrogram energy.
-   Log-mel spectrogram.
-   Mel-frequency filter-bank energies.
-   Continuous wavelet transform (CWT).
-   Discrete wavelet transform (DWT).
-   Wavelet packet decomposition.
-   Wavelet coefficient statistics.
-   Scale-wise energy and entropy.
-   Time-frequency entropy.
-   Spectral flux over time.
-   Local time-frequency peaks.
-   Reassigned spectrogram features (advanced).
-   Synchrosqueezed transforms (advanced).
-   Multi-resolution spectrogram representations.

### 5.6 Cepstral and perceptual features

-   MFCC coefficients (e.g., 1--13 or another validated range).
-   Delta MFCC.
-   Delta-delta MFCC.
-   Log-mel filter-bank coefficients.
-   Cepstral mean and variance.
-   Per-frame MFCC statistics.
-   Segment-level MFCC mean, standard deviation, median, and quantiles.
-   Chroma-like descriptors only if their relevance to PCG is justified;
    they are not automatically meaningful because they are common in
    music analysis.

### 5.7 Nonlinear and complexity features

-   Sample entropy.
-   Approximate entropy.
-   Permutation entropy.
-   Fuzzy entropy.
-   Multiscale entropy.
-   Lempel-Ziv complexity.
-   Detrended fluctuation analysis (DFA).
-   Recurrence quantification features.
-   Correlation dimension estimates.
-   Hurst exponent estimates.
-   Fractal dimension.
-   Poincaré-style interval descriptors, when valid beat intervals
    exist.

These features can be sensitive to record length, noise, parameter
choice, and nonstationarity. Report implementation details and avoid
overinterpreting them physiologically.

### 5.8 Murmur-specific descriptors

When murmurs are present and labels/annotations support analysis:

-   Murmur presence probability.
-   Murmur start and end time.
-   Murmur duration.
-   Murmur timing within systole or diastole.
-   Crescendo/decrescendo profile.
-   Spectral centroid and bandwidth during murmur.
-   Murmur-to-heart-sound energy ratio.
-   Spectral flatness/noisiness.
-   Pitch category or dominant frequency.
-   Temporal continuity.
-   Cycle-to-cycle murmur consistency.
-   Murmur grade prediction (only with suitable expert labels).
-   Murmur location association across auscultation sites.
-   Model uncertainty and abstention score.

### 5.9 Spatial, multi-site, and multi-sensor features

If multiple chest locations or sensors are recorded:

-   Site-specific feature vectors.
-   Cross-site amplitude and spectral differences.
-   Cross-site murmur consistency.
-   Inter-site event timing.
-   Spatial pattern of murmur intensity.
-   Cross-channel correlation/coherence.
-   Sensor agreement and disagreement.
-   Synchronized ECG-PCG event timing.
-   PCG-PPG timing relationships.
-   Cardiorespiratory sound interactions.

Do not compute cross-site or synchronization features from recordings
collected sequentially unless the timing and protocol support the
intended comparison.

### 5.10 Learned deep representations

Instead of hand-crafted features, a model can learn representations
from:

-   Raw waveform windows.
-   STFT magnitude or log spectrogram.
-   Mel spectrogram.
-   Wavelet scalogram.
-   MFCC sequences.
-   Segmented cardiac-cycle tensors.
-   Multi-location feature maps.
-   Self-supervised embeddings.
-   Contrastive embeddings.
-   Transformer tokens or latent representations.

### 5.11 Feature engineering recommendations

-   Compute features at both recording level and cycle/segment level.
-   Preserve units and document normalization.
-   Use patient-level splits before fitting scalers or feature
    selection.
-   Fit feature selection only on training folds.
-   Compare hand-crafted features, learned representations, and hybrid
    approaches.
-   Examine feature stability across devices, locations, and noise
    conditions.
-   Use ablation studies to establish which feature groups add value.
-   Avoid data leakage from multiple recordings of the same patient.
-   Save a feature dictionary and version every extraction pipeline.

------------------------------------------------------------------------

## 6. Biomarkers and patient-level variables

It is useful to separate **PCG-derived acoustic markers** from
**external clinical biomarkers**.

### 6.1 PCG-derived candidate acoustic markers

These are candidate signal descriptors, not established clinical
biomarkers by default:

-   S1 duration and energy.
-   S2 duration and energy.
-   S1/S2 energy ratio.
-   Systolic and diastolic acoustic timing.
-   Cycle interval and variability.
-   Murmur duration, timing, intensity, and spectral profile.
-   Additional sound event count and timing.
-   Spectral entropy and band energy.
-   Signal-quality score.
-   Cross-site acoustic differences.
-   Longitudinal change in acoustic features.

A feature becomes a clinically useful biomarker only after analytical
validity, clinical validity, and clinical utility are established in
appropriate populations.

### 6.2 External biomarkers and reference variables

Potential linked variables include:

-   ECG-derived heart rate and rhythm.
-   ECG intervals and morphology.
-   PPG-derived pulse rate and pulse waveform indices.
-   Cuff blood pressure.
-   SpO2.
-   Respiratory rate.
-   Echocardiographic ejection fraction and valve measurements.
-   BNP/NT-proBNP.
-   Troponin.
-   Lipid profile.
-   Glucose and HbA1c.
-   Renal function and other laboratory measures when clinically
    justified.
-   Clinical diagnosis, symptoms, and outcomes.

These must be collected from valid sources and synchronized
appropriately. They cannot be extracted from a PCG file merely by
applying more signal-processing algorithms.

------------------------------------------------------------------------

## 7. Recommended end-to-end research pipeline

### Stage 1: Data intake and audit

-   Preserve an immutable copy of every original file.
-   Read sample rate, channels, duration, encoding, and metadata.
-   Verify that the audio can be decoded.
-   Check for clipping, silence, corrupted segments, and abnormal
    duration.
-   Create a patient/recording manifest.
-   Document consent, provenance, permitted use, and dataset license.

### Stage 2: Preprocessing

-   Convert to a consistent analysis representation while retaining
    original files.
-   Resample only when justified; document the target rate.
-   Remove DC offset if present.
-   Apply carefully selected filters.
-   Compare raw and processed signals to ensure relevant murmurs/events
    are not removed.
-   Detect and annotate noisy intervals.
-   Use denoising only after evaluating signal distortion.
-   Normalize per recording or per dataset only within a leakage-safe
    training pipeline.

### Stage 3: Signal quality and segmentation

-   Build a signal-quality model or rule-based quality gate.
-   Detect S1/S2 and cardiac cycles.
-   Use expert annotations where available.
-   Compare automatic segmentation with manual labels.
-   Include uncertain/unsegmented states rather than forcing every
    segment into a class.
-   Quantify segmentation error.

### Stage 4: Feature extraction and visualization

-   Generate waveform, envelope, spectrogram, and scalogram views.
-   Extract time, frequency, time-frequency, cepstral, nonlinear, and
    event-based features.
-   Save features at segment, cycle, recording, and patient levels as
    appropriate.
-   Store feature names, units, parameters, and software versions.

### Stage 5: Modeling

Start with interpretable baselines:

-   Logistic regression.
-   Linear or RBF support vector machine.
-   Random forest.
-   Gradient-boosted trees.
-   k-nearest neighbors as a simple baseline.

Then evaluate:

-   1D CNN on raw waveform.
-   2D CNN on spectrograms.
-   CNN + LSTM/GRU.
-   Temporal convolutional networks.
-   Transformer-based models.
-   Self-supervised pretraining.
-   Multi-instance learning for multiple recordings per patient.
-   Multimodal models if aligned external data exist.

### Stage 6: Evaluation

-   Split by patient/subject, not random audio segment.
-   Keep an external test cohort or site when possible.
-   Report sensitivity, specificity, precision, F1, AUROC, AUPRC, and
    confusion matrix.
-   Report calibration and confidence intervals.
-   Analyze performance by age, sex, site, device, and noise level where
    sample sizes allow.
-   Evaluate "uncertain / refer / cannot assess" behavior.
-   Conduct error analysis with clinical experts.

### Stage 7: Reporting and deployment

-   Provide model version, data provenance, and preprocessing details.
-   Explain which signal regions influenced predictions.
-   Show uncertainty and quality warnings.
-   Avoid diagnostic language unless the system has the necessary
    validation and regulatory authorization.
-   Monitor performance drift after deployment.
-   Maintain privacy, access controls, and audit logs.

------------------------------------------------------------------------

## 8. Machine-learning and deep-learning directions

  -----------------------------------------------------------------------
  Research task           Candidate methods       Suggested output
  ----------------------- ----------------------- -----------------------
  Signal quality          Random forest, CNN,     Usable / degraded /
                          autoencoder             unusable

  S1/S2 segmentation      Hidden Markov model,    Event boundaries or
                          CNN, U-Net, temporal    state sequence
                          model                   

  Murmur detection        SVM, XGBoost, CNN       Murmur / no murmur /
                                                  uncertain

  Murmur characterization CNN, CRNN, transformer  Timing, shape, pitch,
                                                  quality

  Normal/abnormal         Logistic regression,    Screening score and
  screening               XGBoost, CNN            uncertainty

  Anomaly detection       Autoencoder, one-class  Anomaly score
                          SVM, self-supervised    
                          model                   

  Multi-site analysis     Attention, late fusion, Patient-level screening
                          graph models            output

  Longitudinal monitoring Temporal CNN, RNN,      Change score over time
                          transformer             

  Explainability          SHAP, integrated        Feature or time-region
                          gradients, saliency     evidence

  On-device screening     Quantized CNN,          Efficient local
                          MobileNet-like models   inference
  -----------------------------------------------------------------------

### Model-development principles

-   Establish a transparent baseline before proposing a complex
    architecture.
-   Use patient-level cross-validation.
-   Avoid treating many segments from one patient as independent
    subjects.
-   Address class imbalance with training-only methods and report
    prevalence-aware metrics.
-   Evaluate external generalization.
-   Calibrate probabilities.
-   Include a reject/abstain option for poor-quality or
    out-of-distribution recordings.
-   Compare models under identical splits and preprocessing.
-   Do not claim clinical superiority from accuracy alone.

------------------------------------------------------------------------

## 9. Datasets and data strategy

Public datasets provide a starting point, but each has its own
population, label definition, acquisition protocol, and license.

### 9.1 PhysioNet/CinC Challenge 2016

-   **Resource:** [PhysioNet Challenge
    2016](https://physionet.org/content/challenge-2016/1.0.0/)
-   **Focus:** Normal/abnormal heart-sound recording classification.
-   **Data:** Recordings from multiple contributing databases and
    acquisition environments.
-   **Research use:** Baseline classification, robustness, signal
    quality, and cross-source generalization.
-   **Caution:** Abnormal labels are broad and do not provide a specific
    diagnosis for every abnormal recording. The recordings vary in
    duration and quality.

### 9.2 CirCor DigiScope / PhysioNet Challenge 2022

-   **Resource:** [CirCor DigiScope PCG
    Dataset](https://physionet.org/content/circor-heart-sound/1.0.3/)
-   **Focus:** Pediatric heart sounds and murmur
    detection/characterization.
-   **Data:** Multiple auscultation locations, patient metadata, murmur
    annotations, and S1/S2 segmentation information.
-   **Research use:** Murmur detection, murmur
    timing/shape/pitch/quality, segmentation, and multi-site modeling.
-   **Caution:** It is a pediatric cohort; performance should not
    automatically be generalized to adults. Check the dataset's current
    release, split definitions, and license before use.

### 9.3 Dataset checklist

For every dataset, document:

-   Patient count and recording count.
-   Age distribution and population.
-   Device and sampling frequency.
-   Auscultation locations.
-   Recording duration.
-   Label definitions and annotator expertise.
-   Whether labels are patient-level, recording-level, or segment-level.
-   Missing metadata and missing labels.
-   Class imbalance.
-   Patient overlap across splits.
-   License, access conditions, and citation requirements.
-   Known acquisition and population limitations.

### 9.4 Data strategy

A strong study should use:

1.  A development dataset for model design.
2.  Patient-level internal validation.
3.  An independent dataset or site for external validation.
4.  Expert review of a representative subset of errors.
5.  A documented mapping between label definitions across datasets.

Do not merge datasets blindly. Differences in age, clinical setting,
recording device, label criteria, and prevalence can create misleading
performance.

------------------------------------------------------------------------

## 10. Evaluation, validation, and reproducibility

### 10.1 Classification metrics

-   Sensitivity / recall.
-   Specificity.
-   Precision / positive predictive value.
-   Negative predictive value.
-   F1 score.
-   Balanced accuracy.
-   AUROC.
-   AUPRC.
-   Confusion matrix.
-   Calibration curve and Brier score.
-   Decision-curve analysis where clinically appropriate.

### 10.2 Segmentation metrics

-   Event sensitivity and positive predictive value.
-   Boundary timing error.
-   Onset/offset absolute error.
-   Intersection over union (IoU).
-   Dice coefficient.
-   State-sequence accuracy.
-   Cycle-level detection error.

### 10.3 Heart-rate / interval agreement

Compare PCG-derived cycle timing against a suitable reference such as
synchronized ECG or validated PPG:

-   Mean absolute error.
-   Root mean squared error.
-   Bias and limits of agreement.
-   Percentage of recordings within a pre-defined tolerance.
-   Beat matching precision/recall.
-   Failure rate and uncertainty coverage.

Correlation alone is not sufficient to establish agreement.

### 10.4 Essential validation safeguards

-   Patient-wise split, not segment-wise random split.
-   No preprocessing or feature-selection leakage from test data.
-   Confidence intervals and sample counts.
-   External validation across devices and clinical sites.
-   Subgroup performance analysis.
-   Robustness to noise and recording placement.
-   Calibration and uncertainty assessment.
-   Comparison with a clinically relevant baseline.
-   Predefined primary endpoint and analysis plan.
-   Transparent reporting of exclusions and failed recordings.

------------------------------------------------------------------------

## 11. Potential future work and novel research directions

The following ideas can form individual papers, thesis chapters, or a
longer research program. Novelty must be confirmed through a current
literature review and a clear comparison with prior work.

### 11.1 Quality-aware heart-sound intelligence

**Problem:** Many algorithms produce a prediction even when the
recording is too noisy to interpret.

**Proposed direction:** - Train a quality model to identify noise, poor
contact, clipping, and unusable recordings. - Jointly estimate signal
quality and murmur confidence. - Add a reject option when quality is
inadequate. - Test whether quality-aware inference reduces unsafe false
reassurance.

**Potential contribution:** A more reliable screening workflow rather
than a classifier that always returns an answer.

### 11.2 Explainable PCG classification

**Problem:** Deep models can classify a recording without showing which
acoustic events support the output.

**Proposed direction:** - Use time-region saliency, integrated
gradients, SHAP, and event-level evidence. - Highlight the relevant
cycle, murmur interval, or frequency region. - Compare explanations with
expert annotations. - Test explanation stability under noise and small
perturbations.

**Potential contribution:** Evidence-linked outputs that clinicians and
researchers can inspect.

### 11.3 Self-supervised learning for unlabeled PCG

**Problem:** Expert-labeled heart sound datasets are limited and
expensive to annotate.

**Proposed direction:** - Pretrain on unlabeled PCG using masked
reconstruction, contrastive learning, or temporal prediction. -
Fine-tune on smaller expert-labeled cohorts. - Compare performance and
data efficiency against supervised baselines.

**Potential contribution:** Better use of large collections of unlabeled
recordings.

### 11.4 Domain generalization across devices and hospitals

**Problem:** A model trained on one electronic stethoscope or hospital
may fail on another.

**Proposed direction:** - Train and test across device/site
partitions. - Explore domain adaptation, feature alignment, and
invariant representations. - Use leave-one-device-out and
leave-one-site-out evaluation. - Quantify performance degradation and
recovery.

**Potential contribution:** Evidence of robustness beyond a single
dataset.

### 11.5 Multimodal PCG + ECG + PPG analysis

**Problem:** PCG, ECG, and PPG capture different aspects of
cardiovascular activity.

**Proposed direction:** - Collect synchronized signals. - Match cardiac
cycles across modalities. - Study electrical-to-acoustic and
acoustic-to-peripheral-pulse timing. - Fuse modality-specific
embeddings. - Evaluate whether fusion improves a clearly defined
endpoint.

**Potential contribution:** A richer electromechanical and hemodynamic
research representation.

**Constraint:** Do not synthesize missing ECG or PPG channels from PCG
and treat them as real measurements.

### 11.6 Longitudinal personal baseline modeling

**Problem:** Population-level thresholds may not capture meaningful
changes within an individual.

**Proposed direction:** - Collect repeated recordings using a consistent
device and protocol. - Learn a personal acoustic baseline. - Detect
deviations in cycle timing, murmur features, or signal morphology. -
Separate physiological change from sensor-placement and device changes.

**Potential contribution:** Personalized change detection, subject to
clinical validation.

### 11.7 Pediatric--adult transfer learning

**Problem:** Pediatric and adult cardiac acoustics and disease
distributions differ.

**Proposed direction:** - Train on one population and test on another. -
Quantify domain shift. - Explore age-conditioned models and transfer
learning. - Validate separately in pediatric and adult cohorts.

**Potential contribution:** A clear analysis of population-specific
generalization.

### 11.8 Generative AI for denoising and augmentation

**Problem:** Noisy recordings and rare murmur classes can limit model
training.

**Proposed direction:** - Explore diffusion models, variational
autoencoders, or GANs for augmentation and denoising. - Measure whether
generated samples preserve clinically relevant event timing and
morphology. - Use expert review and signal-level fidelity metrics. -
Test downstream benefit on held-out real recordings.

**Potential contribution:** Better data efficiency without relying on
unrealistic synthetic sounds.

**Constraint:** Synthetic samples must never be counted as independent
patients or used as a substitute for external clinical validation.

### 11.9 Few-shot and rare-condition learning

**Problem:** Some conditions have very few labeled examples.

**Proposed direction:** - Prototypical networks, metric learning,
few-shot adaptation, and class-aware representation learning. - Evaluate
performance as the number of labeled patients changes. - Include
uncertainty for unseen or underrepresented conditions.

**Potential contribution:** More useful research on rare acoustic
phenotypes.

### 11.10 Federated and privacy-preserving PCG learning

**Problem:** Multi-hospital data may not be shareable centrally.

**Proposed direction:** - Train models across institutions without
transferring raw audio. - Compare federated learning with centralized
and local baselines. - Evaluate privacy, communication cost, fairness,
and site generalization.

**Potential contribution:** A collaborative research framework for
sensitive clinical audio.

### 11.11 Lightweight edge and smartphone inference

**Problem:** Many low-resource settings cannot rely on cloud
connectivity or expensive hardware.

**Proposed direction:** - Quantization, pruning, distillation, and
compact architectures. - On-device quality assessment and inference. -
Measure latency, memory, energy use, and accuracy. - Include offline
operation and secure data handling.

**Potential contribution:** A practical point-of-care research
prototype.

### 11.12 Acoustic digital biomarkers and external clinical outcomes

**Problem:** PCG-derived descriptors are not yet interchangeable with
established clinical biomarkers.

**Proposed direction:** - Link PCG features with synchronized
echocardiography, ECG, laboratory measurements, and clinical outcomes. -
Predefine a small number of hypotheses. - Adjust for age, sex,
comorbidities, device, and acquisition site. - Validate associations in
an independent cohort.

**Potential contribution:** Evidence for or against specific acoustic
markers as candidate digital biomarkers.

### 11.13 Multi-location spatial murmur modeling

**Problem:** A murmur may have different acoustic strength and quality
across auscultation sites.

**Proposed direction:** - Use standardized multi-site recordings. -
Model location-specific features and cross-site relationships. - Explore
attention or graph-based fusion. - Compare single-site and multi-site
performance.

**Potential contribution:** A spatial representation of cardiac acoustic
patterns.

### 11.14 Human-in-the-loop annotation and active learning

**Problem:** Manual segmentation and murmur annotation require expert
time.

**Proposed direction:** - Select uncertain or informative examples for
expert review. - Use active learning to prioritize annotation. - Track
annotator agreement. - Measure annotation effort saved and downstream
model performance.

**Potential contribution:** A more efficient and transparent annotation
pipeline.

### 11.15 Causal and counterfactual research

**Problem:** Predictive association does not explain why a sound pattern
occurs or whether an intervention changes it.

**Proposed direction:** - Develop carefully specified causal hypotheses
using clinical context. - Separate confounders from mediators. - Use
longitudinal or intervention data where available. - Treat
counterfactual explanations as hypotheses, not clinical facts.

**Potential contribution:** Stronger physiological interpretation than
correlation-only modeling.

### 11.16 Standardized PCG benchmark and reproducibility framework

**Problem:** Results are difficult to compare when splits,
preprocessing, labels, and metrics differ.

**Proposed direction:** - Publish fixed patient-level splits where
licensing permits. - Define standardized preprocessing and feature
baselines. - Include quality-aware and uncertainty-aware metrics. -
Provide reproducible code and model cards. - Evaluate external datasets
using a consistent protocol.

**Potential contribution:** A reusable benchmark that supports fair
comparison across studies.

------------------------------------------------------------------------

## 12. Suggested project milestones

A practical progression is:

  -----------------------------------------------------------------------
  Phase                   Work package            Deliverable
  ----------------------- ----------------------- -----------------------
  1                       Literature review and   Research protocol
                          research question       

  2                       Dataset acquisition and Dataset manifest
                          audit                   

  3                       Audio preprocessing and Cleaned/annotated
                          quality assessment      signal pipeline

  4                       Waveform and            Reproducible figures
                          time-frequency          
                          visualization           

  5                       S1/S2 segmentation      Event labels and
                                                  segmentation evaluation

  6                       Feature extraction      Versioned feature table

  7                       Baseline machine        Baseline results
                          learning                

  8                       Deep learning and       Model comparison
                          ablation                

  9                       External and subgroup   Generalization report
                          validation              

  10                      Explainability and      Evidence-oriented
                          uncertainty             outputs

  11                      Prototype and           Research demo
                          documentation           

  12                      Manuscript preparation  Paper, code, and
                                                  reproducibility package
  -----------------------------------------------------------------------

### Suggested first research project

A manageable and scientifically defensible first study is:

**"Quality-Aware Heart Murmur Screening and Acoustic Feature Analysis
Using Phonocardiogram Signals."**

Possible objectives:

1.  Assess recording quality and identify unusable segments.
2.  Visualize PCG waveforms and time-frequency representations.
3.  Segment S1, systole, S2, and diastole using available annotations.
4.  Extract time-domain, frequency-domain, MFCC, and cardiac-cycle
    features.
5.  Train interpretable baseline models for murmur screening.
6.  Compare with a CNN-based spectrogram model.
7.  Evaluate patient-wise and external generalization.
8.  Add uncertainty-aware referral or abstention.
9.  Analyze errors by recording location, age group, and device where
    data support it.

This scope is more achievable than attempting to diagnose many
individual diseases from one short recording.

------------------------------------------------------------------------

## 13. Example project structure

``` text
heart-sound-intelligence/
│
├── README.md
├── LICENSE
├── requirements.txt
├── configs/
│   ├── preprocessing.yaml
│   ├── features.yaml
│   └── training.yaml
│
├── data/
│   ├── raw/                 # Original recordings; do not modify
│   ├── interim/             # Decoded/cleaned working files
│   ├── processed/           # Model-ready signals
│   ├── annotations/         # S1/S2 and murmur annotations
│   └── metadata/            # De-identified metadata and manifests
│
├── notebooks/
│   ├── 01_audio_audit.ipynb
│   ├── 02_visualization.ipynb
│   ├── 03_preprocessing.ipynb
│   ├── 04_segmentation.ipynb
│   ├── 05_feature_extraction.ipynb
│   └── 06_model_experiments.ipynb
│
├── src/
│   ├── io/
│   ├── quality/
│   ├── preprocessing/
│   ├── segmentation/
│   ├── visualization/
│   ├── features/
│   ├── models/
│   ├── evaluation/
│   └── reporting/
│
├── tests/
├── models/
├── outputs/
│   ├── figures/
│   ├── tables/
│   ├── audio/
│   └── videos/
│
└── docs/
    ├── data_dictionary.md
    ├── annotation_protocol.md
    ├── experiment_log.md
    └── model_card.md
```

Never commit identifiable patient audio or metadata to a public
repository. Use access-controlled storage and a `.gitignore` for private
data.

------------------------------------------------------------------------

## 14. Tools and Python ecosystem

  Purpose                     Candidate tools
  --------------------------- ------------------------------------------------
  Audio decoding              `soundfile`, `librosa`, `torchaudio`, `ffmpeg`
  Signal processing           `scipy.signal`, `numpy`, `PyWavelets`
  Visualization               `matplotlib`, `plotly`, `librosa.display`
  Tabular data                `pandas`, `polars`
  Classical ML                `scikit-learn`, `xgboost`, `lightgbm`
  Deep learning               `PyTorch`, `TensorFlow/Keras`
  Biomedical signal formats   `wfdb`
  Explainability              `shap`, Captum
  Experiment tracking         MLflow, Weights & Biases
  Interactive dashboard       Streamlit, Dash
  Video rendering             `matplotlib.animation`, `ffmpeg`, OpenCV
  Testing                     `pytest`
  Reproducibility             Git, DVC, environment lock files

Use only the tools needed for the chosen research question. Keep
preprocessing and feature extraction in reusable functions rather than
relying exclusively on notebook cells.

------------------------------------------------------------------------

## 15. Clinical, ethical, and technical limitations

1.  **PCG is not ECG.** An ECG-style plot is a display choice; it does
    not turn acoustic data into electrical data.
2.  **Audio alone has limited diagnostic scope.** A murmur may suggest a
    reason for further assessment but does not establish a specific
    valve diagnosis.
3.  **Recording quality matters.** Sensor placement, pressure, clothing,
    room noise, movement, and device response can alter the signal.
4.  **Population matters.** Pediatric and adult recordings should not be
    assumed interchangeable.
5.  **Labels matter.** "Abnormal" may be a broad referral label, not a
    confirmed disease class.
6.  **Patient-level leakage is dangerous.** Multiple recordings from one
    person must not appear across training and test partitions.
7.  **Preprocessing can remove information.** A filter that reduces
    noise may also suppress a low-frequency or high-frequency event of
    interest.
8.  **Synthetic data are not clinical evidence.** Generated audio needs
    physiological and expert validation.
9.  **Fairness must be evaluated.** Report subgroup performance and
    investigate missing or underrepresented populations.
10. **Privacy is essential.** Clinical recordings and linked metadata
    may be identifiable or sensitive.
11. **Clinical deployment requires validation.** Research prototypes are
    not medical devices and should not be used to make independent
    treatment decisions.
12. **Uncertainty should be visible.** A system should be allowed to say
    "uncertain" or "recording unsuitable."

A useful research system should support clinical assessment, not replace
a qualified clinician or validated diagnostic tests.

------------------------------------------------------------------------

## 16. Selected references and resources

### Public datasets and benchmarks

1.  **PhysioNet/CinC Challenge 2016 --- Classification of Heart Sound
    Recordings**\
    https://physionet.org/content/challenge-2016/1.0.0/\
    Useful for normal/abnormal screening and multi-source robustness
    experiments.

2.  **CirCor DigiScope Phonocardiogram Dataset --- PhysioNet**\
    https://physionet.org/content/circor-heart-sound/1.0.3/\
    Useful for pediatric murmur research, multiple auscultation
    locations, annotations, and segmentation.

3.  **George B. Moody PhysioNet Challenge 2022 --- Heart Murmur
    Detection**\
    https://physionet.org/content/challenge-2022/1.0.0/\
    Useful for understanding murmur and outcome labels, challenge
    design, and evaluation.

### Reviews and research context

4.  **Deep Learning in Heart Sound Analysis: From Techniques to Clinical
    Applications**\
    https://pmc.ncbi.nlm.nih.gov/articles/PMC11461928/\
    A review of datasets, preprocessing, feature extraction,
    deep-learning methods, clinical applications, and limitations.

5.  **A Comprehensive Survey on Heart Sound Analysis in the Deep
    Learning Era**\
    https://mcml.ai/publications/rcn%2B24/\
    Reviews deep-learning approaches and research directions.

6.  **Generative Artificial Intelligence for Heart Sound Analysis: From
    Model Architectures to Clinical Applications**\
    https://doi.org/10.1016/j.iswa.2026.200637\
    Reviews generative approaches for augmentation, denoising, anomaly
    detection, and representation learning.

7.  **A Systematic Review of Machine Learning Approaches for
    Phonocardiogram Classification**\
    https://doi.org/10.1080/10255842.2026.2690183\
    Discusses PCG acquisition, preprocessing, segmentation, feature
    representations, classification, and evaluation challenges.

### Citation and reproducibility notes

-   Cite the dataset paper and version used, not only the landing page.
-   Follow the dataset license and access terms.
-   Record the exact download version and checksum.
-   Cite software packages and model architectures.
-   Document train/validation/test split logic and random seeds.
-   Make code, configuration files, and non-sensitive derived artifacts
    available when permitted.

------------------------------------------------------------------------

## Final research principle

The strongest heart-sound research is not simply a model with high
accuracy. It is a reproducible pipeline that:

1.  Preserves and understands the original acoustic signal.
2.  Distinguishes direct PCG measurements from external biomarkers.
3.  Uses physiologically meaningful segmentation and features.
4.  Trains and tests on independent patients and, ideally, independent
    sites.
5.  Reports uncertainty, limitations, and subgroup performance.
6.  Produces evidence that can be reviewed by domain experts.
7.  Makes a clearly defined contribution to research or clinical
    workflow.

**Recommended starting point:** Build a reliable PCG visualization,
quality-assessment, S1/S2 segmentation, and feature-extraction pipeline
before moving to disease classification. This foundation will make later
research questions more testable and the resulting findings more
credible.
