# Python PPG Signal Processing and Feature Extraction

## A Practical, Research-Oriented Guide with Waveform Visualizations

**Document type:** Technical README / reproducible research guide\
**Focus:** Python workflows for PPG preprocessing, quality assessment,
pulse detection, waveform visualization, and feature extraction\
**Companion topic:** Personalized PPG baseline estimation and artifact
handling\
**Status:** Educational workflow; validate all choices for the target
device, population, and physiological outcome.

------------------------------------------------------------------------

## Abstract

Photoplethysmography (PPG) is an optical measurement of pulsatile
blood-volume changes. Raw PPG recordings can contain baseline drift,
motion artifacts, ambient-light interference, clipping, missing samples,
sensor-contact changes, and electronic noise. Meaningful feature
extraction therefore requires more than applying a filter and detecting
peaks. A reproducible workflow should inspect the raw signal, verify
timestamps and sampling rate, identify corrupted segments, apply
conservative preprocessing, detect candidate pulses, assess signal
quality, extract interpretable features, and validate the resulting
estimates against appropriate references.

This README presents a Python-oriented workflow using NumPy, pandas,
SciPy, Matplotlib, and optionally NeuroKit2. It includes code for
loading data, plotting raw and processed waveforms, filtering, peak
detection, beat segmentation, morphology visualization, feature
extraction, and a basic quality-control report. It also explains common
pitfalls, feature families, validation practices, and how to build a
personalized baseline from high-quality beats.

**Important:** Example filter settings and thresholds are starting
points, not universal clinical standards. The correct choices depend on
sampling rate, sensor type, population, activity, and research
objective.

------------------------------------------------------------------------

## 1. What can be extracted from PPG?

PPG features can be grouped into several families.

  -----------------------------------------------------------------------
  Feature family          Example features        Common uses / cautions
  ----------------------- ----------------------- -----------------------
  Pulse timing            Pulse rate,             Pulse rate is usually
                          pulse-to-pulse          more robust than subtle
                          intervals, inter-beat   variability features;
                          interval variability    intervals require
                                                  accurate beat detection

  Amplitude               Peak-to-trough          Depends strongly on
                          amplitude, pulse        sensor fit, gain, site,
                          amplitude variability,  temperature, and
                          perfusion-related       perfusion
                          indices                 

  Morphology              Rise time, pulse width, Requires consistent
                          decay time, area,       pulse segmentation and
                          slopes, normalized      adequate signal quality
                          pulse shape             

  Derivative morphology   First-derivative        Sensitive to noise and
                          extrema,                filtering choices
                          second-derivative       
                          features, curvature     

  Frequency domain        Spectral peak, band     Window length and
                          power, spectral entropy nonstationarity matter

  Quality / artifact      SQI, clipping ratio,    Essential for deciding
                          missing-sample rate,    which features are
                          motion level, template  trustworthy
                          similarity              

  Context                 Activity, posture,      Helps interpret
                          temperature, device,    between-recording
                          site, session           differences
  -----------------------------------------------------------------------

**Terminology caution:** PPG pulse-rate variability (PRV) is not always
interchangeable with ECG-derived heart-rate variability (HRV). ECG
measures electrical cardiac timing, whereas PPG measures peripheral
pulse arrival, which is influenced by pulse transit and vascular
dynamics.

------------------------------------------------------------------------

## 2. Recommended Python environment

A simple environment is enough for a first implementation.

``` bash
python -m venv .venv

# macOS / Linux
source .venv/bin/activate

# Windows PowerShell
# .venv\Scripts\Activate.ps1

python -m pip install --upgrade pip
pip install numpy pandas scipy matplotlib
```

Optional tools:

``` bash
pip install neurokit2
```

Use NeuroKit2 as an optional comparison for PPG processing and peak
detection. Check the package version and documentation for the exact API
before building a long-term pipeline.

### Suggested project layout

``` text
ppg-research/
├── README.md
├── requirements.txt
├── data/
│   ├── raw/
│   └── processed/
├── outputs/
│   ├── figures/
│   ├── tables/
│   └── reports/
└── src/
    ├── io_utils.py
    ├── preprocessing.py
    ├── quality.py
    ├── beats.py
    ├── features.py
    └── run_pipeline.py
```

Keep original raw files unchanged. Save processed data as separate
outputs and record every processing parameter.

------------------------------------------------------------------------

## 3. Input data assumptions

For the examples below, assume a CSV with a time column and one PPG
channel:

``` csv
time_s,ppg
0.000,512
0.010,519
0.020,533
0.030,548
...
```

The example implies 100 Hz sampling. Your own sampling rate may differ.

If the file only contains a PPG column, you must know the sampling
frequency from the device metadata. Do not guess it from the number of
samples.

### Load and inspect data

``` python
from pathlib import Path
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

csv_path = Path("data/raw/recording.csv")
df = pd.read_csv(csv_path)

print(df.head())
print(df.dtypes)
print(df.isna().sum())

ppg = pd.to_numeric(df["ppg"], errors="coerce").to_numpy(dtype=float)

if "time_s" in df.columns:
    time_s = pd.to_numeric(df["time_s"], errors="coerce").to_numpy(dtype=float)
    valid_time = np.isfinite(time_s)
    if not valid_time.all():
        raise ValueError("Time column contains invalid values.")
    dt = np.diff(time_s)
    print("Median sampling interval:", np.median(dt))
    print("Estimated sampling rate:", 1 / np.median(dt))
else:
    fs = 100.0  # Replace with the actual device sampling rate
    time_s = np.arange(len(ppg)) / fs

print("Samples:", len(ppg))
print("Duration (s):", time_s[-1] - time_s[0])
print("NaN / Inf samples:", (~np.isfinite(ppg)).sum())
```

Check for timestamp gaps and irregular sampling. Standard digital
filters assume a known and usually uniform sampling interval. If
timestamps are irregular, investigate the cause before resampling.

------------------------------------------------------------------------

## 4. Visualize the raw signal first

Never start by filtering without looking at the raw recording.

``` python
fig, ax = plt.subplots(figsize=(14, 4))
ax.plot(time_s, ppg, linewidth=0.8)
ax.set(title="Raw PPG", xlabel="Time (s)", ylabel="Sensor units")
ax.grid(True, alpha=0.3)
fig.tight_layout()
plt.show()
```

Look for:

-   Plausible repeating pulses
-   Slow baseline drift
-   Abrupt jumps or dropouts
-   Flat or clipped regions
-   Strong motion-induced distortion
-   Unusually small pulse amplitude
-   Irregular sampling or missing data

Sensor units may be ADC counts, voltage, or arbitrary device units.
Unless the hardware is calibrated, do not label raw values as blood
volume or absolute optical intensity.

------------------------------------------------------------------------

## 5. Sampling rate and filter design

The sampling rate (f_s) is needed for filter design and conversion
between samples and seconds.

A common starting point for adult pulse analysis is a bandpass somewhere
around 0.5--8 Hz or 0.5--10 Hz, depending on the target. These are
illustrative ranges only. Lower cutoffs may remove slow baseline drift
but can also attenuate slow physiological modulation. Higher cutoffs may
preserve sharper morphology but retain more noise.

**Choose filters based on the research target:**

-   Heart-rate estimation: a pulse-oriented band may be acceptable if
    validated.
-   HRV/PRV: preserve accurate beat timing; filtering must not shift or
    distort peaks.
-   Pulse morphology: use conservative filtering and inspect the effect
    on shape.
-   Respiration-related modulation: do not automatically discard the
    slow components needed for the analysis.
-   SpO₂: use the device's intended red/infrared channels and a
    validated algorithm; generic single-channel filtering is not
    sufficient.

### Butterworth bandpass example

``` python
from scipy.signal import butter, sosfiltfilt

def bandpass_ppg(x, fs, low_hz=0.5, high_hz=8.0, order=3):
    """Offline zero-phase Butterworth bandpass filter.

    This function expects a finite, evenly sampled signal.
    Do not pass NaNs or large gaps directly into the filter.
    """
    x = np.asarray(x, dtype=float)

    if not np.isfinite(x).all():
        raise ValueError("Signal contains NaN/Inf; handle gaps before filtering.")
    if not (0 < low_hz < high_hz < fs / 2):
        raise ValueError("Require 0 < low_hz < high_hz < Nyquist frequency.")

    sos = butter(
        order,
        [low_hz, high_hz],
        btype="bandpass",
        fs=fs,
        output="sos"
    )
    return sosfiltfilt(sos, x)

fs = 100.0  # Replace with actual sampling rate
ppg_filtered = bandpass_ppg(ppg, fs, low_hz=0.5, high_hz=8.0)
```

`sosfiltfilt` performs forward-backward filtering, avoiding net phase
delay for offline analysis. It is non-causal and uses future samples; it
is not appropriate as-is for a real-time streaming system. For real-time
processing, use a causal filter and evaluate its delay and waveform
distortion.

### Visualize raw versus filtered

``` python
fig, axes = plt.subplots(2, 1, figsize=(14, 7), sharex=True)

axes[0].plot(time_s, ppg, linewidth=0.8)
axes[0].set_title("Raw PPG")
axes[0].set_ylabel("Sensor units")
axes[0].grid(True, alpha=0.3)

axes[1].plot(time_s, ppg_filtered, linewidth=0.9)
axes[1].set_title("Filtered PPG")
axes[1].set_xlabel("Time (s)")
axes[1].set_ylabel("Filtered units")
axes[1].grid(True, alpha=0.3)

fig.tight_layout()
plt.show()
```

Inspect several short segments at high zoom. A filter that looks good
over a long window may distort individual pulses or create edge
artifacts.

------------------------------------------------------------------------

## 6. Baseline drift and detrending

Baseline drift may come from slow contact changes, movement,
temperature, or optical coupling. Options include a high-pass filter,
detrending, or a slowly varying baseline estimate. No method can
automatically determine whether every slow change is noise.

For a simple offline comparison:

``` python
from scipy.signal import detrend

ppg_detrended = detrend(ppg, type="linear")
```

Linear detrending removes a global linear trend; it is not a general
solution to nonlinear drift. Compare raw, detrended, and filtered
signals and preserve a copy of the original.

------------------------------------------------------------------------

## 7. Detect candidate pulse peaks

Peak detection is a candidate-generation step, not proof that each peak
is a true pulse. Motion artifacts can create false peaks; low perfusion
can cause missed peaks.

A minimum peak distance can be estimated from a plausible maximum pulse
rate. For example, at 100 Hz and a maximum candidate rate of 200
beats/min, the minimum separation is approximately 30 samples. This is
only a starting constraint.

``` python
from scipy.signal import find_peaks

def detect_ppg_peaks(x, fs, min_bpm=40, max_bpm=200, prominence=None):
    """Return candidate peak indices and peak properties."""
    x = np.asarray(x, dtype=float)
    if not np.isfinite(x).all():
        raise ValueError("Handle gaps before peak detection.")

    min_distance = max(1, int(fs * 60.0 / max_bpm))
    peaks, properties = find_peaks(
        x,
        distance=min_distance,
        prominence=prominence
    )
    return peaks, properties

peaks, peak_props = detect_ppg_peaks(
    ppg_filtered,
    fs,
    min_bpm=40,
    max_bpm=200,
    prominence=None
)

fig, ax = plt.subplots(figsize=(14, 4))
ax.plot(time_s, ppg_filtered, label="Filtered PPG", linewidth=0.9)
ax.scatter(time_s[peaks], ppg_filtered[peaks], s=22, marker="x", label="Candidate peaks")
ax.set(title="Candidate pulse peaks", xlabel="Time (s)", ylabel="Filtered units")
ax.legend()
ax.grid(True, alpha=0.3)
fig.tight_layout()
plt.show()
```

### Important peak-detection considerations

-   Tune prominence and distance on representative recordings, not just
    one clean example.
-   Use polarity correction if the device's pulses are inverted.
-   A PPG systolic peak is not always the best fiducial point for pulse
    timing.
-   For PRV, timing errors of even a few samples may matter.
-   Use a quality check and, where possible, an independent ECG
    reference to evaluate peak detection.
-   Do not interpolate missed beats silently.

------------------------------------------------------------------------

## 8. Calculate pulse rate and pulse-to-pulse intervals

Given detected peak indices, compute the time between consecutive peaks.
These are pulse-to-pulse intervals, not ECG R--R intervals.

``` python
peak_times = time_s[peaks]
pulse_intervals_s = np.diff(peak_times)

# Basic interval screening: illustrative only; adapt to population and protocol.
valid_interval = (
    (pulse_intervals_s >= 60 / 200) &
    (pulse_intervals_s <= 60 / 40)
)
valid_intervals_s = pulse_intervals_s[valid_interval]

pulse_rate_bpm = 60.0 / pulse_intervals_s

print("Median pulse rate (bpm):", np.nanmedian(pulse_rate_bpm))
print("Number of candidate peaks:", len(peaks))
print("Number of pulse intervals:", len(pulse_intervals_s))
print("Intervals passing the illustrative range:", valid_interval.sum())
```

Avoid calculating variability metrics from a heavily corrupted interval
series. Interval screening should be pre-specified and validated, and
rejected intervals should be recorded rather than silently discarded.

------------------------------------------------------------------------

## 9. Segment and visualize individual pulses

For morphology features, define a consistent pulse window around each
candidate beat. A simple window between adjacent peaks can be useful for
visualization, but it is not a physiological pulse-onset detector.
Better morphology work should identify pulse onset consistently and
handle ectopic or ambiguous beats explicitly.

``` python
def segment_between_peaks(x, peaks, min_samples=3):
    """Segment signal between consecutive detected peaks."""
    segments = []
    bounds = []
    for left, right in zip(peaks[:-1], peaks[1:]):
        if right - left >= min_samples:
            segments.append(np.asarray(x[left:right + 1], dtype=float))
            bounds.append((int(left), int(right)))
    return segments, bounds

segments, bounds = segment_between_peaks(ppg_filtered, peaks)

if segments:
    fig, ax = plt.subplots(figsize=(10, 4))
    for i, seg in enumerate(segments[:20]):
        phase = np.linspace(0, 1, len(seg))
        ax.plot(phase, seg, alpha=0.35, linewidth=0.8)
    ax.set(
        title="Example consecutive-peak segments (not onset-aligned)",
        xlabel="Normalized segment phase",
        ylabel="Filtered units"
    )
    ax.grid(True, alpha=0.3)
    fig.tight_layout()
    plt.show()
```

### Build a median morphology template

For an initial shape comparison, resample accepted beat segments to a
fixed number of points and take their pointwise median. Use only
high-quality beats, and understand that segments bounded by peaks may
not align at pulse onset.

``` python
from scipy.signal import resample

def median_template(segments, n_points=200):
    if not segments:
        raise ValueError("No segments provided.")
    normalized = np.vstack([
        resample(np.asarray(seg, dtype=float), n_points)
        for seg in segments
    ])
    template = np.median(normalized, axis=0)
    q25 = np.percentile(normalized, 25, axis=0)
    q75 = np.percentile(normalized, 75, axis=0)
    return normalized, template, q25, q75

normalized_beats, template, q25, q75 = median_template(segments)

phase = np.linspace(0, 1, len(template))
fig, ax = plt.subplots(figsize=(10, 4))
ax.fill_between(phase, q25, q75, alpha=0.2, label="Interquartile range")
ax.plot(phase, template, linewidth=2, label="Median template")
ax.set(
    title="Illustrative median PPG segment template",
    xlabel="Normalized segment phase",
    ylabel="Filtered units"
)
ax.legend()
ax.grid(True, alpha=0.3)
fig.tight_layout()
plt.show()
```

This code demonstrates a computational pattern, not a validated
beat-quality algorithm. For research-grade templates, segment from a
consistent pulse-onset point, exclude low-quality beats, and avoid
combining different physiological states without justification.

------------------------------------------------------------------------

## 10. Feature extraction

Feature extraction should be tied to a research hypothesis. Start with a
small, interpretable set and add features only when their reliability
and relevance can be justified.

### 10.1 Timing features

-   Pulse rate (beats/min)
-   Pulse-to-pulse intervals (seconds or milliseconds)
-   Mean and median pulse interval
-   Standard deviation of intervals
-   Robust interval dispersion, such as median absolute deviation

These interval statistics are not automatically equivalent to standard
ECG HRV metrics. Use validated definitions and sufficiently clean data
before reporting HRV/PRV metrics.

### 10.2 Amplitude features

For a segment with a defined baseline or trough and systolic peak:

-   Peak amplitude
-   Trough-to-peak amplitude
-   Beat amplitude median and variability
-   Normalized amplitude

Amplitude is particularly sensitive to sensor contact, device gain,
perfusion, and placement. Treat it as a relative feature unless the
measurement is calibrated.

### 10.3 Morphology features

Potential features include:

-   Rise time: onset-to-systolic-peak time
-   Pulse width at a specified relative amplitude
-   Area under the pulse
-   Maximum upstroke slope
-   Maximum downstroke slope
-   Pulse duration
-   Shape correlation with a personal template

These require reliable onset, peak, and end-point definitions. A window
between two systolic peaks is not necessarily equivalent to an
onset-to-onset pulse cycle.

### 10.4 Frequency-domain features

Possible features include dominant spectral frequency and band power.
These are generally calculated over windows rather than individual
beats.

``` python
from scipy.signal import welch

frequencies, psd = welch(ppg_filtered, fs=fs, nperseg=min(len(ppg_filtered), int(fs * 20)))
```

Interpret spectral results carefully: motion can create strong peaks,
and a dominant frequency is not necessarily heart rate.

### 10.5 Basic feature-extraction example

The following code extracts simple features from segments between
consecutive detected peaks. Because those segments are not
onset-aligned, rise time and area are segment-level descriptors rather
than definitive physiological pulse features.

``` python
from scipy.stats import skew, kurtosis

def extract_segment_features(x, fs):
    x = np.asarray(x, dtype=float)
    if len(x) < 4 or not np.isfinite(x).all():
        return {}

    duration_s = (len(x) - 1) / fs
    peak_idx = int(np.argmax(x))
    trough_idx = int(np.argmin(x))

    # Approximate shape and amplitude descriptors
    amplitude = float(np.max(x) - np.min(x))
    area = float(np.trapz(x - np.min(x), dx=1/fs))
    max_slope = float(np.max(np.diff(x) * fs))
    min_slope = float(np.min(np.diff(x) * fs))

    return {
        "segment_duration_s": duration_s,
        "segment_min": float(np.min(x)),
        "segment_max": float(np.max(x)),
        "peak_to_trough_amplitude": amplitude,
        "peak_position_fraction": peak_idx / max(1, len(x) - 1),
        "trough_position_fraction": trough_idx / max(1, len(x) - 1),
        "area_above_segment_min": area,
        "max_slope_units_per_s": max_slope,
        "min_slope_units_per_s": min_slope,
        "standard_deviation": float(np.std(x, ddof=1)),
        "skewness": float(skew(x, bias=False)),
        "kurtosis_excess": float(kurtosis(x, fisher=True, bias=False)),
    }

feature_rows = []
for i, seg in enumerate(segments):
    row = {"segment_index": i}
    row.update(extract_segment_features(seg, fs))
    feature_rows.append(row)

features_df = pd.DataFrame(feature_rows)
features_df.to_csv("outputs_segment_features.csv", index=False)
print(features_df.head())
```

Feature names and definitions should be included in a data dictionary.
Verify unit conventions and ensure all features are computed from
comparable windows.

------------------------------------------------------------------------

## 11. A basic signal-quality report

A first-stage report can quantify missing data, flatness, clipping
proxies, and pulse-template variability. These are diagnostic
indicators, not a complete SQI.

``` python
def basic_quality_report(x):
    x = np.asarray(x, dtype=float)
    finite = np.isfinite(x)
    xf = x[finite]

    report = {
        "n_samples": int(len(x)),
        "finite_fraction": float(finite.mean()) if len(x) else np.nan,
        "missing_or_nonfinite_fraction": float(1 - finite.mean()) if len(x) else np.nan,
    }

    if len(xf) == 0:
        return report

    report.update({
        "mean": float(np.mean(xf)),
        "std": float(np.std(xf)),
        "min": float(np.min(xf)),
        "max": float(np.max(xf)),
        "unique_value_count": int(np.unique(xf).size),
        "flat_fraction": float(np.mean(np.diff(xf) == 0)) if len(xf) > 1 else np.nan,
    })
    return report

print(basic_quality_report(ppg))
```

A flat fraction is not sufficient to diagnose clipping. If the device
provides ADC limits, use those known limits to detect saturation. For
realistic SQI, combine multiple validated indicators and label known
artifact examples.

------------------------------------------------------------------------

## 12. Optional NeuroKit2 comparison

NeuroKit2 offers signal-processing utilities for physiological signals,
including PPG workflows. It can be useful as a comparison against a
custom pipeline.

``` python
# Optional dependency: pip install neurokit2
import neurokit2 as nk

# Check the installed version and current documentation.
# API details may differ across versions.
signals, info = nk.ppg_process(ppg, sampling_rate=int(fs))

nk.ppg_plot(signals, sampling_rate=int(fs))
```

Treat this as an illustrative entry point. Verify the exact API and
outputs for your installed version, inspect the package's quality
assumptions, and validate peak detection on your dataset. Do not assume
a library output is ground truth.

------------------------------------------------------------------------

## 13. Avoid common mistakes

1.  **Guessing sampling rate.** Incorrect `fs` corrupts filter design,
    timing, and frequency estimates.
2.  **Filtering through NaNs or long gaps.** Handle missing data and
    segment boundaries explicitly.
3.  **Over-filtering.** Smoothness can come at the cost of pulse
    morphology and timing.
4.  **Treating every peak as a beat.** Motion and noise can produce
    false peaks.
5.  **Using a rigid template.** Genuine pulse morphology can vary with
    physiology and posture.
6.  **Mixing incompatible sessions.** Different sensor placement or
    activity states may not belong in one baseline.
7.  **Normalizing away useful information.** Preserve raw amplitude and
    timing separately.
8.  **Reporting HRV from poor PPG.** Beat timing quality is critical;
    distinguish PRV from ECG HRV.
9.  **Ignoring rejection rates.** Report how much data the algorithm
    rejects.
10. **Evaluating only on training data.** Use held-out participants or
    sessions as appropriate.
11. **Assuming a filter removes motion artifacts.** Motion often
    overlaps with the pulse frequency.
12. **Not preserving raw data.** Keep original data and log every
    processing step.

------------------------------------------------------------------------

## 14. Recommended validation strategy

Compare at least the following:

  -----------------------------------------------------------------------
  Variant                             Purpose
  ----------------------------------- -----------------------------------
  Raw PPG                             Baseline performance

  Filtered PPG                        Effect of basic preprocessing

  Filtered + quality rejection        Effect of excluding poor segments

  Filtered + personalized template    Effect of individual morphology
  screening                           

  Motion-reference cancellation +     Effect of sensor-assisted
  quality screening                   correction

  Combined pipeline                   Overall accuracy, repeatability,
                                      and data coverage
  -----------------------------------------------------------------------

Use appropriate independent references:

-   ECG for cardiac electrical timing and beat-timing comparisons
-   A validated reference instrument for SpO₂ or blood-pressure claims
-   Independent high-quality PPG channels where available for waveform
    comparisons

For each method, report:

-   Beat-detection sensitivity and positive predictive value
-   Beat timing error
-   HR error where relevant
-   PRV/HRV metric error where appropriate
-   Morphology similarity and amplitude error
-   Repeatability across sessions
-   Fraction of data accepted or rejected
-   Performance by activity, skin-tone group, sensor site, and other
    relevant subgroups where data and study design permit

Avoid data leakage. If the goal is generalization to new people,
separate participants across training and test sets. For a personalized
model, separate enrollment/calibration sessions from subsequent
evaluation sessions.

------------------------------------------------------------------------

## 15. Research workflow checklist

-   [ ] Confirm device, channel, units, and sampling rate.
-   [ ] Preserve the raw recording and metadata.
-   [ ] Check timestamps, missing samples, clipping, and saturation.
-   [ ] Visualize the raw signal.
-   [ ] Select filters based on the target feature.
-   [ ] Visualize raw and filtered signals together.
-   [ ] Detect candidate pulses and review overlays.
-   [ ] Apply quality assessment and record rejection reasons.
-   [ ] Extract features with explicit definitions and units.
-   [ ] Build a personal template only from accepted beats.
-   [ ] Quantify within-person and between-session variability.
-   [ ] Validate against an independent reference.
-   [ ] Report both accuracy and usable-data coverage.
-   [ ] Save configuration, package versions, and random seeds where
    applicable.

------------------------------------------------------------------------

## 16. Suggested references and documentation

These are starting points for implementation and literature review.
Check current documentation and verify bibliographic details before
formal citation.

1.  **Photoplethysmogram Analysis and Applications: An Integrative
    Review**\
    https://pmc.ncbi.nlm.nih.gov/articles/PMC8920970/

2.  **Wearable Photoplethysmography for Cardiovascular Monitoring**\
    https://pmc.ncbi.nlm.nih.gov/articles/PMC7612541/

3.  **A Survey of Photoplethysmography and Imaging Photoplethysmography
    Quality Assessment Methods**\
    https://www.mdpi.com/2076-3417/12/19/9582

4.  **Heart rate tracking in photoplethysmography signals affected by
    motion artifacts: a review**\
    https://link.springer.com/article/10.1186/s13634-020-00714-2

5.  **SciPy signal-processing documentation**\
    https://docs.scipy.org/doc/scipy/reference/signal.html

6.  **NeuroKit2 documentation**\
    https://neuropsychology.github.io/NeuroKit/

7.  **NumPy documentation**\
    https://numpy.org/doc/

8.  **pandas documentation**\
    https://pandas.pydata.org/docs/

9.  **Matplotlib documentation**\
    https://matplotlib.org/stable/

------------------------------------------------------------------------

## 17. Final recommendations

For a first research-grade prototype, begin with a transparent baseline:

1.  load and validate the data;
2.  inspect raw waveforms;
3.  apply a conservative, target-appropriate filter;
4.  detect candidate pulses;
5.  review the detected peaks visually;
6.  calculate timing, amplitude, and basic morphology features;
7.  add SQI and reject unreliable segments;
8.  estimate a robust personalized template from accepted beats;
9.  validate repeatability and target-metric accuracy against reference
    data.

Only then compare more complex methods such as adaptive filtering,
wavelet denoising, decomposition, or machine learning. Complexity should
be justified by measurable improvement in accuracy, robustness, and
usable coverage---not simply by a visually smoother waveform.

**Core principle:** preserve the raw data, make each processing decision
explicit, and treat signal quality and uncertainty as first-class
outputs of the research pipeline.
