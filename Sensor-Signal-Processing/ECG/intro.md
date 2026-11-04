### ECG signals: What they mean, what they look like, and how to measure them using wearable devices

An ECG (Electrocardiogram or EKG) is a measurement of the electrical activity of the heart.

Every time your heart beats, electrical signals travel through the heart muscle and coordinate its contraction. An ECG captures these electrical signals over time.

ECG is particularly interesting in wearable technology because it can help detect irregular heart rhythms, monitor cardiac health, and identify potential heart abnormalities.

Let's understand it step by step.

### 1\. What does an ECG signal mean?

An ECG signal represents the heart's electrical activity as a waveform.

The horizontal axis represents time, while the vertical axis represents electrical voltage (usually measured in millivolts, mV).

A typical ECG heartbeat has five characteristic components:

![HOW TO READ AN ECG - BIOMEDICAL VIEWS](https://images.openai.com/static-rsc-4/3jWmNcjVgukMJyzlu1ikSRuxJhZNJ8oII2LvSsjk1PjQwt_fZX65Hl_fsdPZKIS7mSDNmg2jxlN5iZNAbjquU1jZANkPOJnjBW4T_Ug20opEEYLm2e8T2PEwxZao_p-yrJSJBWoGnfG5UHAEK7wPcv18cO-IySNm4nTTp2Y3YxSiDxwBhSJhFRRRKxw9AOdr?purpose=fullsize)

| Component | Meaning                                                    |
| --------- | ---------------------------------------------------------- |
| P wave    | Electrical activation of the atria (upper heart chambers). |
| Q wave    | Initial downward movement of ventricular activation.       |
| R wave    | Large upward peak during ventricular activation.           |
| S wave    | Downward movement following the R peak.                    |
| T wave    | Electrical recovery of the ventricles.                     |

The most important feature for many wearable ECG applications is the R peak.

Why?

Because the time between consecutive R peaks tells us how frequently the heart beats.

For example:

* R peak 1 occurs at 0.5 seconds.

* R peak 2 occurs at 1.5 seconds.

* R peak 3 occurs at 2.4 seconds.

The intervals are:

* RR1 = 1.0 second

* RR2 = 0.9 seconds

Heart rate can be calculated using:

HR = \\frac{60}{RR\\ interval}

For an RR interval of 1 second:

HR = \\frac{60}{1}=60\\ BPM

### 2\. What does an ECG signal look like?

Here are three useful ways to understand ECG signals.

A. Normal sinus rhythm

![ECG Machine Overview for Biomedical Engineers: Principles, Components, and Clinical Applications - biomedevices.com](https://images.openai.com/static-rsc-4/PjS7y-25KiJPZNBXAmskn9RoNe3TmKkeN2PNSd2pFdVpFKUtjjXsTSd4kaMfsRLrl9fb7Ux2BVDOB4Z1arXChwviPEnLFNAxBTw1mQLi7xJkicsw_2hT7owPO_RqBAjWeeuMbZGMEC41-MHcvAbYtlC4wai0jJWh4f5mYAmuL4qFr7HkEo5I49uxnITLeleK?purpose=fullsize)

Regular heartbeats with consistent timing and recognizable P-QRS-T patterns.

B. Atrial fibrillation (AFib)

![Atrial Fibrillation (a-fib) ECG/EKG Nursing Review](https://images.openai.com/static-rsc-4/WLH5Tc7epAcF1GHM5OqGFJBIeYSBNjzF2A6CpE9XhwkoZltMwZddeXUltCtSHJ9rt4zh845MgLchESZ1nyeHpD7TQflOalK8PrQGWyuIpo_ggBwaSWCDx7LwmAcJ2O3fadaFhcBkXsuwRTOdCew_1ui_wBruj6pTQngE-7cpQYlYZY5zW2KS7CbXYHVnKe7V?purpose=fullsize)

Often shows irregularly spaced beats and no consistent P waves.

C. Tachycardia

![ECG Sinus Tachycardia - 8 Second Electrocardiogram Paper](https://images.openai.com/static-rsc-4/hjgqXWpKCze3zmBAPrWYN0_xuHg-HTIILwkLxzFdshsb39WPcbfXrPOhodOsx14rPpOExBsr_dlcHjLw5jQoSpgig6DcVEooQgiTfJU45FpQ08Kb8jElBe-zhXI9_FytKTEpRQpdlpaZn1qjM4-tjPw86ajX4Oii1FBnmHYNqjx4HylEUMMpDQxXtykj_tLA?purpose=fullsize)

A faster-than-normal heart rhythm, generally above 100 beats per minute in adults at rest.

The shape, timing, amplitude, and relationship between ECG waves can provide important information about heart function.

### 3\. What problems can ECG solve?

ECG is useful for identifying and monitoring several cardiac conditions.

| Problem                  | What ECG can help identify                                       |
| ------------------------ | ---------------------------------------------------------------- |
| Arrhythmia               | Abnormal heart rhythms                                           |
| Atrial fibrillation      | Irregular atrial rhythm                                          |
| Bradycardia              | Abnormally slow heart rate                                       |
| Tachycardia              | Abnormally fast heart rate                                       |
| Heart attack             | Electrical changes associated with myocardial ischemia or injury |
| Conduction abnormalities | Problems with electrical signal propagation                      |
| Long QT syndrome         | Abnormal ventricular electrical recovery                         |
| Heart monitoring         | Changes in cardiac electrical activity over time                 |

ECG can also help doctors evaluate symptoms such as:

* Palpitations

* Dizziness

* Fainting

* Chest discomfort

* Unexplained shortness of breath

Important: ECG is a diagnostic aid, not a universal detector of heart disease. A normal ECG does not rule out every cardiac problem. Some conditions require blood tests, imaging, or other investigations.

### 4\. How can we measure ECG using wearable devices?

There are two important technologies in wearable heart monitoring:

![Apple Scraps AI Health Coach Project Mulberry | Fitt Insider posted on the topic | LinkedIn](https://images.openai.com/static-rsc-4/nrwvzduLj82tAFQuQ7woPO7VuVMCIWljzDn3njZGFm02eJP-8iRR_k5YrTplvRAq6jP-vUSJble1gnS3FjnfyygyzE4qx4rdCdQyLOoNKYfof3xVltqmiWTa9QuR9dQeX9iCxJoor6AII5_357JKFq1c2X1WaXLZInUYTeUveH5LP0HK_dF1q7bOC87g1syc?purpose=fullsize)

A. ECG sensor (electrical measurement)

Measures the actual electrical signals generated by the heart using electrodes that contact the skin.

Actual ECG waveform

![Top Heart Rate and Cardiac Monitoring Devices](https://images.openai.com/static-rsc-4/olRGY11idiGkEkl8qMtBYpnkg57FQnPTEUG_7MqmoI36uOlaFvm6I0_wuhK0rWvs0lUoRcTYloJaX9GCsga5RkUG6d800FBR4leqJ8qIVuMwc4gWsVMgeub91x9pLmMyG3r7AzNzCzlnTc8It0jo7x3NW7Y3_kKRRPVQwZJYkrOabEGoZQSV8kYc8TE4iLh7?purpose=fullsize)

B. PPG sensor (optical measurement)

Uses LEDs and photodetectors to measure changes in blood volume under the skin.

Pulse waveform, not ECG

This distinction is extremely important.

| Feature               | ECG                   | PPG                            |
| --------------------- | --------------------- | ------------------------------ |
| Measures              | Electrical activity   | Blood volume changes           |
| Sensor                | Electrodes            | LED + photodetector            |
| Output                | ECG waveform          | Pulse waveform                 |
| Heart rate            | Yes                   | Yes                            |
| HRV                   | Yes                   | Can estimate                   |
| AFib detection        | Can support detection | Can screen for irregular pulse |
| Continuous monitoring | Device-dependent      | Common in smartwatches         |

A smartwatch reporting heart rate every second is not necessarily measuring ECG. Most smartwatches use PPG for routine heart-rate monitoring.

PPG-based irregular rhythm detection cannot independently establish an AFib diagnosis. PMC +2

### 5\. How does a wearable ECG sensor work?

Let's take an ECG-enabled smartwatch as an example.

![Angleterre : la MHRAA autorisera la fonction ECG de l'Apple Watch Series 4 à certaines conditions](https://images.openai.com/static-rsc-4/iYaphIflFx6grgOeWwruUpBM6-V9Dv64MosJ8FiywE49Pbq1-s-pEmDSTQWT2GG3TWq4Jb0fv8RwGExcMdX1m66EWf2BSeeO51jTaT_xVJ_DC_IPu2s5x_0ABuWI5aaz9X-cOKpMiwte1i0AvT_aTHAdbsnnIdztgKSaDOjHEp4Mxa6KvalYza4LAzM2Dmg6?purpose=fullsize)

A typical single-lead ECG smartwatch works like this:

* An electrode on the back of the watch touches your wrist.

* You place a finger from your opposite hand on the watch's metal electrode.

* Your body completes an electrical measurement circuit.

* The electrodes measure the voltage difference generated by cardiac electrical activity.

* An analog front-end circuit amplifies and filters the tiny signal.

* An ADC (Analog-to-Digital Converter) converts the analog signal into digital samples.

* Software processes the samples and displays the ECG waveform.

This produces a single-lead ECG, broadly comparable to Lead I of a conventional ECG. PMC +1

### The technical architecture

Heart electrical activity

Skin-contact ECG electrodes

Analog Front-End (AFE)

Amplification and analog filtering

ADC

Analog-to-digital conversion

Digital signal processing

Filtering, noise removal, R-peak detection

ECG waveform + cardiac metrics

### 6\. How do you calculate heart metrics from wearable ECG data?

Once you have digital ECG samples, you can extract useful information.

For example, imagine that your ECG device records a signal at 250 Hz.

That means:

250\\ samples/second

The time difference between samples is:

\\Delta t = \\frac{1}{250}=0.004s

You can then process the signal.

Step 1: Signal preprocessing

* Remove baseline wander.

* Remove 50/60 Hz electrical interference.

* Reduce muscle noise.

* Remove motion artifacts where possible.

Step 2: R-peak detection

Identify the highest peaks in each heartbeat.

![ECG R peak detection in Python: a comparison of libraries - Samuel Pröll - Homepage](https://images.openai.com/static-rsc-4/yi0RNdjqZnfnD5Y-VipEQHgZ_j_xTjHo8FnSJph5rPpPtIglt8UTVQaV98uXIjau62IJKc0Ozywl4VoOmjS3GhgnEwt_zQgXGsiBvV2fj7V4lbpYTj_wcNDX96wS9DP7qyRFUPu0J9KJJc4J5pHBWn9CN6vyrPOVAQoCb-andDNxpIKrHXaNJ4iUxGiXr5iR?purpose=fullsize)

Step 3: Calculate RR intervals

RR_i = \\frac{R_{i+1}-R_i}{f_s}

Where:

* = sample index of an R peak.

* = sampling frequency.

Step 4: Calculate heart rate

HR = \\frac{60}{mean(RR)}

Step 5: Calculate heart rate variability (HRV)

One common metric is RMSSD:

RMSSD =
\\sqrt{\\frac{1}{N-1}
\\sum_{i=1}^{N-1}(RR_{i+1}-RR_i)^2}

HRV describes variation in the time between consecutive heartbeats. It can provide information about autonomic regulation, but it is not a standalone diagnosis of health or disease.

### 7\. What data can you collect from wearable ECG?

Here are some useful features you can extract from ECG signals.

| Feature                | What it tells you                            | Application                       |
| ---------------------- | -------------------------------------------- | --------------------------------- |
| Heart rate             | Beats per minute                             | Fitness and cardiac monitoring    |
| RR interval            | Time between beats                           | Rhythm analysis                   |
| HRV / RMSSD            | Beat-to-beat variability                     | Autonomic activity monitoring     |
| QRS duration           | Ventricular activation duration              | Conduction abnormality assessment |
| QT interval            | Ventricular electrical activity and recovery | Long QT screening                 |
| P-wave characteristics | Atrial electrical activity                   | Rhythm analysis                   |
| Irregularity           | Variation in beat timing                     | Arrhythmia screening              |

Not all these measurements can be reliably extracted from every consumer smartwatch. In particular, measuring intervals such as QT and QRS accurately often requires higher-quality ECG recordings and clinical interpretation.

### 8\. What wearable devices can measure ECG?

Some examples of ECG-enabled devices:

![麻省理工科技评论-发现改变世界的新兴科技](https://images.openai.com/static-rsc-4/1T5cH4MOylNLQoQGnFGtI2kiQmZEA2J73Z0W-QSYSV_-09wcUJvDMzO_bDP8vWUg4zuHkDBdm_TzpCteTYTV6eKz2MpZZL9J7nF3aEe_YHErqsJKuWfUXcFUIJPfFtIv1Bif6TKx1VCDIZGKRAVVKh1i5UvFaZQt0R8c-aLA1i8Q9GVbQh2DA2aYPxHFLs-V?purpose=fullsize)

Apple Watch

Records single-lead ECG using wrist and finger electrodes.

Samsung Galaxy Watch

Supports ECG recording on compatible models and in supported regions.

![Портативный монитор пациента - KardiaMobile® - AliveCor - для ЭКГ / частоты сердечных сокращений / для обслуживания пациентов на дому](https://images.openai.com/static-rsc-4/SjO5QHpl3oFH3UVVS4vTg2Ug-WW9mbATjIwaWMnH9UGwhWwg3TIN4Y4KNDV8KF9Bw4jDepgfTMRmyAyh9ujyR3RMH6Dv--owz1HDq2jLK1NQ-UWaXGg2O1vW-NHyVk8mmK1s4vh1UP_n4QBtYlNaq9MV9SA2H8lV0ZY7ossj-2heJqpNYxclI3YoF93N5ULK?purpose=fullsize)

KardiaMobile

Portable ECG device that records heart electrical activity using finger electrodes.

![Langzeit-EKG / 3 Kanäle - Walk Free - Cardioline - kabellos](https://images.openai.com/static-rsc-4/pamyU8fcZ-rUrliIRhgJ7pmZ1Z8Mb1bckRKF60wnzijrxWNpTdEDN6xWD_fQ5ri6ROqrp8U_5LfwN1AKRgOC-xNY7djdIbn2G2CmJ9kaVZJBNUIf4fIHH-QPyWJgdBuAJnmgNOjG6VniPFk975cmdEiBKS4hzcMZ_ozqc2WDZj1f3HZ_Bg1ajf4uTQk7IbB4?purpose=fullsize)

ECG chest patches / Holter monitors

Useful for longer-duration cardiac rhythm monitoring.

### 9\. How can you build an ECG-based health monitoring system?

If you want to develop a wearable ECG monitoring solution, I would suggest this architecture:

Wearable hardware

* ECG electrodes

* ECG analog front-end (e.g. AD8232 or ADS1292R)

* Microcontroller (ESP32 or nRF52)

* Bluetooth Low Energy

Mobile application

* Receive ECG samples

* Display real-time ECG waveform

* Store historical recordings

* Show heart rate and HRV

Cloud / AI analytics

* ECG signal processing

* R-peak detection

* Arrhythmia classification

* Abnormal rhythm alerts

* Long-term trend analysis

Final output

Cardiac health monitoring dashboard

A few technical considerations:

* ECG sampling frequency: 250–500 Hz is a reasonable starting range for many basic rhythm-monitoring projects.

* Use an ECG-specific analog front end, not just an ordinary microcontroller ADC.

* Ensure appropriate input protection, electrical safety, and signal isolation.

* Motion artifacts and poor electrode contact must be handled.

* Validate signal quality and algorithms against reference ECG recordings and expert-reviewed annotations.

An important distinction: an AD8232-based prototype can collect ECG signals, but it does not automatically become a medically validated diagnostic device.

### 10\. What is the difference between ECG and wearable heart-rate monitoring?

This is probably the most important concept to remember:

![PHYSIOLOGY - Clinical Tree](https://images.openai.com/static-rsc-4/H9wsqa4tWbc0FbXxrTs5qNbJhIJnuGc7-Vnlq2n8lVxGD8pUONgj4vt7lCEcwDVF1lOAwHOMtmwlPCmFTX7GZQODe11TkUtLT-J8cDOYkKxf3DHV5AiJpZ1FSsZouaCQDps1NFAZGFjwNhZ4mVr9LYwSclLR6AnqK8Mqkf-bX2T9ECxSm6317PiFo6dcGBpR?purpose=fullsize)

ECG

Measures electrical activity of the heart.

![An Overview of the Sensors for Heart Rate Monitoring Used in Extramural Applications | MDPI](https://images.openai.com/static-rsc-4/Z7LWuHZo-bTrCk78g-GpA15wa4LvmribTy2h5in7BvVCwrGS7cb5n7OPxvK3sepZNoiREuFC_nwMKWUSexgA4O4WQQ53VpTc89t73niefjtm7gODcyoAhoq6tCaWdW7yo9CZaiAZJA2vsvIQuu6Cbf6JozcnFZVtL1y3mCMjzOlVDDqCX__q4gFA0sO1uSkk?purpose=fullsize)

PPG

Measures optical changes in blood volume.

ECG can provide information about electrical rhythm and conduction. PPG provides information about the peripheral pulse. They are complementary technologies, not interchangeable ones.

For clinical use, wearable recordings should be reviewed appropriately. Automated interpretations can make mistakes, and a smartwatch ECG cannot replace a standard 12-lead ECG. PMC +2

### 11\. What would be an interesting ECG research or development project?

Here are five possible projects:

* Real-time ECG monitoring: Capture ECG from a wearable and display the waveform on a mobile app.

* AI-based arrhythmia detection: Classify normal rhythm, atrial fibrillation, and other rhythm abnormalities using ECG datasets.

* ECG + PPG fusion: Combine electrical and optical signals to improve heart monitoring.

* ECG-based HRV analysis: Analyze stress-related and autonomic patterns.

* Continuous cardiac monitoring: Develop a wearable system that detects suspicious rhythm episodes and records them for clinical review.

### A question to help me guide you further

What is your main objective?

1\. What do you want to achieve?

Build a wearable ECG monitoring device

Analyze existing ECG signals

Detect heart diseases using AI

Understand ECG and PPG wearable data

2\. What kind of data do you have?

Smartwatch / wearable sensor data

Raw ECG signals (CSV)

PPG signals

No data yet

3\. What is your technical focus?

Research / AI / machine learning

Hardware / embedded systems

Signal processing / Python

Healthcare application development

Submit

Based on your answers, I can help develop a complete technical pipeline, from wearable sensor acquisition to ECG signal processing and AI-based cardiac monitoring.
