# Smartphone-Only Heart-Rate Estimation: Camera, Microphone & Sensor Fusion

> Research map, literature review, public datasets, baseline methods,
> evaluation plan, and implementation roadmap for estimating heart rate
> using commodity smartphone hardware.

**Status:** Research planning document\
**Scope:** Rear-camera fingertip PPG, front-camera facial rPPG, built-in
microphone phonocardiography (PCG), and optional camera--microphone
fusion\
**Last reviewed:** 2026-11-03

------------------------------------------------------------------------

## 1. Project overview

This project investigates whether a commodity smartphone can estimate
heart rate without a dedicated wearable or external medical sensor,
using:

1.  **Camera PPG:** fingertip placed over the rear camera and LED flash.
2.  **Camera rPPG:** facial video recorded by the front camera, without
    physical contact.
3.  **Microphone PCG:** built-in microphone placed against the chest to
    record acoustic heart sounds.
4.  **Multimodal fusion:** combine independent estimates or features
    from camera and microphone streams, with ECG used as ground truth
    during controlled validation.

These modalities measure different physiological phenomena:

  ------------------------------------------------------------------------------
  Modality          Physical signal          Typical placement What is estimated
  ----------------- ------------------------ ----------------- -----------------
  Fingertip PPG     Optical changes caused   Finger over rear  Peripheral pulse
                    by pulsatile             camera + flash    rate
                    blood-volume changes                       

  Facial rPPG       Small                    Front camera      Peripheral pulse
                    skin-reflectance/color   facing face       rate
                    changes associated with                    
                    blood pulsation                            

  PCG               Acoustic heart sounds,   Phone microphone  Cardiac-cycle
                    particularly S1 and S2   against chest     rate /
                                                               heart-sound
                                                               timing

  ECG reference     Cardiac electrical       Research ECG      Electrical heart
                    depolarization           electrodes        rate and beat
                                                               timing
  ------------------------------------------------------------------------------

**Important:** PCG heart-sound cycles and peripheral pulse beats are
related but are not interchangeable in every case. Arrhythmias, weak
sounds, missed beats, ectopic beats, and pulse deficits can cause
disagreement. Do not describe microphone PCG as directly measuring blood
flow or as an ECG replacement.

### Research question

Can a smartphone's built-in camera and microphone provide useful,
reliable heart-rate estimates under realistic conditions, and can
quality-aware fusion improve reliability over either modality alone?

### Candidate contributions

-   Robust signal-quality assessment and rejection of unreliable
    windows.
-   Cross-device and cross-environment generalization.
-   Motion- and lighting-aware camera PPG/rPPG.
-   Acoustic coupling and noise robustness for built-in microphones.
-   Beat-level alignment and confidence-aware camera--PCG fusion.
-   A lightweight on-device Android implementation.
-   A carefully collected, synchronized smartphone camera + microphone +
    ECG dataset.

------------------------------------------------------------------------

## 2. Related work and literature map

### 2.1 Camera-based fingertip PPG

**BUT PPG --- Brno University of Technology Smartphone PPG Database
(2021; PhysioNet v2.0.0)**\
A highly relevant benchmark for contact-based smartphone PPG. Version
2.0.0 contains 3,888 ten-second recordings from 50 participants,
captured using Xiaomi Mi9 and Huawei P20 Pro smartphones. The finger or
ear is placed over the camera/flash area; synchronized reference ECG
and, for most recordings, accelerometry are available. PPG is sampled at
30 Hz and ECG at 1,000 Hz. Each recording has a quality label and
reference HR. Includes rest and movement conditions.

-   Dataset: https://physionet.org/content/butppg/2.0.0/
-   Original dataset paper: https://doi.org/10.1155/2021/3453007
-   Use for: PPG heart-rate estimation, signal-quality classification,
    motion analysis, reference comparison.
-   Caveat: 50 people is modest; do participant-wise splits and do not
    treat 3,888 windows as 3,888 independent participants.

### 2.2 Contactless facial rPPG

**MMPD --- Multi-Domain Mobile Video Physiology Dataset (EMBC 2023)**\
11 hours of mobile-phone video from 33 participants, designed to vary
skin appearance, motion, and lighting. It was created to address the
shortage of mobile-camera rPPG datasets.

-   Dataset/code: https://github.com/THU-CS-PI/MMPD_rPPG_dataset
-   Paper: https://arxiv.org/abs/2302.03840
-   Use for: mobile facial rPPG, lighting/motion/skin-tone robustness,
    benchmarking traditional and neural methods.
-   Caveat: small participant count; ensure the official protocol and
    labels are followed.

**PHRM --- Passive Heart-Rate Monitoring During Smartphone Use in
Everyday Life (Nature, 2026)**\
A large-scale facial-video rPPG study for passive HR and resting-HR
estimation during everyday smartphone interactions. The paper reports
192,353 development videos from 485 participants and 162,546 validation
videos from 211 participants, with laboratory and free-living
validation.

-   Paper: https://www.nature.com/articles/s41586-026-10507-6
-   Dataset/model access: follow the access instructions and conditions
    linked by the paper.
-   Use for: current state of the art, passive measurement, large-scale
    validation, real-world research design.
-   Caveat: access is controlled; do not assume the raw data are
    unrestricted or immediately downloadable.

**M³PD --- Dual-view Smartphone PPG Dataset (2026)**\
A dual-view mobile PPG dataset with synchronized facial and fingertip
videos from front and rear smartphone cameras. The paper reports 60
participants, including 47 cardiovascular patients, and introduces
F³Mamba for dual-view fusion.

-   Paper: https://doi.org/10.1145/3810228
-   Code/data: https://github.com/Health-HCI-Group/F3Mamba
-   Use for: facial + fingertip camera fusion and clinical-population
    evaluation.
-   Caveat: this is camera-view fusion, not camera + microphone fusion.

**rPPG-Toolbox**\
A research codebase for reproducible rPPG benchmarking and
implementations of several methods.

-   Repository: https://github.com/ubicomplab/rPPG-Toolbox
-   Use for: baselines, data loaders, training/evaluation patterns.
-   Note: the toolbox is code, not a single dataset. Follow each
    dataset's own access and license terms.

### 2.3 Smartphone microphone and phonocardiography

**Cardiac Auscultation Using Smartphones: Pilot Study (2018)**\
Evaluated an Android app called CPstethoscope. Participants recorded
heart sounds by placing the phone against the chest; the study used the
built-in microphone rather than an add-on sensor.

-   Paper: https://mhealth.jmir.org/2018/2/e49
-   Full text: https://pmc.ncbi.nlm.nih.gov/articles/PMC5853766/
-   Use for: smartphone microphone placement, acquisition workflow,
    feasibility and recording constraints.
-   Important: this is a heart-sound acquisition study, not proof that
    arbitrary phone microphones can produce clinically accurate HR in
    all settings.

**Smartphone as an electronic stethoscope: factors influencing heart
sound quality (2022)**\
An iPhone app study with 1,148 users and 7,597 heart-sound recordings.
More than 80% of users obtained at least one good-quality recording;
quality was not uniformly good, highlighting the need for quality
detection and user guidance.

-   Paper: https://pmc.ncbi.nlm.nih.gov/articles/PMC9708017/
-   Use for: real-world acquisition variability, user training,
    recording quality and usability.

**Smartphone for heart sound measurement in hospital: feasibility and
influencing factors (2025)**\
Clinical feasibility study of smartphone heart-sound recordings in a
hospital environment. The paper discusses the built-in microphone as an
accessible acoustic sensor and reports that environmental noise and
recording context affect quality.

-   Paper: https://pmc.ncbi.nlm.nih.gov/articles/PMC12088729/
-   Journal version:
    https://academic.oup.com/ehjdh/article/6/3/486/8006140
-   Use for: clinical recording workflow and environmental confounders.

**Development of a Smartphone App for Visualizing Heart Sounds and
Murmurs (2017)**\
A smartphone phonocardiogram app using an external microphone attached
to a stethoscope, with tests on a human patient simulator. Useful as a
visualization/acquisition reference, but distinguish its external
microphone setup from a built-in-microphone-only system.

-   PubMed: https://pubmed.ncbi.nlm.nih.gov/28441656/

**Low-cost compliant acoustic coupling for smartphone-based
phonocardiography through textile interfaces (2026)**\
A study reports heart-sound acquisition using the built-in microphone of
an iPhone 15, with the microphone region facing the chest. It
investigates the effect of compliant coupling and textile interfaces on
acoustic transmission.

-   Paper:
    https://www.sciencedirect.com/science/article/pii/S0924424726003699
-   Use for: physical coupling, phone orientation, contact mechanics and
    microphone placement.
-   Caveat: check the full methods and validation before generalizing to
    other phone models.

### 2.4 PCG algorithms and foundational resources

For PCG, common tasks include heart-sound segmentation, S1/S2
localization, cycle detection, signal-quality estimation, and murmur
classification. HR estimation is a related but distinct task.

Useful algorithm families:

-   **Band-pass filtering:** isolate the useful heart-sound band while
    avoiding excessive filtering.
-   **Envelope extraction:** Hilbert envelope, Shannon energy,
    homomorphic envelope.
-   **S1/S2 segmentation:** detect first and second heart sounds.
-   **Hidden semi-Markov models (HSMM):** model the repeating
    S1--systole--S2--diastole sequence.
-   **Wavelet methods:** denoising and transient detection.
-   **Spectrogram/CNN models:** learned segmentation or quality
    assessment.
-   **Beat interval estimation:** estimate cycle duration from repeated
    S1 or S2 events, not from every S1 and S2 event as if each were a
    beat.

------------------------------------------------------------------------

## 3. Public datasets

### 3.1 Camera datasets

  --------------------------------------------------------------------------------------------------------------------
  Dataset        Modality / size Reference       Best use         Access
  -------------- --------------- --------------- ---------------- ----------------------------------------------------
  BUT PPG v2     Smartphone      Synchronized    Contact PPG HR + https://physionet.org/content/butppg/2.0.0/
                 fingertip/ear   ECG; ACC for    quality          
                 PPG; 3,888 × 10 most records                     
                 s; 50 subjects                                   

  MMPD           Mobile facial   Physiological   Mobile rPPG      https://github.com/THU-CS-PI/MMPD_rPPG_dataset
                 videos; 11      reference       robustness       
                 hours; 33       signals as                       
                 subjects        described in                     
                                 paper                            

  PHRM           Large-scale     ECG             Passive          Paper/access:
                 facial videos;                  everyday-life    https://www.nature.com/articles/s41586-026-10507-6
                 192,353                         rPPG             
                 development and                                  
                 162,546                                          
                 validation                                       
                 videos                                           

  M³PD           Dual-view       See paper/data  Camera-view      https://github.com/Health-HCI-Group/F3Mamba
                 facial +        documentation   fusion           
                 fingertip                                        
                 smartphone                                       
                 videos; 60                                       
                 subjects                                         

  VIPL-HR        Facial videos   BVP/HR          rPPG             https://vipl.ict.ac.cn/view_database.php?id=14
                 under varied    references per  generalization   
                 conditions; 107 dataset                          
                 subjects        protocol                         
  --------------------------------------------------------------------------------------------------------------------

### 3.2 Microphone / PCG datasets

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Dataset          Contents              Smartphone relevance     Reference / limitation       Access
  ---------------- --------------------- ------------------------ ---------------------------- -----------------------------------------------------------------------------------------------
  PASCAL           Dataset A includes    **High for mobile        S1/S2 segmentation labels    https://www.peterjbentley.com/heartchallenge/index.html
  Classifying      176 iStethoscope      audio** because subset A are available for part of    
  Heart Sounds     iPhone recordings;    came from an iPhone app  the data; not a synchronized 
  Challenge 2011   Dataset B includes                             ECG benchmark                
                   digital-stethoscope                                                         
                   recordings                                                                  

  PhysioNet/CinC   Heart-sound           Mixed; not all are       Labels are primarily         https://physionet.org/content/challenge-2016/1.0.0/
  2016             recordings from       smartphone recordings    normal/abnormal/uncertain;   
                   multiple sources and                           not a universal synchronized 
                   devices                                        ECG reference                

  CirCor DigiScope 5,282 pediatric       Clinical PCG, not        Rich S1/systole/S2/diastole  https://physionet.org/content/circor-heart-sound/1.0.3/
                   heart-sound           ordinary built-in phone  and murmur annotations;      
                   recordings from 1,568 microphone data          pediatric cohort             
                   patients; murmur and                                                        
                   segmentation                                                                
                   annotations                                                                 

  MIT Heart Sounds 409 PCG recordings    Electronic-stethoscope   PCG recorded simultaneously  Available within the PhysioNet/CinC 2016 archive documentation:
  Database         from 121 subjects     acquisition, not         with ECG; useful for         https://physionet.org/content/challenge-2016/1.0.0/
  (MITHSDB)                              smartphone built-in mic  PCG--ECG timing research     

  Yaseen           1,000 recordings      Not specifically         Classification-focused;      https://github.com/yaseen21khan/Classification-of-Heart-Sound-Signal-Using-Multiple-Features-
  heart-sound      across five classes   smartphone               verify original license and  
  dataset                                                         split before use             
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Dataset selection warning:** PCG datasets are not interchangeable with
smartphone recordings. A digital stethoscope has different acoustic
coupling, frequency response, gain, noise floor, and mechanical contact
from a phone's built-in microphone. Use PCG datasets for algorithm
prototyping, then collect phone-native audio for device-specific
validation.

**Another warning:** many PCG datasets provide murmur labels or S1/S2
segmentation, not a synchronized ECG. Do not claim ECG-level HR
validation unless synchronized ECG is actually supplied.

### 3.3 General rPPG datasets

These can be useful for pretraining or external validation, but check
whether the camera is a smartphone and whether the reference signal is
synchronized.

-   PURE: https://github.com/ubicomplab/rPPG-Toolbox
-   UBFC-rPPG: https://github.com/ubicomplab/rPPG-Toolbox
-   UBFC-Phys: https://sites.google.com/view/ybenezeth/ubfc-phys
-   COHFACE: https://www.idiap.ch/dataset/cohface
-   VIPL-HR: https://vipl.ict.ac.cn/view_database.php?id=14

------------------------------------------------------------------------

## 4. Recommended research architecture

### 4.1 Camera branch: fingertip PPG

1.  Capture video with rear camera and torch/flash enabled.
2.  Lock exposure, focus, white balance and frame rate where the device
    API permits.
3.  Select a stable region of interest (ROI) on the fingertip.
4.  Compute mean or robust RGB intensity per frame.
5.  Compare red, green, blue, and derived channel signals.
6.  Remove trend and normalize.
7.  Apply a physiologically plausible band-pass filter; document the
    chosen band and test sensitivity to it.
8.  Estimate HR using Welch PSD and/or peak-to-peak intervals.
9.  Estimate signal quality and reject unreliable windows.

**Baseline methods:** red-channel mean, green-channel mean, detrending,
Butterworth band-pass, Welch PSD, autocorrelation, peak detection.

### 4.2 Camera branch: facial rPPG

1.  Capture face video with front camera.
2.  Detect face and stable skin ROIs (forehead/cheeks); exclude eyes,
    lips, hair and background.
3.  Track ROIs across frames and detect motion/occlusion.
4.  Extract RGB traces from each ROI.
5.  Compare CHROM, POS, ICA and GREEN baselines.
6.  Apply detrending and filtering.
7.  Estimate pulse frequency using spectral and temporal methods.
8.  Add quality scoring based on motion, lighting, clipping, ROI size
    and periodicity.

**Baseline methods:** GREEN, CHROM, POS, ICA, and a toolbox
implementation. Deep learning models such as DeepPhys, PhysNet, TS-CAN
and EfficientPhys can be evaluated after reproducible traditional
baselines are established.

### 4.3 Microphone branch: built-in microphone PCG

1.  Record uncompressed PCM audio (WAV) where possible.
2.  Document sample rate, channel count, phone model, microphone
    location, Android/iOS audio source and audio-processing settings.
3.  Place the phone's microphone opening against the chest at a
    documented auscultation location.
4.  Keep phone orientation and contact pressure as consistent as
    practical.
5.  Record a quiet baseline and environmental-noise sample.
6.  Use appropriate pre-emphasis / band-pass filtering only after
    inspecting the raw signal.
7.  Compute amplitude envelope, Shannon energy or wavelet envelope.
8.  Detect candidate S1 and S2 events.
9.  Enforce plausible S1--S2 and S2--next-S1 sequence constraints.
10. Estimate beat intervals from S1-to-S1 (or S2-to-S2) intervals.
11. Reject windows with poor SNR, uncertain segmentation or irregular
    event sequence.

**Important implementation details:** - Avoid assuming one fixed
frequency response across phone models. - Android audio APIs may apply
automatic gain control, noise suppression or echo cancellation. Test and
document these; disable processing only where the OS/device allows it. -
The microphone port may not be the part of the phone that contacts the
chest. Design a reproducible placement protocol. - A soft coupling
interface may improve contact, but it changes the acoustic system and
must be documented. - Do not use audio playback or speaker output during
acquisition. - A phone microphone is an airborne/acoustic sensor, not a
calibrated contact accelerometer.

### 4.4 Camera + microphone fusion

Start with **late fusion**, not a complex end-to-end multimodal neural
network.

For each time window, compute:

-   Camera HR estimate and confidence.
-   Microphone HR estimate and confidence.
-   Signal-quality score for each modality.
-   Motion and illumination indicators.
-   Agreement/disagreement between estimates.

A simple confidence-weighted estimate is:

\[ `\widehat{HR}`{=tex}\_{fusion} =
`\frac{q_c \widehat{HR}_c + q_m \widehat{HR}_m}`{=tex} {q_c + q_m +
`\epsilon`{=tex}} \]

where: - (`\widehat{HR}`{=tex}\_c) = camera-derived estimate, -
(`\widehat{HR}`{=tex}\_m) = microphone-derived estimate, - (q_c, q_m) =
calibrated quality/confidence weights, - (`\epsilon`{=tex}) = small
numerical stabilizer.

This formula is a starting baseline, not a clinically validated
estimator. If the estimates disagree substantially, flag the window
rather than forcing a fused number. For arrhythmia or pulse deficit, PCG
cycle rate and peripheral pulse rate may legitimately differ.

Later compare: - late fusion of HR estimates; - feature-level fusion of
PPG and PCG embeddings; - temporal cross-attention; - quality-gated
mixture of experts.

------------------------------------------------------------------------

## 5. Experimental protocol

### 5.1 Phase 1 --- Reproduce public baselines

**Camera** - Use BUT PPG for fingertip/ear PPG. - Use MMPD for mobile
facial rPPG. - Reproduce at least one conventional method and one
toolbox baseline.

**Microphone** - Use PASCAL Dataset A for mobile-origin audio. - Use
PhysioNet/CinC 2016 and CirCor for broader PCG algorithm development. -
Use MITHSDB where synchronized PCG--ECG is needed and verify the exact
record-level data structure.

**Output:** reproducible baseline tables, dataset cards, and scripts.

### 5.2 Phase 2 --- Smartphone-specific data collection

Collect synchronized streams from the same participant:

-   Rear camera + flash fingertip PPG.
-   Front camera facial video (if consented).
-   Built-in microphone PCG with phone against chest.
-   Reference ECG (preferred) or validated reference pulse sensor, with
    clear limitations.
-   Optional accelerometer and gyroscope.
-   Timestamp synchronization and device metadata.

Suggested conditions: - seated rest; - standing rest; - controlled
post-exercise recovery; - quiet room; - moderate environmental noise; -
several lighting levels for camera; - controlled variation in contact
pressure and phone placement for microphone; - more than one phone
model.

Start with a feasibility pilot and power the larger study based on
observed variance and the intended confidence interval. Obtain ethics
approval and informed consent before human-subject data collection.

### 5.3 Phase 3 --- Generalization and fusion

Evaluate: - within-device performance; - leave-one-device-out
performance; - leave-one-participant-out performance; - quiet vs noisy
audio; - stable vs moving camera; - lighting subgroups; -
skin-pigmentation subgroup performance, with ethically collected and
appropriately measured data; - single-modality vs fused performance; -
quality-gated vs no-quality-gating performance.

### 5.4 Avoid data leakage

-   Split by participant, never by randomly splitting adjacent windows
    from the same person.
-   Keep all recordings from a participant in one partition.
-   If testing cross-device generalization, hold out entire phone
    models.
-   Tune thresholds and filters on training/validation only.
-   Keep a final untouched test set.
-   Report the number of participants as well as the number of windows.

------------------------------------------------------------------------

## 6. Evaluation metrics

  -----------------------------------------------------------------------
  Metric                              Definition / purpose
  ----------------------------------- -----------------------------------
  MAE (bpm)                           Mean absolute HR error

  RMSE (bpm)                          Penalizes larger errors

  MAPE (%)                            Relative error; unstable when
                                      reference values approach zero

  Pearson r                           Correlation, not agreement

  Bland--Altman bias and limits of    Agreement with reference
  agreement                           

  HR success/coverage rate            Fraction of windows producing a
                                      valid estimate

  Signal-quality AUROC / F1           Quality classifier performance

  Beat timing error                   Event-level timing against ECG or
                                      expert annotation

  Latency                             Time from acquisition to result

  Energy / CPU / memory               On-device resource cost
  -----------------------------------------------------------------------

Report both **conditional accuracy** (only accepted windows) and
**coverage** (how many windows were accepted). A system can appear
accurate simply by rejecting difficult cases.

For a clinically oriented study, define the target population, intended
use, reference standard, and acceptable error thresholds before
analysis. Do not infer clinical validity from a low MAE on a small
public dataset.

------------------------------------------------------------------------

## 7. Practical technology stack

### Research / offline analysis

-   Python 3.10+
-   NumPy, SciPy, pandas
-   librosa or soundfile for audio I/O
-   OpenCV for video/ROI processing
-   NeuroKit2 / WFDB for ECG and physiological signal utilities
-   scikit-learn for classical models and metrics
-   PyTorch for neural models
-   rPPG-Toolbox for rPPG baselines
-   matplotlib for plots

### Android prototype

-   Kotlin
-   CameraX or Camera2 for camera acquisition
-   Android `AudioRecord` for PCM microphone capture
-   TFLite / LiteRT or ONNX Runtime Mobile for on-device inference
-   Room / local file storage for consented research sessions
-   Avoid sending raw face video or audio to a server unless essential
    and explicitly consented.

### Suggested repository structure

``` text
smartphone-heart-rate/
├── README.md
├── LICENSE
├── CITATION.cff
├── docs/
│   ├── literature-review.md
│   ├── dataset-cards.md
│   ├── protocol.md
│   └── ethics-and-privacy.md
├── data/
│   ├── README.md
│   ├── raw/                 # ignored by git
│   ├── interim/
│   └── processed/
├── configs/
│   ├── camera_ppg.yaml
│   ├── facial_rppg.yaml
│   ├── microphone_pcg.yaml
│   └── fusion.yaml
├── src/
│   ├── camera/
│   │   ├── fingertip_ppg.py
│   │   └── facial_rppg.py
│   ├── microphone/
│   │   ├── audio_io.py
│   │   ├── pcg_preprocess.py
│   │   └── pcg_events.py
│   ├── fusion/
│   │   └── late_fusion.py
│   ├── quality/
│   └── evaluation/
├── notebooks/
├── tests/
├── app/
│   └── android/
└── results/
```

------------------------------------------------------------------------

## 8. Recommended first experiments

  ----------------------------------------------------------------------------
  Priority          Experiment        Dataset           Deliverable
  ----------------- ----------------- ----------------- ----------------------
  1                 Fingertip PPG HR  BUT PPG           MAE/RMSE + quality
                    baseline                            analysis
                    (red/green +                        
                    Welch)                              

  2                 Facial rPPG       MMPD              HR error by
                    baseline                            lighting/motion
                    (POS/CHROM)                         

  3                 PCG segmentation  PASCAL A, MITHSDB Event detection +
                    and S1-to-S1                        timing error
                    cycle estimate                      

  4                 PCG robustness    CinC 2016, CirCor Coverage vs error
                    and quality                         
                    gating                              

  5                 Cross-device test Own multi-phone   Leave-one-device-out
                                      recordings        results

  6                 Camera + mic late Own synchronized  Fusion vs each
                    fusion            dataset           modality

  7                 On-device         Own recordings    Latency, battery,
                    prototype                           usability
  ----------------------------------------------------------------------------

**Critical limitation:** Public datasets do not appear to provide a
large, representative corpus of synchronized *built-in smartphone
microphone PCG + smartphone camera PPG/rPPG + ECG* captured
simultaneously. That gap itself may justify collecting a carefully
designed dataset, subject to ethics approval.

------------------------------------------------------------------------

## 9. Research gaps and possible paper contributions

1.  **Phone-native acoustic generalization:** PCG algorithms trained on
    digital-stethoscope recordings may not transfer to built-in phone
    microphones. Quantify the domain gap.
2.  **Acoustic coupling:** test the influence of phone model, microphone
    port, orientation, pressure, clothing and coupling pad.
3.  **Quality-aware estimation:** predict when a modality is unreliable
    and abstain rather than output a misleading HR.
4.  **Cross-modal agreement:** use disagreement between PPG and PCG as a
    quality or physiology signal, while distinguishing pulse deficit
    from sensor failure.
5.  **Multimodal fusion:** determine whether camera + microphone
    improves coverage or error under complementary failure conditions.
6.  **Low-cost deployment:** evaluate latency, thermal behavior, battery
    consumption and performance on lower-cost Android devices.
7.  **Fairness and robustness:** report subgroup results across skin
    pigmentation, age, sex, phone model and environmental conditions
    where sample sizes support meaningful analysis.

A defensible novelty claim should be based on a systematic literature
review and a reproducible comparison, not merely on the fact that the
app uses two sensors.

------------------------------------------------------------------------

## 10. Safety, privacy and ethics

-   This project is for research and prototyping, not diagnosis or
    emergency monitoring.
-   Do not claim medical-grade accuracy without an appropriately
    designed clinical validation study.
-   Heart sounds and face video are sensitive personal data. Obtain
    informed consent and minimize collection.
-   Prefer on-device processing; store only derived features when raw
    media is not necessary.
-   Encrypt research files, restrict access, define retention/deletion
    schedules, and de-identify metadata.
-   Obtain institutional ethics/IRB approval before recruiting
    participants.
-   Do not collect data from minors or clinical populations without
    appropriate approvals and safeguards.
-   Provide a clear "unable to measure" state when signal quality is
    poor.

------------------------------------------------------------------------

## 11. Core references

### Camera / PPG / rPPG

1.  Nemcova A. et al. (2021). *Brno University of Technology Smartphone
    PPG Database (BUT PPG): Annotated Dataset for PPG Quality Assessment
    and Heart Rate Estimation.* BioMed Research International.
    https://doi.org/10.1155/2021/3453007
2.  Tang J. et al. (2023). *MMPD: Multi-Domain Mobile Video Physiology
    Dataset.* EMBC. https://arxiv.org/abs/2302.03840
3.  *Passive heart-rate monitoring during smartphone use in everyday
    life.* Nature (2026).
    https://www.nature.com/articles/s41586-026-10507-6
4.  *M³PD Dataset: Enabling Dual-view Photoplethysmography on
    Smartphones in Lab and Clinical Settings.* IMWUT (2026).
    https://doi.org/10.1145/3810228
5.  rPPG-Toolbox. https://github.com/ubicomplab/rPPG-Toolbox

### Microphone / PCG

6.  *Cardiac Auscultation Using Smartphones: Pilot Study.* JMIR mHealth
    and uHealth (2018). https://mhealth.jmir.org/2018/2/e49
7.  *Smartphone as an electronic stethoscope: factors influencing heart
    sound quality.* (2022).
    https://pmc.ncbi.nlm.nih.gov/articles/PMC9708017/
8.  *Smartphone for heart sound measurement in hospital: feasibility and
    influencing factors.* European Heart Journal -- Digital Health
    (2025). https://pmc.ncbi.nlm.nih.gov/articles/PMC12088729/
9.  Bentley P. et al. *PASCAL Classifying Heart Sounds Challenge 2011.*
    https://www.peterjbentley.com/heartchallenge/index.html
10. Liu C. et al. (2016). *An Open Access Database for the Evaluation of
    Heart Sound Algorithms.* Physiological Measurement.
    https://doi.org/10.1088/0967-3334/37/12/2181
11. Oliveira J. et al. *The CirCor DigiScope Phonocardiogram Dataset.*
    https://physionet.org/content/circor-heart-sound/1.0.3/
12. *Low-cost compliant acoustic coupling for smartphone-based
    phonocardiography through textile interfaces.* (2026).
    https://www.sciencedirect.com/science/article/pii/S0924424726003699

------------------------------------------------------------------------

## 12. Dataset access and citation checklist

Before using a dataset: - Read its official documentation and license. -
Cite the original dataset paper and version. - Record the download date
and exact version. - Respect PhysioNet credentialing / data-use
requirements where applicable. - Keep original files unchanged and
record preprocessing scripts. - Do not redistribute restricted data or
pretrained weights without permission. - Record subject IDs and split
membership to prevent leakage. - Keep a manifest with file hashes and
preprocessing versions.

------------------------------------------------------------------------

## 13. Immediate next steps

1.  Download BUT PPG v2.0.0 and reproduce a fingertip HR baseline.
2.  Request/download MMPD and reproduce POS/CHROM facial rPPG baselines.
3.  Download PASCAL Challenge data and prototype S1/S2 detection on its
    iStethoscope subset.
4.  Review MITHSDB records for synchronized PCG--ECG timing validation.
5.  Design a pilot protocol to collect phone-native microphone +
    camera + ECG recordings simultaneously.
6.  Only after those baselines, test confidence-aware camera--microphone
    fusion.

**Working hypothesis:** Camera PPG/rPPG will provide the primary
pulse-rate estimate, while microphone PCG can supply complementary
cardiac-cycle timing and an independent quality signal. Whether fusion
improves robust HR estimation is an empirical question that must be
tested against synchronized ECG.
