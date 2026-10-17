# Wearable Sensor Signal Processing — 8-Week Roadmap

A practical learning plan for extracting meaningful features from wearable-device signals using **Python and MATLAB**. Focus areas include photoplethysmography (PPG), electrocardiography (ECG), accelerometer, and gyroscope data from smartwatches, rings, fitness bands, and research sensors.

> **Important:** This is an educational/research roadmap, not medical advice. A feature extracted from a sensor is not automatically a clinically valid measurement. Validate algorithms against appropriate annotations or reference signals, and respect dataset licenses, consent, and privacy requirements.

## Contents

- [Goals](#goals)
- [Recommended resources](#recommended-resources)
- [Signals and features](#signals-and-features)
- [Eight-week plan](#eight-week-plan)
- [Daily study template](#daily-study-template)
- [Capstone project](#capstone-project)
- [Suggested repository structure](#suggested-repository-structure)
- [Validation checklist](#validation-checklist)
- [Definition of done](#definition-of-done)

## Goals

By the end of eight weeks, aim to:

1. Load and inspect sampled sensor data and understand its metadata.
2. Understand sampling rate, units, timestamps, aliasing, filtering, and frequency analysis.
3. Preprocess physiological and motion signals while documenting parameters.
4. Detect PPG pulse peaks and ECG R-peaks, where data quality permits.
5. Extract time-domain, frequency-domain, and signal-quality features.
6. Explore how movement affects physiological signal quality.
7. Implement and compare selected operations in Python and MATLAB.
8. Evaluate outputs against annotations, reference measurements, or synthetic test signals.
9. Publish a reproducible project with plots, tests, instructions, and limitations.

### Time budget

- **Duration:** 8 weeks
- **Pace:** 2.5–3 hours/day, 6 days/week
- **Total:** approximately 120–144 hours
- **Flexibility:** if programming, probability, or linear algebra is new to you, extend the schedule or reduce the number of features.

---

## Recommended resources

### 1. Primary: Signal Processing and Learning for Wearables

Educational resource associated with Peter H. Charlton and collaborators.

- **Read:** <https://peterhcharlton.github.io/bsp-book/>
- **Why:** closest to the goal of processing physiological signals measured by wearables, including signal processing and learning methods.
- **How to use it:** study actively, reproduce examples, and apply each concept to a real recording.
- **Priority:** start here.

### 2. Statistics: OpenIntro Statistics

David Diez, Mine Çetinkaya-Rundel, and Christopher Barr.

- **Read:** <https://www.openintro.org/book/os/>
- **Focus:** descriptive statistics, probability, distributions, sampling, confidence intervals, hypothesis tests, and regression.
- **How to use it:** solve selected exercises and apply the concepts when comparing features across conditions or participants.

### 3. Python data science: Python Data Science Handbook

Jake VanderPlas.

- **Read and browse notebooks:** <https://jakevdp.github.io/PythonDataScienceHandbook/>
- **Focus:** NumPy, pandas, visualization, data cleaning, and introductory machine-learning workflows.
- **How to use it:** reproduce examples and adapt them to sensor data instead of only reading.

### 4. Signal quality: Signal Quality Assessment in Physiological Monitoring

Christina Orphanidou.

- **Publisher page:** <https://link.springer.com/book/10.1007/978-3-319-68415-4>
- **Why:** noisy signals, motion artifacts, poor contact, and missing data can make extracted features unreliable.
- **How to use it:** consult it after learning basic preprocessing and feature extraction.

### 5. Public datasets

- **PhysioNet PPG topic search:** <https://physionet.org/content/?topic=ppg>
- **Wrist PPG During Exercise:** <https://physionet.org/content/wrist-ppg-exercise/>

Read each dataset's documentation before use. Confirm channels, sample rates, units, synchronization, protocol, annotation definitions, access conditions, and license. Not every dataset contains all sensor types or a reference signal.

### 6. Software documentation

- Python: <https://www.python.org/>
- NumPy: <https://numpy.org/doc/>
- SciPy signal processing: <https://docs.scipy.org/doc/scipy/reference/signal.html>
- pandas: <https://pandas.pydata.org/docs/>
- Matplotlib: <https://matplotlib.org/stable/>
- scikit-learn: <https://scikit-learn.org/stable/>
- MATLAB: <https://www.mathworks.com/help/matlab/>
- MATLAB Signal Processing Toolbox: <https://www.mathworks.com/help/signal/>

Some MATLAB functions require a licensed toolbox. Check availability before depending on a particular function.

---

## Signals and features

### PPG — photoplethysmography

An optical signal related to changes in blood volume near the sensor. Wrist and finger recordings may be affected by movement, contact pressure, ambient light, sensor placement, and device-specific processing.

**Learn first**
- Inspect raw waveforms, sample rates, and signal units.
- Detrend or filter only when appropriate for the intended feature.
- Detect pulse peaks and calculate pulse-to-pulse intervals.
- Flag noisy segments and implausible intervals.
- Compare rest and movement when the dataset supports it.

**Potential features**
- Pulse rate
- Pulse-to-pulse intervals with quality flags
- Pulse amplitude and amplitude variability
- Pulse width or selected morphology measures
- Signal-quality indicators
- Justified frequency-domain summaries

**Caution:** PPG pulse intervals are not identical to ECG RR intervals. PPG-derived variability is not automatically interchangeable with ECG-derived HRV.

### ECG — electrocardiography

Measures the heart's electrical activity. Recordings may contain baseline wander, power-line interference, muscle noise, movement artifacts, and electrode-contact problems.

**Learn first**
- Inspect waveform and recording metadata.
- Assess baseline and noise.
- Apply documented filters.
- Detect QRS complexes/R-peaks.
- Calculate RR intervals and inspect missed or false detections.

**Potential features**
- Heart rate
- RR intervals
- Time-domain HRV measures when duration and quality are adequate
- Selected QRS timing or morphology features
- Signal-quality indicators

**Caution:** HRV depends on recording duration, preprocessing, ectopic-beat handling, and protocol. Document these decisions.

### Accelerometer and gyroscope

Inertial sensors capture movement and rotation. Axes, units, coordinate systems, sampling rates, and preprocessing can vary by device.

**Learn first**
- Verify units, orientation, timestamps, and sample rate.
- Plot each axis and vector magnitude.
- Segment data into fixed-duration windows.
- Compare stationary and active periods.
- Explore time- and frequency-domain summaries.

**Potential features**
- Per-axis mean and standard deviation
- Root mean square (RMS)
- Signal magnitude and its variation
- Signal magnitude area (SMA), with a documented formula
- Energy and selected spectral features
- Dominant frequency where meaningful
- Movement-intensity features

**Caution:** State whether gravity is included or removed. Do not assume that axes or units are comparable across devices without checking metadata.

### Other possible sensors

Later, consider skin temperature, electrodermal activity (EDA), respiration, SpO2, or barometer data. Start with PPG and motion before expanding scope.

---

## Eight-week plan

The estimates below are flexible and total roughly 120–144 hours. Adjust according to your existing knowledge and any overlapping content in your Udemy course.

### Week 1 — Foundations and data inspection (14–16 h)

- Review sampling rate, time axes, units, missing samples, and amplitude.
- Refresh Python arrays, pandas, and plotting; review MATLAB arrays and plotting.
- Download one public dataset and read its documentation.
- Plot raw PPG, ECG, and accelerometer channels where available.
- Check gaps, clipping, outliers, metadata, and synchronization.

**Deliverable:** notebook/script that loads a recording, reports metadata, and plots raw channels.

### Week 2 — DSP fundamentals (14–16 h)

- Study sampling, aliasing, Fourier transforms, and power spectral density.
- Learn low-pass, high-pass, band-pass, and notch filters.
- Compare raw and filtered signals, including edge effects.
- Understand causal versus zero-phase/offline filtering.
- Document filter type, order, cutoffs, sample rate, and implementation.

**Deliverable:** preprocessing notebook with raw/filtered comparisons and a short explanation of trade-offs.

### Week 3 — PPG processing (14–18 h)

- Inspect PPG morphology and label clean/noisy intervals.
- Implement or adapt a pulse-peak detector.
- Calculate pulse intervals and heart-rate estimates for suitable segments.
- Flag implausible intervals and low-quality windows.
- Compare rest and movement if supported by the data.

**Deliverable:** PPG pipeline with plots, detected peaks, intervals, and quality flags.

### Week 4 — Motion features (14–18 h)

- Inspect axes, units, and orientation.
- Calculate vector magnitude and document gravity handling.
- Segment signals into windows and record the window size.
- Calculate mean, standard deviation, RMS, SMA, and selected spectral features.
- Compare movement features with PPG quality/error if synchronized data are available.

**Deliverable:** window-level feature table with timestamps and quality notes.

### Week 5 — ECG processing (14–18 h)

- Review ECG morphology and common noise sources.
- Implement or adapt an R-peak detector.
- Calculate RR intervals and heart rate on suitable recordings.
- Check missed beats and false detections against annotations or visual review.
- Compare ECG and PPG timing only when synchronization and reference quality support it.

**Deliverable:** ECG pipeline with R-peaks, RR intervals, and an evaluation summary.

### Week 6 — Statistics and feature evaluation (14–18 h)

- Review distributions, summary statistics, confidence intervals, and regression.
- Compare feature distributions across activity conditions or sessions.
- Examine participant-level variation and missingness.
- Consider quality-related selection bias.
- For predictive models, split by participant/session when appropriate to avoid leakage from correlated windows.

**Deliverable:** short report explaining feature differences and the limits of the evidence.

### Week 7 — Python/MATLAB parity and robustness (14–18 h)

- Implement one or two key operations in both languages.
- Compare filter outputs, peak timestamps, intervals, and feature values.
- Investigate differences due to indexing, parameters, units, defaults, and boundary handling.
- Test multiple recordings, including noisy examples.
- Keep known synthetic test signals for repeatable checks.

**Deliverable:** comparison report with tolerances and explanations for discrepancies.

### Week 8 — Capstone and documentation (16–20 h)

- Refactor code into reusable functions.
- Run the pipeline on a small, documented dataset.
- Generate plots and a feature table.
- Document assumptions, limitations, and evaluation results.
- Finish usage instructions, environment requirements, and reproducibility notes.

**Deliverable:** a GitHub project that another person can understand and run.

---

## Daily study template

For a 2.5-hour study day, six days each week:

| Activity | Time |
|---|---:|
| Wearable resource or course | 45 min |
| Coding and experiments | 60 min |
| Statistics/theory and exercises | 30 min |
| Notes, plots, and review | 15 min |
| **Total** | **150 min** |

Use the sixth study day for review, finishing the weekly deliverable, and planning the next week. Keep one day for rest or optional light reading.

**Rule:** each session should produce something observable—a solved exercise, plot, tested function, comparison, or written explanation.

---

## Capstone project: Wearable feature extraction

**Goal:** build a reproducible pipeline that extracts features from PPG and motion signals, adding ECG if the dataset supports it.

### Inputs

- Raw or minimally processed recordings
- Sample rates, units, timestamps, and channel descriptions
- Activity/session labels if available
- Reference signals or annotations if available

### Pipeline

1. **Load and inspect:** validate file format, channels, units, timestamps, and missing values.
2. **Preprocess:** apply justified filters and document parameters; preserve raw data.
3. **Segment:** split into windows with start/end times; record overlap and discarded windows.
4. **Detect events:** detect pulse peaks and/or ECG R-peaks; save timestamps and quality information.
5. **Extract features:** compute a small, tested set of temporal, spectral, and quality features; add motion features.
6. **Evaluate:** compare detections with annotations or suitable references where available.
7. **Export:** save a tidy feature table and plots, including metadata needed to reproduce results.

### Example output schema

| recording_id | window_start_s | window_end_s | ppg_quality | pulse_rate_bpm | accel_rms | notes |
|---|---:|---:|---|---:|---:|---|
| demo_001 | 0 | 30 | example | example | example | Placeholder values |

The table contains placeholders, not real measurements. Define each feature, unit, and calculation window precisely.

### Success criteria

- Pipeline runs from documented inputs to outputs.
- Raw and processed signals can be compared visually.
- Missing or low-quality segments are flagged transparently.
- Features have tests against synthetic signals or known cases.
- Results are evaluated against annotations/reference data where available.
- README explains limitations and reproducibility steps.

---

## Suggested repository structure

```text
wearable-signal-processing/
├── README.md
├── requirements.txt
├── data/
│   └── README.md
├── notebooks/
│   ├── 01_data_inspection.ipynb
│   ├── 02_filtering_basics.ipynb
│   ├── 03_ppg_features.ipynb
│   ├── 04_accelerometer_features.ipynb
│   ├── 05_ecg_features.ipynb
│   └── 06_feature_evaluation.ipynb
├── src/
│   └── wearable_signals/
│       ├── io.py
│       ├── preprocessing.py
│       ├── quality.py
│       ├── peaks.py
│       ├── features.py
│       └── evaluation.py
├── matlab/
│   ├── inspect_signal.m
│   ├── preprocess_signal.m
│   └── extract_features.m
├── tests/
│   ├── test_preprocessing.py
│   └── test_features.py
├── reports/
│   └── figures/
└── references/
    └── reading_notes.md
```

Start smaller if needed; add modules when useful. Do not commit private/raw data, credentials, or restricted files. Put dataset acquisition instructions and citations in `data/README.md`.

### Minimal Python setup

```bash
python -m venv .venv
```

Activate the environment, then install the packages needed for your workflow:

```bash
python -m pip install numpy scipy pandas matplotlib jupyter scikit-learn
```

Record tested versions in `requirements.txt` once the pipeline runs. Specialized dataset readers may require additional packages.

---

## Validation checklist

Before trusting a feature, ask:

- [ ] Are sample rate and timestamps correct?
- [ ] Are units, axis definitions, and device processing documented?
- [ ] Is the filter appropriate for the signal and feature?
- [ ] Have filter transients and boundary effects been considered?
- [ ] Are peaks checked against annotations or careful visual review?
- [ ] Are motion artifacts and low-quality windows flagged?
- [ ] Are interval calculations restricted to plausible, quality-controlled detections?
- [ ] Is the recording long enough for the feature?
- [ ] Are units and window lengths explicit?
- [ ] Are missing data and discarded windows reported?
- [ ] Is evaluation split by participant/session where appropriate?
- [ ] Are results reproducible from documented inputs and parameters?
- [ ] Are privacy, consent, licensing, and data-use requirements respected?

An algorithm that works on one clean example may fail on another device, participant, activity, or sensor placement. Robustness testing is part of the work.

---

## Study method

1. Read a short section.
2. Summarize it in your own words.
3. Reproduce the example.
4. Apply it to a real recording.
5. Change one parameter and observe the effect.
6. Check against annotations, references, or a known test signal.
7. Record assumptions, limitations, and lessons.
8. Commit working code and notes to Git.

Prioritize a trustworthy loading, visualization, preprocessing, and evaluation workflow before expanding the feature set.

## Definition of done

At the end of eight weeks, aim to have:

- [ ] Completed the core sections of the wearable signal-processing resource.
- [ ] Reviewed relevant OpenIntro Statistics chapters and solved exercises.
- [ ] Built a working PPG feature-extraction pipeline.
- [ ] Built an accelerometer feature-extraction pipeline.
- [ ] Implemented a basic ECG/R-peak workflow if suitable data are available.
- [ ] Compared at least one operation in Python and MATLAB.
- [ ] Evaluated outputs using annotations, reference signals, or synthetic tests.
- [ ] Published a reproducible repository with plots, instructions, and limitations.

**Prioritize correctness and understanding over feature count.** A small set of validated features is more valuable than a large table of unreliable measurements.

## Notes and further reading

Use `references/reading_notes.md` to track resources/chapters, key concepts, reproduced examples, open questions, dataset details, and papers to revisit.

Record the exact dataset version, preprocessing parameters, package versions, and algorithm choices so your results can be reproduced and compared.
