### PPG Sensor (Photoplethysmography)

A PPG sensor is an optical sensor that measures changes in blood volume beneath your skin using light. It is commonly used in smartwatches, fitness bands, pulse oximeters, and other wearable health devices.

![Haylou Solar 5 Smartwatch - Entrega en todo el mundo](https://images.openai.com/static-rsc-4/c_nS0swBW48YL7NFLs5poJhToLG2ntd_FtP-WoxC6TNm4pjxNhQ4l2SaPTio_UwqifgRn4NXrTRg-rQO3XuQDR8keqkGrxZy4PAIPwXe0YNCCm1VMsK2Ks4V15zNNXVnnbdVdR6BglcmNKIewkJoBoylNnQAVoMWlFbaJQe-1ZyFianGobf8-nkwpUE1-5F8?purpose=fullsize)

![A Programmable Gain Calibration Method to Mitigate Skin Tone Bias in PPG Sensors](https://images.openai.com/static-rsc-4/TkISXeRDOT70uv1Ogy60sk5hSbEo5rxdz-4mDtKCjuO6gist71m4N2jWp17_h881mA19P0Rn9jjaDTNqkEJiUEdtfnmtf8PolxJpfWJRdzfQcdgT48WVMr1aLnRqHXRFM5bsoabWKIK1KsmbKGHzCsabBBrbY9hzfaKxDNeEUOwAUruBuRCy-8I68wxvL9vB?purpose=fullsize)

![Diagnostic Features and Potential Applications of PPG Signal in Healthcare: A Systematic Review](https://images.openai.com/static-rsc-4/cWm1ARhQOf_K2ePw6NoEmH0GnixOu41ZmA36KAgoyQs91CLDZlLEm1fThmC6YDdwN22IMFocTDqywzzAfZwYQP0bYMn7__npvTXS4BQCzRUpd6vGjyMiFK5L3QlzQevGT9RdjIw8lam5IojzCx_eFLNf9BxpNjudtmT2t9ExLWrDPbwOcSRYj9kIbnMmyGq-?purpose=fullsize)

### 1\. How does a PPG sensor work?

A PPG sensor typically uses a light source, such as an LED, and a photodetector.

Step 1: Emit light

The LED shines light into the skin.

Step 2: Blood volume changes

With every heartbeat, the amount of blood in small blood vessels changes, affecting how light is absorbed or scattered.

Step 3: Detect the signal

A photodetector measures the changing light and converts it into an electrical signal.

Step 4: Process the data

Electronics and software filter the signal to estimate heart rate and other physiological measurements.

### 2\. What can a PPG sensor measure?

* Heart rate (BPM): Counts pulse cycles per minute.

* Blood oxygen saturation (SpO₂): Estimates oxygen saturation, typically using red and infrared light.

* Heart rate variability (HRV): Estimates variation in the time between heartbeats.

* Respiratory rate: Can be estimated from changes in the pulse waveform.

* Peripheral perfusion: Provides information about pulsatile blood flow in peripheral tissue.

Note: Not every PPG device supports all these measurements, and accuracy depends on sensor design, placement, motion, skin contact, and signal processing.

### 3\. Types of PPG sensors

![Using Smartwatches in Stress Management, Mental Health, and Well-Being: A Systematic Review](https://images.openai.com/static-rsc-4/mwyji_fLugjo6URUm1zPxjhGdaJ7lhRulIpNoL7U6yB7xLTcvdURJCjlvnpoXOQ-i_-Xu9ynq8V5qe4Z2EYNHeWo2SFL2IFOLcoZf5irFQx6XKEAoEqO7llcnCbSxKL6qFtrDzUdZL8nca0Wd7SGifFUUWIh6KcDFucF-4pEfEB6Wi7xNLHpDCKnF0SLjbzQ?purpose=fullsize)

Reflective PPG

The LED and photodetector are on the same side of the skin. Light is reflected or scattered back to the detector.

Applications: smartwatches, wristbands, and wearable devices.

![How to Design a Better Pulse Oximeter | Analog Devices](https://images.openai.com/static-rsc-4/OA1mDMSr-Uqau6_MSj7CN8_sY3Lg4MFE0LUZ6Zy4MvP151U4tNYgykxZw7hNto7aiD_ThRT5jx-CN5ASvoJLBDmRT44PBPmM9DItl6NcLcXS-0UwkDztW5cbyeIcWam8oGw5YCX9isDSr0VVcg5Y0CYKA7XE8EaZ0JhfXN5JY-W2VISiRn0VrHv1aZerlxEG?purpose=fullsize)

Transmissive PPG

Light passes through tissue, and a detector on the opposite side measures the transmitted light.

Applications: fingertip pulse oximeters and some ear sensors.

### 4\. Common PPG sensor modules

| Sensor/module | Key features                                                                    |
| ------------- | ------------------------------------------------------------------------------- |
| MAX30102      | Integrated red and infrared LEDs; heart-rate and SpO₂ applications              |
| MAX30105      | Optical sensing module often used for particle and relative signal measurements |
| MAX86141      | Optical AFE for wearable PPG applications; requires external optical components |
| MAX86150      | Integrated optical PPG and ECG sensing capabilities                             |

These modules differ in their optical components, electronics, and intended applications. Check the datasheet before choosing one.

### 5\. What does a PPG signal look like?

![Photoplethysmography Signal Processing and Synthesis | Peter Charlton](https://images.openai.com/static-rsc-4/jv8hByVp-sj1zl8AWScnOCo2KVohW8OMug2UeMoQjgXcM_kql6RCfMZn4ZTzqg6BLP_lbRkOPWkhnxJetHR4e9-jj7SJsgqEE58Jcjl8ibb5tfy4EMcVYhbYrF8bUEs_-u2ajfSDv0dLk4OB_vCbICD_bYsbwsG_gVaPNpoYxPqwIr9YN4JzMN_YL6o6bOSQ?purpose=fullsize)

A typical PPG waveform has a repeating pulse pattern. The time between successive pulses can be used to estimate heart rate.

For example, if the time between two successive pulse peaks is 0.8 seconds:

\\text{Heart Rate}=\\frac{60}{0.8}=75\\text{ BPM}

Real signals often contain noise from hand movement, ambient light, poor contact, and changes in circulation, so filtering and peak detection are important.

### 6\. Advantages and limitations

Advantages

* Non-invasive and generally comfortable.

* Relatively inexpensive and compact.

* Suitable for continuous monitoring.

* Uses light rather than electrical stimulation.

Limitations

* Motion can introduce substantial noise.

* Poor skin contact can reduce signal quality.

* Low peripheral blood flow may weaken the signal.

* Heart rate and SpO₂ estimates are not equally reliable in all conditions.

### 6\. Improve stability by averaging multiple beats

If you calculate BPM from just one interval, a single incorrectly detected peak can cause a large error.

Instead, calculate several valid inter-beat intervals:

HR_{\\text{avg}}=
\\frac{60}{\\operatorname{mean}(\\Delta t_1,\\ldots,\\Delta t_m)}

For example, suppose the measured intervals are 0.80, 0.82, 0.79, and 0.81 seconds.

The average interval is 0.805 seconds, giving:

HR_{\\text{avg}}=\\frac{60}{0.805}\\approx74.5\\text{ BPM}

You can also calculate the BPM for each interval and average those values. The results are not exactly identical, so choose one approach and use it consistently.

For a real-time monitor, a rolling window of recent valid intervals can make the display more stable while still allowing it to respond to changes in heart rate.

### 7\. Practical Python implementation

This example processes an array of PPG samples. It assumes that you have already collected the signal and that SciPy is installed.

```python
import numpy as np
from scipy.signal import butter, sosfiltfilt, find_peaks

# Replace this with your actual PPG samples.
# Example: a NumPy array containing raw IR readings.
ppg = np.loadtxt("ppg_samples.csv", delimiter=",")

fs = 100  # Sampling rate in Hz

# 1. Remove the DC baseline
ppg_centered = ppg - np.mean(ppg)

# 2. Band-pass filter: illustrative 0.5–5 Hz
sos = butter(
    2, [0.5, 5.0],
    btype="bandpass",
    fs=fs,
    output="sos"
)
filtered = sosfiltfilt(sos, ppg_centered)

# 3. Detect peaks
peaks, properties = find_peaks(
    filtered,
    distance=int(0.30 * fs),
    prominence=0.5 * np.std(filtered)
)

# 4. Calculate intervals and BPM
if len(peaks) >= 2:
    intervals = np.diff(peaks) / fs
    valid = (intervals >= 0.30) & (intervals <= 2.0)

    if np.any(valid):
        bpm = 60 / np.mean(intervals[valid])
        print(f"Estimated heart rate: {bpm:.1f} BPM")
    else:
        print("No valid pulse intervals")
else:
    print("Not enough peaks detected")
```

A few important details:

* The `0.5 * np.std(filtered)` prominence threshold is only an example. Real signals may need adaptive thresholds.

* `sosfiltfilt` filters offline in both directions. It is useful for recorded data analysis, but it cannot be used directly as a zero-latency, real-time filter.

* Real-time processing needs causal filtering and appropriate handling of filter delay.

* The file should contain one column of PPG samples, with the sampling rate known and samples in the correct chronological order.

### 8\. Common problems and how to troubleshoot them

| Problem                     | Likely cause                                                   | Possible solution                                      |
| --------------------------- | -------------------------------------------------------------- | ------------------------------------------------------ |
| BPM is twice the real value | Dicrotic features or noise counted as extra beats              | Improve peak prominence and minimum peak spacing       |
| BPM jumps suddenly          | Motion artifacts or missed peaks                               | Reject implausible intervals and check signal quality  |
| BPM stays at zero           | Poor contact, weak signal, or incorrect threshold              | Check sensor placement and inspect raw readings        |
| BPM is consistently wrong   | Incorrect sample rate or timing assumptions                    | Verify the sensor's configured sampling rate           |
| Signal looks flat           | Saturation, poor configuration, or insufficient optical signal | Check raw ADC values, LED settings, and sensor contact |

A PPG-derived heart rate is an estimate, not an ECG measurement. Motion, perfusion, and algorithm choices can affect accuracy.

For a hardware implementation, the MAX30102 uses I²C to deliver digital optical readings, so you can implement the processing on an ESP32, Arduino, or another microcontroller.

### What would be the best next step?

I recommend learning how to plot a real PPG signal and mark its detected peaks. That makes filtering errors and BPM calculations much easier to understand.

Short answer: Process the raw PPG signal, not just heart rate.

If you want to detect glucose changes or investigate other biomarkers:

* Heart rate (HR): Gives you only pulse rate, losing most of the information in the PPG waveform.

* Raw PPG waveform: Preserves pulse shape, amplitude, timing, and variability, which may contain useful features for research.

* Advanced features: Combine PPG features with HRV, multiple wavelengths, temperature, motion, and other sensor data where appropriate.

* Glucose detection: PPG-based glucose estimation is still experimental. PPG alone cannot reliably measure blood glucose or replace a glucose meter or CGM.

My recommendation: Collect raw PPG data, extract waveform features, and investigate whether they correlate with your target biomarker using validated reference measurements.

Remember: correlation does not prove that PPG can accurately detect a biomarker. Biomarker-specific validation is essential.

Yes, exactly! If your goal is to investigate glucose changes or discover other biomarkers, you should preserve and analyze the raw PPG waveform, rather than using only heart rate (HR).

A typical pipeline looks like this:

* Collect raw PPG data — ideally multiple wavelengths if your hardware supports them.

* Preprocess the signal — remove noise, motion artifacts, and baseline drift.

* Extract features, such as:

    * Time-domain: pulse amplitude, rise time, pulse width, inter-beat intervals.

    * Morphological: pulse shape, peak characteristics, waveform area.

    * Frequency-domain: spectral power and frequency-related features.

* Combine features with relevant additional sensor data if available.

* Train and validate a model against reference biomarker measurements.

Your model might use these features to investigate whether a biomarker can be estimated reliably.

Important: PPG features are not specific to glucose. They are also influenced by temperature, blood pressure, circulation, motion, and other factors. You need independently measured glucose values or other appropriate reference labels to establish whether your model genuinely predicts the biomarker.

Bottom line: Keep raw PPG → extract multiple features → validate against reference measurements. Treat HR as one additional feature, not your only input.
