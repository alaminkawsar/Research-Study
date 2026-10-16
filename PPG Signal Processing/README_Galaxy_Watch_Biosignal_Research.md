# Galaxy Watch Biosignal Research: PPG, Wearable Sensors, and Feature Engineering

> A practical, research-oriented guide to collecting Samsung Galaxy Watch sensor data, extracting signal features, and evaluating whether those features are associated with a biomarker such as glucose.
>
> **Important:** This is a research project, not a medical device. Galaxy Watch PPG is not a validated standalone glucose measurement method. Do not use model output for diagnosis, medication, or treatment decisions.

## Table of contents

- [1. Project goals](#1-project-goals)
- [2. What Galaxy Watch data can you access?](#2-what-galaxy-watch-data-can-you-access)
- [3. Important limitations before you start](#3-important-limitations-before-you-start)
- [4. Recommended project architecture](#4-recommended-project-architecture)
- [5. Step 1 — Check your watch and SDK](#5-step-1--check-your-watch-and-sdk)
- [6. Step 2 — Collect data](#6-step-2--collect-data)
- [7. Step 3 — Design a synchronized research protocol](#7-step-3--design-a-synchronized-research-protocol)
- [8. Step 4 — Clean and inspect PPG](#8-step-4--clean-and-inspect-ppg)
- [9. Step 5 — Detect beats and segment pulses](#9-step-5--detect-beats-and-segment-pulses)
- [10. Step 6 — Extract a feature set](#10-step-6--extract-a-feature-set)
- [11. Other sensor modalities](#11-other-sensor-modalities)
- [12. Glucose-related study design](#12-glucose-related-study-design)
- [13. Machine learning and validation](#13-machine-learning-and-validation)
- [14. Suggested repository structure](#14-suggested-repository-structure)
- [15. Starter Python pipeline](#15-starter-python-pipeline)
- [16. Quality checks and common failures](#16-quality-checks-and-common-failures)
- [17. A staged roadmap](#17-a-staged-roadmap)
- [18. References and official documentation](#18-references-and-official-documentation)

---

## 1. Project goals

The aim is to build a reproducible pipeline:

**Galaxy Watch sensors → timestamped raw/processed data → quality control → signal processing → feature extraction → reference biomarker matching → statistical analysis → held-out validation.**

Start by characterizing the signals and measuring repeatability. Only later test whether any features predict a target such as glucose.

Questions this project can investigate:

1. Which PPG features are stable within one person and across sessions?
2. How do movement, skin temperature, activity, and watch fit affect those features?
3. Do features correlate with a reference measurement after accounting for confounders?
4. Does a model generalize to a new recording session or a person it has never seen?

A correlation is not proof of a physiological mechanism or a clinically useful measurement.

## 2. What Galaxy Watch data can you access?

Samsung's **Health Sensor SDK** is the most relevant starting point for research involving raw watch signals. Samsung documents support for Galaxy Watch4 series and later Wear OS-powered Galaxy Watch devices, but availability depends on model, software, Health Sensor Service version, SDK version, permissions, and tracker type.

| Modality | What it can provide | Potential research uses | Cautions |
|---|---|---|---|
| PPG green, red, infrared (IR) | Raw optical samples for supported tracker types | Pulse morphology, timing, AC/DC trends, signal quality; compare channels | Sampling rate and collection duration differ by tracker type; optical readings are not glucose measurements |
| Heart rate and inter-beat interval (IBI) | Processed HR and beat interval values | Baseline comparison, pulse-rate trends, HRV-related exploratory features | HR is processed and loses much of the raw waveform morphology; IBI quality must be checked |
| Accelerometer X/Y/Z | Motion at documented sampling rate | Motion detection, activity/context, artifact flags | Motion is a confounder and may not capture every source of optical artifact |
| Skin and ambient temperature | Processed temperature data on supported watches | Contextual covariates; temperature-related effects | Watch-reported skin temperature is not core body temperature; availability varies |
| ECG | Raw ECG on supported device/workflow | Research comparison for cardiac timing when permitted | ECG access/recording workflow and restrictions differ; ECG is not PPG |
| EDA | Electrodermal activity on supported models | Exploratory autonomic/stress-related context | Model availability varies; not specific to glucose |
| SpO₂ | Processed oxygen-saturation estimate | Contextual variable, not a PPG raw-waveform substitute | On-demand/spot measurement restrictions apply |
| BIA / multi-frequency BIA | Bioimpedance-related measurements | Exploratory body-composition context | Not a continuous sensor stream; measurement conditions matter |
| Sweat loss after running | Processed estimate on supported workflows | Exercise context | Not a general-purpose continuous biomarker |

**Official starting points:**
- Samsung Health Sensor SDK overview: https://developer.samsung.com/health/sensor/overview.html
- SDK introduction and target devices: https://developer.samsung.com/health/sensor/guide/introduction.html
- Sensor data specifications: https://developer.samsung.com/health/sensor/guide/data-specifications.html
- API reference: https://developer.samsung.com/health/sensor/api-reference/overview-summary.html
- FAQ: https://developer.samsung.com/health/sensor/faq.html

### Important sampling-rate detail

Samsung's currently documented specifications distinguish tracker types:

- **Continuous PPG:** raw green, IR, and red channels documented at **25 Hz**.
- **On-demand PPG:** raw green, IR, and red channels documented at **100 Hz**, but intended for short, foreground measurements (Samsung documentation says not to track the on-demand type for longer than 30 seconds).
- **Continuous accelerometer:** documented at **25 Hz**.
- **Continuous processed heart rate including IBI:** documented at **1 Hz**.
- **EDA:** documented at 1 Hz on supported Galaxy Watch8-series-and-later devices.
- **Skin temperature:** tracker availability and whether continuous/on-demand depends on model and SDK/service version.

These are SDK documentation values, not a guarantee that every watch, OS build, or tracker exposes every channel in every situation. Check the current data-specification page and query tracker capabilities on the actual device. Never assume a 100 Hz PPG stream if the tracker actually delivers 25 Hz.

### Health Sensor SDK vs Health Connect vs Samsung Health Data SDK

These serve different purposes:

- **Health Sensor SDK:** preferred route to supported raw PPG and sensor streams from a compatible watch app.
- **Health Connect:** Android phone-side health-data sharing layer. It can expose synchronized health records such as heart rate, sleep, activity, and oxygen saturation with permission, but it is not a route to arbitrary raw PPG waveforms.
- **Samsung Health Data SDK:** access to supported records stored in Samsung Health. It is useful for processed health history, not a replacement for the raw PPG sensor SDK.

References:
- Health Connect FAQ for Samsung Health: https://developer.samsung.com/health/health-connect-faq.html
- Samsung Health Data SDK: https://developer.samsung.com/health/data/overview.html

## 3. Important limitations before you start

1. **Developer access is not the same as consumer access.** Samsung's Health Sensor SDK has setup and developer-mode requirements. Samsung says Health Sensor Service developer mode is for app testing/debugging, not for ordinary end users. Review the current program and distribution terms before planning a public app.
2. **Raw access may be constrained.** The watch model, region, service version, permissions, foreground/background rules, tracker type, and SDK policies can affect availability.
3. **The watch is not a research-grade reference instrument by default.** Validate timing, sampling, missing samples, channel quality, and repeatability.
4. **Wrist PPG is vulnerable to motion and contact pressure.** Temperature, skin perfusion, ambient conditions, exercise, stress, posture, and medications can alter the waveform.
5. **PPG does not directly measure glucose.** Glucose-related claims require synchronized reference glucose measurements and rigorous independent validation.
6. **Privacy matters.** Biosignals and glucose readings are sensitive health data. Use informed consent, encrypted storage, access controls, and de-identification. Do not upload identifiable raw health data to public repositories.

## 4. Recommended project architecture

```text
Galaxy Watch
  └── Samsung Health Sensor SDK
        ├── PPG green / red / IR
        ├── Accelerometer
        ├── HR / IBI
        └── Other supported signals
                ↓
        Timestamped collection app
                ↓
        Local CSV / Parquet + session metadata
                ↓
        Quality control and synchronization
                ↓
        Filtering and pulse segmentation
                ↓
        Beat-level features + window-level features
                ↓
        Reference measurements / labels
                ↓
        Subject-wise validation and analysis
```

For a first version, use a **Wear OS app written in Kotlin** to collect data with Samsung's SDK. Save data locally on the watch or transfer it to a paired Android phone. Use Python for offline analysis.

Do not start with machine learning. First prove that the app collects well-timestamped data and that the signals/features are reproducible.

## 5. Step 1 — Check your watch and SDK

Record these details in your project README or session metadata:

- Exact Galaxy Watch model (for example, Watch4, Watch5, Watch6, Watch7, Watch8)
- Watch OS / Wear OS version
- Phone model and Android version
- Samsung Health app version
- Health Sensor Service version
- Samsung Health Sensor SDK version
- Supported tracker types returned by the SDK
- Which PPG channels are actually available
- Sampling rate, timestamps, and whether sample arrays are batched
- Whether the app must remain foregrounded
- Permissions granted and any developer-mode requirements

Use Samsung's official getting-started guide and sample apps. Check `getSupportHealthTrackerTypes()` / tracker capability rather than hard-coding assumptions. Confirm the SDK and Health Sensor Service versions are compatible; Samsung documents compatibility requirements and version errors.

**Do not assume that ordinary Samsung Health exports contain raw PPG.** Health history exports and Health Connect are mainly for supported health records; raw optical samples require the appropriate sensor SDK workflow.

## 6. Step 2 — Collect data

### Suggested initial recording protocol

For signal-engineering tests, not clinical conclusions:

1. Wear the watch snugly, slightly above the wrist bone, without cutting off circulation.
2. Sit still for 5 minutes before recording.
3. Record 2–5 minutes at rest, if the selected tracker and SDK permit it.
4. Record the raw channels and exact timestamps/sample metadata.
5. Record accelerometer data simultaneously when possible.
6. Mark events: start/end, posture changes, movement, watch adjustment, meals, exercise, and reference-measurement times.
7. Repeat across multiple sessions and days.
8. Save the original raw stream unchanged.

For on-demand PPG, follow Samsung's short-duration and foreground restrictions. Do not treat the documented 100 Hz on-demand mode as permission for long-term continuous capture.

### Example CSV schema

Choose one row per sample when feasible:

```csv
session_id,timestamp_ns,channel,value,unit,tracker_type,quality_flag
S001,1730000000000000000,ppg_green,12345,raw_count,PPG_CONTINUOUS,
S001,1730000000040000000,ppg_green,12360,raw_count,PPG_CONTINUOUS,
S001,1730000000000000000,accel_x,0.12,g,ACCELEROMETER_CONTINUOUS,
```

This schema is illustrative only. Use the SDK's real timestamp units and sample representation; do not invent timestamps by assuming evenly spaced samples if the SDK supplies actual timestamps. If data arrive as arrays, store the event timestamp plus the sample timing convention documented by Samsung.

Prefer separate files or tables for:
- raw samples,
- session metadata,
- event markers,
- reference measurements,
- derived features.

Never overwrite the raw file with a filtered signal.

### Session metadata example

```json
{
  "session_id": "S001",
  "participant_code": "P001",
  "watch_model": "fill-in-exact-model",
  "watch_os_version": "fill-in",
  "sensor_sdk_version": "fill-in",
  "tracker_type": "fill-in",
  "nominal_sampling_rate_hz": 25,
  "channels": ["ppg_green", "ppg_red", "ppg_ir", "accel_x", "accel_y", "accel_z"],
  "posture": "seated",
  "activity": "rest",
  "notes": "Example only; replace with observed metadata"
}
```

Only list channels that the device really supplied. The sampling rate shown is an example for a continuous PPG tracker, not a universal default.

## 7. Step 3 — Design a synchronized research protocol

If the target is glucose or another biomarker, the reference measurement is essential.

- Obtain the target measurement using a validated method appropriate for the research question.
- Record exact measurement timestamps, units, device/method, and any quality/uncertainty information.
- Align sensor windows with the reference measurement using a pre-specified time window that is physiologically and scientifically justified.
- Avoid pairing a PPG segment with a glucose value recorded much earlier or later without a rationale.
- Capture context likely to confound PPG: activity, posture, temperature, time of day, meals, hydration, and sensor fit.
- Predefine exclusions and quality thresholds before testing the model.
- Use ethical review/consent where required; do not intentionally alter medication or glucose for an experiment without appropriate clinical oversight.

**Avoid leakage:** If the same person contributes many sessions, all sessions from that person should generally stay in the same train/test group when estimating performance on unseen people. If the intended use is personalized prediction, evaluate on later held-out sessions from the same participant separately.

## 8. Step 4 — Clean and inspect PPG

Use Python (NumPy, pandas, SciPy, Matplotlib). Recommended order:

1. Check timestamps, duplicates, gaps, clipping, and missing values.
2. Estimate the actual sampling rate from timestamps; compare it with the configured rate.
3. Plot raw channels before filtering.
4. Detect motion and poor-contact segments using signal checks and accelerometer context.
5. Remove baseline drift and filter a copy of the signal.
6. Compare raw and filtered plots to ensure filtering has not distorted peaks.
7. Keep the raw stream and all processing parameters for reproducibility.

A band-pass range around 0.5–5 Hz can be a reasonable *initial experiment* for pulse-oriented analysis, but it is not universally correct. Select cutoffs based on target pulse range, sampling rate, noise, and feature being measured. Filtering can change pulse shape and timing, so morphology features should be checked under alternative reasonable settings.

For offline analysis, zero-phase filters such as `scipy.signal.sosfiltfilt` can be useful. They use future samples and are **not** directly suitable for real-time causal operation. For real-time systems use causal filters and account for phase/group delay.

### Simple preprocessing example

```python
import numpy as np
from scipy.signal import butter, sosfiltfilt

def filter_ppg(x, fs, low_hz=0.5, high_hz=5.0, order=3):
    x = np.asarray(x, dtype=float)
    if x.ndim != 1:
        raise ValueError("Expected one-dimensional PPG signal")
    if not np.all(np.isfinite(x)):
        raise ValueError("Handle missing/non-finite samples before filtering")
    if not (0 < low_hz < high_hz < fs / 2):
        raise ValueError("Cutoffs must be between 0 and Nyquist frequency")
    sos = butter(order, [low_hz, high_hz],
                 btype="bandpass", fs=fs, output="sos")
    return sosfiltfilt(sos, x)
```

Filter each uninterrupted segment separately. Do not filter across large gaps or concatenate unrelated sessions.

## 9. Step 5 — Detect beats and segment pulses

1. Detect candidate systolic peaks in a filtered PPG channel.
2. Use a minimum peak distance based on a plausible heart-rate range.
3. Use prominence or adaptive thresholds rather than local maxima alone.
4. Find a foot/trough before each systolic peak using a consistent method.
5. Segment pulse cycles from one foot to the next foot (or use another clearly documented boundary rule).
6. Reject segments with missing peaks, clipped samples, large motion, impossible duration, or poor morphology.
7. Manually inspect plots from several sessions. A peak detector is not ground truth.

If the sample rate is \(f_s\) and consecutive peaks occur at indices \(n_i\) and \(n_{i+1}\):

\[
IBI_i = \frac{n_{i+1}-n_i}{f_s}
\]

\[
HR_i = \frac{60}{IBI_i}
\]

Use actual timestamps instead of index-derived intervals if sampling is irregular or samples are missing. PPG pulse-to-pulse intervals are not identical to ECG R–R intervals; pulse transit time and detection errors can contribute differences.

## 10. Step 6 — Extract a feature set

Use a hierarchy: sample-level signal quality → beat-level morphology/timing → window-level statistics. Start small, validate each feature, then expand.

### A. Beat-level features

| Feature group | Example features | Definition / notes |
|---|---|---|
| Timing | Inter-beat interval, pulse duration, rise time, decay time | Use seconds; define boundaries consistently |
| Amplitude | Peak-to-foot amplitude, normalized amplitude | Raw optical counts are device/contact dependent; normalization may help but does not eliminate confounding |
| Morphology | Pulse width at 25/50/75% height, systolic peak position, notch/secondary-peak measures if clearly visible | Dicrotic/notch detection is unreliable on some wrist waveforms; do not force a notch where none is clear |
| Shape | Area above baseline, normalized area, slope upstroke/downstroke | Specify integration baseline and units |
| Derivative | First-derivative maximum/minimum, second-derivative extrema | Derivatives amplify noise; filter and validate carefully |
| Multi-channel | Green/IR/red amplitude ratios or channel correlations | Only if channels are truly synchronized and SDK exposes them; optical geometry/sensor processing may differ |
| Quality | Peak prominence, pulse-template correlation, clipping fraction, motion level | Use for filtering/weighting, not as a biomarker by itself |

Example definitions for a pulse segment \(p(t)\), foot baseline \(b\), and systolic peak time \(t_p\):

- Amplitude: \(A = p(t_p)-b\)
- Rise time: \(T_r = t_p-t_{foot}\)
- Pulse area: \(S = \int_{t_{foot}}^{t_{next\ foot}} [p(t)-b]\,dt\)
- Normalized pulse: \(p_{norm}(t) = [p(t)-b]/A\), only if \(A\) is safely above a noise threshold.
- Upstroke slope: estimate a local derivative near the rising edge.
- Width at 50% height: time difference between rising and falling crossings of \(b+0.5A\).

State whether width is measured on the raw, detrended, or band-pass-filtered waveform. These choices can produce different values.

### B. Window-level features

Aggregate over a defined window (for example, 30–60 seconds if the data quality and sampling permit):

- median and interquartile range of amplitude, rise time, pulse width, and pulse area;
- mean, standard deviation, median, and robust quantiles of IBI;
- proportion of rejected beats and missing samples;
- signal-to-noise proxies and template similarity;
- motion summary from accelerometer magnitude/variance;
- differences/ratios between available PPG channels;
- context variables such as skin temperature, activity, and posture, when reliably time-aligned.

For HRV-type features, use validated methods and adequate beat timing. PPG-derived pulse intervals have their own errors; do not label them ECG-equivalent HRV without validation. Frequency-domain HRV requires sufficiently long, clean intervals and careful resampling/ectopic-artifact handling.

### C. Frequency-domain features

Possible exploratory features from a window include:
- dominant pulse frequency and its corresponding pulse rate;
- power in a pre-defined frequency band;
- spectral entropy or other signal-complexity measures.

Use a clearly documented window and windowing method. Spectral features can reflect movement, periodic activity, and filter settings—not just physiology. Frequency-domain results should complement, not replace, pulse morphology analysis.

### D. Start with a manageable baseline set

A reasonable first feature table:

```text
session_id
participant_id
window_start
window_end
channel
valid_sample_fraction
motion_summary
valid_beat_fraction
median_ibi_s
ibi_sd_s
median_hr_bpm
median_pulse_amplitude
iqr_pulse_amplitude
median_rise_time_s
median_width_50_s
median_pulse_area
median_upstroke_slope
template_correlation
reference_value
reference_unit
reference_timestamp
```

Not all features will be meaningful or available in every dataset. Keep missing features as missing, record why they are missing, and do not silently impute before exploratory analysis.

## 11. Other sensor modalities

### Accelerometer

Use X/Y/Z to identify movement windows, activity transitions, and possible PPG artifacts. A common derived signal is acceleration magnitude:

\[
a_{mag}(t)=\sqrt{a_x(t)^2+a_y(t)^2+a_z(t)^2}
\]

Before combining sensors, synchronize timestamps and account for different sampling rates (Samsung documents 25 Hz for the continuous accelerometer and continuous PPG in its current specification). Resampling/interpolation should be deliberate and should not create false high-frequency detail.

### Skin temperature

Use as a contextual variable, not a direct proxy for core body temperature. Temperature can change peripheral perfusion and PPG morphology, so it can confound a model. Availability and continuous/on-demand behavior vary by model and SDK version.

### Heart rate and IBI

Use the SDK's processed HR/IBI as a comparison signal and possible additional feature. It does not replace raw PPG if morphology is your research interest.

### ECG

Where supported and authorized, ECG can help investigate cardiac timing compared with PPG pulse timing. It does not provide glucose directly, and ECG collection has separate access and protocol constraints.

### EDA, SpO₂, BIA, and other data

These can add context in specific studies, but availability varies. SpO₂ is a processed oxygen estimate, not raw PPG. BIA is typically a discrete measurement rather than a continuous stream. More channels do not automatically improve prediction; they can add confounding and missingness.

## 12. Glucose-related study design

PPG features may reflect vascular and autonomic physiology, but they are influenced by many factors unrelated to glucose. A model can appear accurate by learning person identity, time of day, exercise, meals, or sensor contact rather than glucose.

For any glucose investigation:

1. Use an appropriate validated reference (for example, a properly used glucose meter or approved CGM for the study question).
2. Record reference timestamps, units, and device/method.
3. Predefine the PPG-to-reference alignment rule and rationale.
4. Collect enough variation in the target and confounders; do not infer accuracy from a few paired points.
5. Include repeated measurements across days and participants where possible.
6. Evaluate on held-out participants and, separately, future sessions.
7. Compare against simple baselines, including a model that uses only participant/context information, to detect leakage.
8. Report uncertainty, missingness, subgroup performance, calibration, and failure cases.
9. Do not claim non-invasive glucose measurement unless strong independent evidence supports it.
10. Do not change medication, diet, or glucose levels for experimentation without appropriate clinical oversight.

**A safer early research goal:** investigate signal quality, pulse morphology, and within-person changes before claiming biomarker prediction.

## 13. Machine learning and validation

### Suggested order

1. Plot raw and filtered signals.
2. Verify peak/foot detection manually on representative samples.
3. Measure repeatability of each feature across stable resting recordings.
4. Explore feature distributions and correlation with reference values.
5. Build a simple baseline (linear regression or regularized regression).
6. Compare with tree-based models only after a leakage-safe baseline works.
7. Use group splits by participant for unseen-person generalization.
8. Use nested cross-validation or a separate validation set for tuning; keep a final test set untouched.
9. Report metrics suitable for the target, including MAE/RMSE and calibration for regression, and uncertainty intervals where possible.
10. For glucose, assess error across the clinically relevant range and use applicable clinical standards if moving toward medical claims. Ordinary correlation or \(R^2\) alone is insufficient.

### Common leakage traps

- Randomly splitting individual beats from the same person into train and test.
- Using overlapping windows from one recording in both sets.
- Including session identifiers, future data, or reference values indirectly in features.
- Tuning thresholds on the final test set.
- Comparing a model with a baseline that uses less information without reporting the difference.

## 14. Suggested repository structure

```text
galaxy-watch-biosignal-research/
├── README.md
├── LICENSE
├── CITATION.cff
├── docs/
│   ├── sensor-access.md
│   ├── study-protocol.md
│   └── data-dictionary.md
├── android-watch-app/
│   └── README.md
├── data/
│   ├── raw/                 # Keep private; normally gitignored
│   ├── metadata/
│   └── processed/
├── notebooks/
│   ├── 01_signal_qc.ipynb
│   ├── 02_filtering_and_peaks.ipynb
│   ├── 03_feature_extraction.ipynb
│   └── 04_feature_validation.ipynb
├── src/
│   ├── io.py
│   ├── quality.py
│   ├── preprocessing.py
│   ├── peaks.py
│   ├── features.py
│   └── evaluation.py
├── tests/
│   ├── test_timestamps.py
│   └── test_features.py
├── requirements.txt
└── .gitignore
```

Example `.gitignore`:

```gitignore
data/raw/
data/processed/
*.csv
*.parquet
*.edf
*.fit
.env
.DS_Store
__pycache__/
.ipynb_checkpoints/
```

Do not commit participant-level biosignals, glucose records, access tokens, or identifiable metadata. Consider committing only synthetic/example data and code.

## 15. Starter Python pipeline

This is an **offline analysis template**, not a medical algorithm. It expects one regularly sampled PPG channel in a CSV column named `ppg`. Set `FS` to the actual sampling rate for the tracker. Review plots before trusting the output.

Install dependencies:

```bash
python -m pip install numpy pandas scipy matplotlib
```

Create `src/features.py` or run as a notebook cell:

```python
import numpy as np
import pandas as pd
from scipy.signal import butter, sosfiltfilt, find_peaks, peak_widths

FS = 25.0  # Example for continuous PPG; verify actual tracker rate.

def preprocess_ppg(x, fs=FS, low_hz=0.5, high_hz=5.0):
    x = np.asarray(x, dtype=float)
    if x.ndim != 1 or len(x) < int(fs * 5):
        raise ValueError("Provide at least 5 seconds of one-dimensional PPG.")
    if not np.all(np.isfinite(x)):
        raise ValueError("Split/repair missing data before filtering.")
    if not (0 < low_hz < high_hz < fs / 2):
        raise ValueError("Filter cutoffs must be below Nyquist frequency.")
    sos = butter(3, [low_hz, high_hz], btype="bandpass",
                 fs=fs, output="sos")
    return sosfiltfilt(sos, x)

def extract_window_features(x, fs=FS):
    x = np.asarray(x, dtype=float)
    filtered = preprocess_ppg(x, fs)

    # Illustrative thresholds. Tune only on development data and inspect plots.
    peaks, props = find_peaks(
        filtered,
        distance=max(1, int(0.30 * fs)),
        prominence=0.5 * np.std(filtered)
    )

    if len(peaks) < 3:
        return {"valid": False, "reason": "too_few_peaks"}

    # Interval between consecutive detected peaks.
    ibi = np.diff(peaks) / fs
    valid_ibi = ibi[(ibi >= 0.30) & (ibi <= 2.0)]

    amplitudes, rise_times, areas, widths50 = [], [], [], []

    # For each peak, use the minimum between the previous and current peak
    # as a simple foot/trough estimate. This is not a universal foot detector.
    for i in range(1, len(peaks)):
        left, peak = int(peaks[i - 1]), int(peaks[i])
        if peak - left < 2:
            continue

        segment = filtered[left:peak + 1]
        foot = left + int(np.argmin(segment))
        if not (foot < peak):
            continue

        amp = filtered[peak] - filtered[foot]
        if amp <= 0:
            continue

        amplitudes.append(amp)
        rise_times.append((peak - foot) / fs)

        pulse = filtered[foot:peak + 1] - filtered[foot]
        areas.append(np.trapezoid(pulse, dx=1 / fs))

        # Width at 50% of peak prominence is a rough morphology feature.
        width = peak_widths(filtered, [peak], rel_height=0.5)[0][0] / fs
        widths50.append(width)

    if not valid_ibi.size or not amplitudes:
        return {"valid": False, "reason": "no_valid_intervals_or_pulses"}

    return {
        "valid": True,
        "n_samples": int(len(x)),
        "duration_s": float(len(x) / fs),
        "n_detected_peaks": int(len(peaks)),
        "n_valid_ibi": int(len(valid_ibi)),
        "median_ibi_s": float(np.median(valid_ibi)),
        "median_hr_bpm": float(60.0 / np.median(valid_ibi)),
        "ibi_sd_s": float(np.std(valid_ibi, ddof=1)) if len(valid_ibi) > 1 else np.nan,
        "median_amplitude": float(np.median(amplitudes)),
        "iqr_amplitude": float(np.percentile(amplitudes, 75) - np.percentile(amplitudes, 25)),
        "median_rise_time_s": float(np.median(rise_times)),
        "median_width50_s": float(np.median(widths50)),
        "median_pulse_area": float(np.median(areas)),
    }

if __name__ == "__main__":
    df = pd.read_csv("ppg.csv")
    x = df["ppg"].to_numpy(dtype=float)

    result = extract_window_features(x, FS)
    print(pd.Series(result))
```

### Notes on this template

- For a 25 Hz continuous stream, the Nyquist frequency is 12.5 Hz; the illustrative 5 Hz upper cutoff is below that limit. At other sample rates, check the filter constraints.
- The simple trough logic and fixed prominence threshold can fail on real wrist PPG. Plot every stage and improve detection before large-scale analysis.
- `peak_widths` measures width relative to peak prominence in the supplied filtered signal; it is not necessarily the clinical or physiological pulse width you intend. Define and document your width method.
- Do not compute across gaps, concatenate sessions, or treat interpolated data as real samples.
- Feature amplitude depends on sensor configuration and fit; do not compare absolute raw counts across devices as if they were calibrated physical units.
- At low sample rates, timing and morphology resolution are limited. A 25 Hz stream has a 40 ms sample interval, which may be too coarse for some fine morphology features. Check the SDK's actual rate and validate the feature's repeatability.
- Add unit tests using synthetic signals with known peak times, and test missing data, clipping, motion, and short windows.
- Keep feature definitions and algorithm versions with each result.

## 16. Quality checks and common failures

| Symptom | Possible explanation | First check |
|---|---|---|
| No obvious pulse | Poor contact, weak perfusion, wrong channel, or sensor access issue | Plot raw green/red/IR separately; inspect sensor placement |
| Many extra peaks | Motion, threshold too low, secondary waveform features | Inspect peak markers; improve quality gating |
| Implausible HR | Incorrect sample rate, missed/double peaks, timestamp gaps | Recompute intervals from real timestamps |
| Feature values drift between sessions | Temperature, contact pressure, position, hardware processing, or physiological changes | Compare metadata and signal quality before interpreting biology |
| PPG channels disagree | Different optical wavelengths and signal quality | Analyze channels separately first |
| Model works only on random split | Participant/session leakage or confounding | Use participant-wise or time-wise held-out validation |
| Apparent glucose relationship disappears after adjustment | Confounding or weak/no signal | Report honestly; do not keep tuning on the test set |

## 17. A staged roadmap

### Phase 1 — Sensor access and reproducibility
- Confirm model/SDK/tracker support.
- Collect raw PPG and accelerometer data.
- Save timestamps and metadata.
- Verify real sampling rate, missing data, and battery/runtime limits.

### Phase 2 — Signal quality
- Plot raw channels.
- Compare stationary and movement segments.
- Build a quality score or artifact flag.
- Document exclusion rules.

### Phase 3 — Feature extraction
- Detect pulses and validate visually.
- Calculate timing, amplitude, width, area, slope, and quality features.
- Summarize them per fixed window.
- Test repeatability across sessions.

### Phase 4 — Physiological context
- Add accelerometer and temperature context where available.
- Align all sensor streams and event markers.
- Compare raw-PPG-derived intervals with SDK HR/IBI; investigate disagreements.

### Phase 5 — Biomarker study
- Define the scientific question and reference measurement.
- Collect paired data ethically and safely.
- Pre-register or document the analysis plan.
- Evaluate leakage-safe baselines and independent generalization.
- Report negative findings and limitations.

### Phase 6 — Reproducible release
- Publish code, feature definitions, configuration, and synthetic examples.
- Keep private health data out of Git.
- Include software versions, study protocol, and limitations.

## 18. References and official documentation

### Samsung platform and API documentation

1. **Samsung Health Sensor SDK overview** — supported sensor streams and raw PPG availability.  
   https://developer.samsung.com/health/sensor/overview.html

2. **Samsung Health Sensor SDK introduction** — setup, target devices, library, samples, and limitations.  
   https://developer.samsung.com/health/sensor/guide/introduction.html

3. **Health Sensor Data Specifications** — tracker types, documented rates, raw vs processed signals, and on-demand constraints.  
   https://developer.samsung.com/health/sensor/guide/data-specifications.html

4. **Samsung Health Sensor SDK API reference overview** — tracker and data classes.  
   https://developer.samsung.com/health/sensor/api-reference/overview-summary.html

5. **Samsung Health Sensor SDK FAQ** — developer mode and supported continuous trackers.  
   https://developer.samsung.com/health/sensor/faq.html

6. **Health Connect FAQ for Samsung Health data** — synchronization, permissions, and what records are available through Health Connect.  
   https://developer.samsung.com/health/health-connect-faq.html

7. **Samsung Health Data SDK overview** — supported stored health records and SDK constraints.  
   https://developer.samsung.com/health/data/overview.html

### Signal processing, datasets, and tools

8. **SciPy signal processing documentation** — filtering, peak detection, peak widths, and signal utilities.  
   https://docs.scipy.org/doc/scipy/reference/signal.html

9. **NeuroKit2 documentation** — open-source physiological signal processing functions, including PPG-related analysis. Review methods and validate them for wrist-worn data.  
   https://neuropsychology.github.io/NeuroKit/

10. **PhysioNet** — research physiological datasets and resources. Dataset permissions and sensor provenance differ; a dataset is not automatically equivalent to Galaxy Watch wrist PPG.  
    https://physionet.org/

11. **PPG-DaLiA dataset** — wrist PPG and accelerometer data in daily-life conditions, useful for learning about motion artifacts and wearable PPG. Verify the original paper, protocol, and license before use.  
    https://archive.ics.uci.edu/dataset/495/ppg+dalia

12. **Health Connect documentation** — Android health-data sharing APIs.  
    https://developer.android.com/health-and-fitness/guides/health-connect

### How to use these references

- Use Samsung documentation as the source of truth for the current watch/SDK's data access and sampling behavior.
- Use SciPy or NeuroKit2 for candidate algorithms, but do not assume an algorithm validated on finger PPG or clinical sensors transfers unchanged to wrist PPG.
- Use public datasets to prototype signal processing, not as proof of glucose prediction.
- Before using any dataset or code in a publication or product, check license, citation, consent, and usage restrictions.

---

## Final recommendation

Start with a narrow, measurable objective: **collect one raw PPG channel and accelerometer data, verify timestamps and sampling rate, visualize the waveform, and extract a small set of beat-level features with quality flags.** Only after the pipeline is reliable should you add more channels or attempt biomarker modeling.

The most important early deliverable is not a glucose-prediction model. It is a reliable, reproducible dataset and feature-extraction pipeline that makes it possible to test a scientific hypothesis honestly.
