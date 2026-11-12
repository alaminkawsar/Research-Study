# Part-1 (PPG Generation - Camera)
pulse-synchronous PPG-like waveform using only a camera and reflected light, without attaching a physical PPG sensor to the body.

This technique is called remote photoplethysmography (rPPG), also known as camera-based PPG or imaging photoplethysmography (iPPG).

There is an important distinction, however:

* Contact PPG: A physical LED illuminates the skin, and a photodetector measures changes in transmitted or reflected light caused by changes in blood volume.

* Camera-based PPG (rPPG): A camera records subtle changes in skin color caused by variations in blood volume in superficial blood vessels. An algorithm extracts those changes and reconstructs a pulse waveform.

The camera does not directly measure blood volume. It measures optical intensity/color changes that are physiologically related to blood volume.

![A Programmable Gain Calibration Method to Mitigate Skin Tone Bias in PPG Sensors](https://images.openai.com/static-rsc-4/TkISXeRDOT70uv1Ogy60sk5hSbEo5rxdz-4mDtKCjuO6gist71m4N2jWp17_h881mA19P0Rn9jjaDTNqkEJiUEdtfnmtf8PolxJpfWJRdzfQcdgT48WVMr1aLnRqHXRFM5bsoabWKIK1KsmbKGHzCsabBBrbY9hzfaKxDNeEUOwAUruBuRCy-8I68wxvL9vB?purpose=fullsize)

![Optimal signal quality index for remote photoplethysmogram sensing | npj Biosensing](https://images.openai.com/static-rsc-4/wudfauoVDt-UVMan4KqSNbGxpVAI5ucQtEmxF7iu6dhJYBqj54nTE8x6uHnV-pFDEIJY4N9eVseZx--uPS4s7FW5WMrcqR3Ae2P3Vrr6T59bwGPM5lyRc0XRVXvhAwyb4FcJkHKzAuW_-rzwRmgnsv7jv7K56i6B5vdcYqtBX2ObJc_Ox9PWmtcxDhwtBiGm?purpose=fullsize)

![Sensors for Emotion Recognition | Encyclopedia MDPI](https://images.openai.com/static-rsc-4/uFY9HNW1HZcnjJIjaMZw8eE2FqRpMyrbUpIspUijC0FUsND-bIx1p3j5GN0SPCrEpoBioJl6_Mw_jmdgt35CnqmKhcVnTSW-Axw6MOV78NQJRdx68KQcUa_bOd8LYCnsgMakQfr93p9xH0kqHGWI69_9CO0Vc2ykMVEJRLTwa-TzHk3UUW6xCG8L67rlAG5Z?purpose=fullsize)

![Assessment of Deep Learning-based Heart Rate Estimation using Remote Photoplethysmography under Different Illuminations](https://images.openai.com/static-rsc-4/__NSyTYCCN_QGhwnRuHNX6mfnCQFvZ4liY17x924tU1nV2hfEICuQaPNw3mlGstR9QTyHIBy3i7aZa_aYFcQS8fI5ph0yfyqEHWdAdsizU5MeMct5tXLrDhPL2CmJZ6hc9t4ejIgOfYCamT_CnBbZlagd8DRy-3Rhg3hXaJ8YC-1FwuYvQcf4ikQB7P-W0iB?purpose=fullsize)

![综述：可穿戴PPG传感器中先进材料的制备、性能及应用-电子工程专辑](https://images.openai.com/static-rsc-4/aME0ep0vsywFG4NY76NvX0EzXwyOjwY4N87g-M7MQ5AfGupnzuW_KrUjKBBtLLKPwlDAhjxQSXoE6dfMdhcmA1-IhcXkBlFK-aj6GCUYCga0x_U0HWnWqDzMxb6Xd4cjxACC9BWV3zSJqgUM0V_HrtpCw_nsaVXAvu_JVdmysSttvjNMNlL5KNCZhYNquznQ?purpose=fullsize)

![Firefly algorithm and DNN for improved contactless heart rate measurement from videos | Scientific Reports](https://images.openai.com/static-rsc-4/zwcK7dHjsiPxxl-oNdEhKxguSIq4DXiniIJYZs5RKBpMMzPeOJmwGc9Q2aQvVioWXDdO_Td-05Oby18RSJeoGnoXjPzkJG-8LG_YmLTuq1uqrW8kEFP1Psqfd0TBy1zKELRujQL6ZI1VlP5S-mWSGLbHNItx-PlCS7HKInIcgRYGwFQ-8PPVp_u_6LieU8pn?purpose=fullsize)

![Blood Pressure Measurement: From Cuff-Based to Contactless Monitoring](https://images.openai.com/static-rsc-4/KeyW17YcKe-3a9Y8ClCbvaUCBGMetbA_zJn7_5wBbuIwmxH2dw0qnAVQeIZSfLgECqZpgo_SKtfwlCiUUiiKQY6qRH9Y5hInNCM8tEKvHXIP4xURIMmiDyJSFPJH4h2TCvr8qR0ztP0Ifm0TWAjiXMQTXbgRXEcgt2FDU8B0GgCHxGlRO92k4kykyullKG2O?purpose=fullsize)

![Evaluation of Remote Photoplethysmography Measurement Conditions toward Telemedicine Applications](https://images.openai.com/static-rsc-4/pbfAI90RdroS2_5AXI7qjNJue59zqIXcAmLoH2jG3CfJigjDmUBk8nTeIrNQDO4CWXitB-rp_8tDGwcUAdr5cCAJ53s2dsnmEF9vylOwXFGIyf9-eLbNcrL3rbu1tfBoo_ggVcfUUU-2I_rVwfez4jyNmSrL-VDro7E3BBV6XhKXy-7WSu74yKbom5okRps9?purpose=fullsize)

![Josef Čada: Chytrý prstýnek](https://images.openai.com/static-rsc-4/Oq_Rtn8d1b0bfMQFpLy3GUIvc8zC2eZH8AMTRcLWJPIo61lUoV7PvjNHOUfgx4Mv-7XsJQRxb3hNw8TvIC0Fj6xpnfmrpgW5ZjtZ0Q72rD8bicCosUBRaIViuPizFfoip4zIwfzjUmtO1432guo7JjgXtM0yBhMDLQr1pspiDpXXJVqusY_HDfcrKSYMQYCw?purpose=fullsize)

The short answer is that rPPG can produce waveforms that correlate strongly with conventional contact PPG. However, waveform morphology, amplitude, signal quality, and timing agreement are not necessarily identical.

### 1\. Research papers that directly compare camera PPG with contact PPG

I found several particularly relevant studies. Some compare the actual waveforms, not merely the estimated heart rates. These are the most useful papers for your question.

### Paper 1 — Direct comparison of RGB camera signals against contact PPG (2023)

Title: Evaluating RGB channels in remote photoplethysmography: a comparative study with contact-based PPG

* Authors: Rodrigo Castellano Ontiveros et al.

* Journal: Frontiers in Physiology

* Year: 2023

* DOI: `10.3389/fphys.2023.1296277`

[Read the full research paper](https://www.frontiersin.org/journals/physiology/articles/10.3389/fphys.2023.1296277/full?utm_source=chatgpt.com) · [PubMed record](https://pubmed.ncbi.nlm.nih.gov/38187134/?utm_source=chatgpt.com)

What they did:

They extracted rPPG signals from video using individual RGB channels and compared them with conventional contact PPG.

They used:

* Pearson correlation coefficient.

* Dynamic Time Warping (DTW).

* Root Mean Square Error (RMSE).

* Heart-rate difference in BPM.

They evaluated three datasets:

| Dataset  | Participants | Activities                           |
| -------- | ------------ | ------------------------------------ |
| LGI-PPGI | 6            | Resting, talking, exercise, rotation |
| PURE     | 10           | Resting and different head movements |
| MR-NIRP  | 8            | Still and motion                     |

Important findings:

* The green channel performed better than the red and blue channels.

* Green-channel extraction produced the closest overall correspondence with contact PPG among the three individual RGB channels.

* Performance changed considerably depending on subject activity and recording conditions.

For example, their average absolute heart-rate differences were:

| Dataset  | Green channel |
| -------- | ------------- |
| LGI-PPGI | 18.73 BPM     |
| PURE     | 7.17 BPM      |
| Combined | 10.31 BPM     |

These numbers are important: a camera signal may contain a recognizable pulse waveform but still produce unreliable heart-rate estimates under certain conditions.

The authors also compare the signals directly in the time domain, which makes this paper especially relevant to your question. Frontiers +2

### Paper 2 — Reconstructing the actual contact PPG waveform from camera PPG (2021)

Extremely relevant to your objective

Title: Restoration of Remote PPG Signal through Correspondence with Contact Sensor Signal

* Authors: So-Eui Kim et al.

* Journal: Sensors

* Year: 2021

* DOI: `10.3390/s21175910`

[Read on PubMed](https://pubmed.ncbi.nlm.nih.gov/34502807/?utm_source=chatgpt.com) · [Read full paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC8434340/?utm_source=chatgpt.com)

This paper addresses a particularly interesting problem.

The authors explain that the raw remote PPG signal generally has:

* A weaker pulsatile component.

* Less clearly defined waveform morphology.

* More noise compared with contact PPG.

Their objective was to reconstruct a signal resembling the conventional contact PPG.

They investigated three approaches:

* Support Vector Regression (SVR).

* A three-layer deep-learning model.

* A combination of SVR and deep learning.

Reported results

| Metric              | Before restoration | After restoration |
| ------------------- | ------------------ | ----------------- |
| Cosine similarity   | 0.921              | Up to 0.977       |
| Pearson correlation | 0.778              | Up to 0.939       |

This is particularly interesting if your objective is not just estimating heart rate but producing a camera-derived waveform that resembles a conventional PPG waveform.

Important qualification: Their restoration models use correspondence with contact-sensor signals during training. Therefore, the results do not mean that a camera can reproduce the contact sensor's waveform perfectly without calibration or reference data.

PubMed +1

### Paper 3 — Contactless cardiovascular assessment versus wearable PPG (2023)

Title: Contactless Cardiovascular Assessment by Imaging Photoplethysmography: A Comparison with Wearable Monitoring

* Journal: Sensors

* Year: 2023

* DOI: `10.3390/s23031505`

[Read the full paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC9919512/?utm_source=chatgpt.com)

This study is especially useful because it investigates more than heart rate.

The researchers compared eight image-based PPG extraction techniques:

* GRD

* AGRD

* PCA

* ICA

* LE

* SPE

* CHROM

* POS

They used the UBFC-rPPG dataset, containing 42 participants, with:

* Camera video recorded at 30 FPS.

* Finger-clip PPG as the reference signal.

They evaluated pulse rate and pulse-rate variability (PRV).

Key finding: POS and CHROM performed particularly well for pulse-rate estimation and several PRV measurements.

For example, the POS method achieved:

| Parameter               | Mean difference    |
| ----------------------- | ------------------ |
| Pulse rate              | -0.186 BPM         |
| 95% limits of agreement | -4.05 to +3.68 BPM |

However, agreement for individual PRV parameters was less consistent. This is a critical distinction if you intend to analyze the detailed waveform rather than simply calculate BPM.

PMC +2

### Paper 4 — Recovering systolic and diastolic peaks using an ordinary camera (2014)

Important waveform evidence

Title: Remote Detection of Photoplethysmographic Systolic and Diastolic Peaks Using a Digital Camera

* Authors: Daniel McDuff, S. Gontarek, Rosalind W. Picard.

* Year: 2014.

* MIT Media Lab.

[Read the publication](https://www.media.mit.edu/publications/remote-detection-of-photoplethysmographic-systolic-and-diastolic-peaks-using-a-digital-camera/?utm_source=chatgpt.com)

This paper is particularly interesting because it goes beyond heart-rate estimation.

The researchers used:

* An ordinary digital camera.

* Ambient light.

* Facial video recorded from as far as 3 metres.

* A conventional fingertip contact PPG sensor as reference.

They investigated whether the camera could recover systolic and diastolic peak/inflection timing.

Reported results

### 0.94

Correlation of systolic–diastolic peak intervals

### 26 ms

Absolute error in inter-beat intervals

### 12 ms

Absolute error in mean systolic–diastolic peak timing

### 30 FPS

Camera frame rate

This demonstrates that camera-based PPG can preserve useful pulse morphology information, not just heart-rate frequency.

MIT Media Lab +1

### Paper 5 — FusionPPG: Recovering a more accurate blood-pulse waveform (2016)

Title: Spectral-spatial fusion model for robust blood pulse waveform extraction in photoplethysmographic imaging

* Year: 2016

* PMID: 28018712

[Read full paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC5175538/?utm_source=chatgpt.com)

This paper proposes FusionPPG, which combines spatial and spectral information to identify pulsatile pixels and extract a more accurate blood-pulse waveform.

Its evaluation included 24 participants.

The researchers reported:

* Better waveform matching than FaceMeanPPG and DistancePPG.

* Statistically significant improvements (p less than 0.001).

* Heart-rate correlation with ground truth of .

This is a useful paper if you want to develop your own signal-extraction algorithm rather than simply use average RGB values.

PMC +1

### Paper 6 — Machine learning-based construction of remote PPG signals (2024)

Title: A machine learning-based approach for constructing remote photoplethysmogram signals from video cameras

* Year: 2024

* Journal: Communications Medicine

* DOI: `10.1038/s43856-024-00519-6`

[Read the full paper](https://www.nature.com/articles/s43856-024-00519-6?utm_source=chatgpt.com) · [Read on PubMed Central](https://pmc.ncbi.nlm.nih.gov/articles/PMC11161609?utm_source=chatgpt.com)

This is another strong match for your objective.

The authors developed a machine-learning approach to construct an rPPG signal resembling the fingertip contact PPG.

They:

* Trained using the PURE dataset.

* Tested on PURE, LGI-PPGI, and MR-NIRP.

* Compared against conventional methods such as POS, LGI, and CHROM.

* Evaluated using correlation, DTW, and heart-rate differences.

An important contribution is that the method was evaluated on datasets that were not used during training.

This paper is worth investigating if you eventually want to train a model that converts camera-derived signals into contact-PPG-like waveforms.

PMC +2

### 2\. What do these papers collectively tell us?

Here is how I would interpret the research:

| Research objective                      | Is camera PPG feasible?        | Evidence                                 |
| --------------------------------------- | ------------------------------ | ---------------------------------------- |
| Detect heartbeat                        | Yes                            | Multiple studies                         |
| Generate a continuous pulse waveform    | Yes                            | FusionPPG, 2016                          |
| Match contact PPG waveform              | Yes, with limitations          | Kim et al., 2021                         |
| Estimate systolic/diastolic peak timing | Yes                            | McDuff et al., 2014                      |
| Estimate pulse-rate variability         | Possible, but more challenging | van Es et al., 2023                      |
| Reconstruct contact-like PPG using ML   | Yes, experimentally            | Kim et al., 2021; Ontiveros et al., 2024 |

The most important distinction is:

A high correlation in heart rate does not necessarily mean that the two PPG waveforms are identical.

For example, two signals can have almost identical peak frequencies but different:

* Systolic peak amplitudes.

* Diastolic wave characteristics.

* Dicrotic notch positions.

* Pulse morphology.

* Baseline fluctuations.

* Pulse arrival times.

Therefore, if your goal is to generate actual PPG waveforms, waveform-level validation is essential.

### 3\. How would you generate PPG using only a camera and reflected light?

The basic architecture is:

### Camera-based PPG acquisition pipeline

![Dr. Lai-Man PO, Associate Professor, Department of Electronic Engineering, City University of Hong Kong](https://images.openai.com/static-rsc-4/GBHyMu0F8xuA-8-oezBLx3w-MMQFRROay0fEQpD8Lts4XBMuR6ah9ujbm_dxT-81LBI_4pEoJgX2SZ1quY-mL7nJ4Svy9njjxwS3thZE3jEqGJbyGgXZQRbZ1erx--2KZt8vg7q8MKKuQaOcbi_qTBZAzpNKxcbQhKnxEY5LAx3-hqXP755AK2Dm3EnEI5jG?purpose=fullsize)

1\. Optical illumination

Ambient light or controlled LED illumination reflects from facial skin.

2\. Camera acquisition

Record facial video, ideally at 30–60 FPS or higher.

3\. Region of Interest (ROI)

Extract forehead and cheek skin pixels while excluding eyes, hair and background.

4\. RGB signal extraction

Calculate average red, green and blue intensity for each video frame.

5\. Signal processing

Detrending, filtering, chrominance separation and motion-artifact removal.

6\. Reconstructed rPPG waveform

Continuous pulse waveform that can be compared with conventional contact PPG.

### Which signal-extraction algorithms should you investigate?

I would start with these five:

| Algorithm | Purpose                                       |
| --------- | --------------------------------------------- |
| GREEN     | Extract green-channel intensity variation     |
| ICA       | Separate independent physiological components |
| CHROM     | Separate chrominance-based pulse information  |
| POS       | Plane-Orthogonal-to-Skin method               |
| LGI       | Local Group Invariance method                 |

My recommendation is to implement GREEN, CHROM and POS first.

GREEN provides a simple baseline. CHROM and POS are more sophisticated approaches for suppressing illumination and motion-related noise.

### What about the light source?

You have two possibilities:

Option A: Ambient light

* No additional illumination hardware.

* Camera captures naturally reflected light.

* This is genuinely non-contact and has been demonstrated in the McDuff et al. study.

Option B: Controlled LED illumination

* Use a stable LED light source.

* Illuminate the forehead or cheek.

* Capture the reflected light using the camera.

* Reduce changes caused by ambient lighting.

Controlled illumination could be particularly useful for a laboratory experiment because it makes the acquisition conditions more repeatable.

A critical point: ordinary visible-light RGB cameras are suitable for pulse waveform extraction, but you should not assume that they can produce clinically reliable SpO₂ measurements. SpO₂ requires additional optical and calibration considerations.

### 4\. How can you experimentally prove that camera PPG matches actual PPG?

I would recommend a simultaneous acquisition experiment.

![SympCam: Remote Optical Measurement of Sympathetic Arousal · Sensing, Perception & Interaction Lab](https://images.openai.com/static-rsc-4/w3d1Rx0cS7lEPLI64cZJam-5QOq5dxH1-THD-IJvyI1t4dlUryMECKkI8T538gh4ddkv74SPrTvjWWQGPnpOTrdw50R2O_5GHhnDMiIm7wMASC_DmxbZJsiS3o2GD-EHs0FjSR5ZV4l6Ws8A6-SLlbQYPPs97fcEavRuL5k9YirD0mI3rf_AJ6aSVGpCRVP2?purpose=fullsize)

Experimental setup:

Use the following equipment:

* RGB camera (30–60 FPS minimum).

* Stable LED illumination.

* Finger-contact PPG sensor or pulse oximeter that provides raw PPG data.

* Computer for recording and processing.

* Software for synchronization.

Record both signals simultaneously:

* Camera → facial rPPG.

* Finger sensor → reference contact PPG.

Make sure both recordings have synchronized timestamps.

### Metrics you should calculate

I would divide your validation into three categories.

A. Waveform similarity

| Metric              | What it measures                       |
| ------------------- | -------------------------------------- |
| Pearson correlation | Linear waveform similarity             |
| RMSE                | Difference between signal amplitudes   |
| DTW                 | Similarity despite temporal variations |
| Cosine similarity   | Overall waveform direction similarity  |
| SNR                 | Quality of the extracted pulse signal  |

B. Peak detection and timing

| Metric                      | What it measures                                 |
| --------------------------- | ------------------------------------------------ |
| Peak detection accuracy     | Whether both signals detect the same beats       |
| Inter-beat interval error   | Difference between successive beat intervals     |
| Systolic peak timing error  | Difference in systolic peak location             |
| Dicrotic notch timing error | Difference in notch location, where identifiable |

C. Physiological parameters

* Heart rate.

* Pulse rate variability.

* SDNN.

* RMSSD.

* Pulse morphology.

Use Bland–Altman analysis for agreement, rather than relying only on Pearson correlation.

One important consideration: a finger PPG and facial rPPG measure pulse waves at different anatomical locations. Therefore, you should account for pulse propagation delay and synchronization before comparing their waveform shapes. Also, rPPG amplitude is generally arbitrary and affected by camera exposure, skin reflectance and illumination. Normalize amplitude or compare morphology separately when appropriate.

### 5\. Public datasets you can use

You do not necessarily need to collect your own data initially.

| Dataset   | Why it is useful                                   |
| --------- | -------------------------------------------------- |
| PURE      | Synchronized facial video and contact PPG          |
| LGI-PPGI  | Multiple activities and synchronized reference PPG |
| MR-NIRP   | Visible/NIR remote PPG research                    |
| UBFC-rPPG | Facial video with reference physiological signals  |

These datasets are especially useful because they provide camera video and reference physiological measurements.

### 6\. My recommendation for your research direction

I would formulate the research problem as:

"Reconstruction and Morphological Validation of Contact Photoplethysmographic Signals Using Camera-Based Remote Photoplethysmography."

The research objective would be to establish whether a conventional RGB camera can reconstruct a contact-PPG-like waveform using only reflected light.

I would investigate three research stages:

* Stage 1: Raw rPPG extraction

    Extract facial PPG signals using GREEN, CHROM and POS algorithms. Compare the results against simultaneously recorded contact PPG.

* Stage 2: Waveform reconstruction

    Investigate signal-processing and machine-learning approaches to improve waveform morphology and recover systolic peaks, diastolic features and the dicrotic notch.

* Stage 3: Physiological validation

    Evaluate whether the reconstructed signal can reliably support HR, PRV and waveform morphology analysis.

### Five papers I would prioritize reading

In order of relevance to your proposed research:

* Kim et al. (2021) — Restoration of Remote PPG Signal through Correspondence with Contact Sensor Signal.

* Ontiveros et al. (2024) — A machine learning-based approach for constructing remote photoplethysmogram signals from video cameras.

* McDuff et al. (2014) — Remote Detection of Photoplethysmographic Systolic and Diastolic Peaks Using a Digital Camera.

* van Es et al. (2023) — Contactless Cardiovascular Assessment by Imaging Photoplethysmography.

* FusionPPG (2016) — Spectral-spatial fusion model for robust blood pulse waveform extraction in photoplethysmographic imaging.

These papers cover signal extraction, waveform reconstruction, morphology and comparison with contact PPG.

### 7\. One important question about your intended research

There are two substantially different research objectives here:

What exactly do you want to achieve?

A. Generate an actual PPG waveformCamera output should resemble the contact sensor waveform, including systolic peaks, diastolic features and dicrotic notch.

B. Extract heart rate and HRVOnly accurate beat detection, heart rate and inter-beat intervals are required.

C. Reconstruct contact PPG using deep learningTrain a model to convert camera-derived signals into contact-PPG-like signals.

D. Prove whether camera PPG and contact PPG are equivalentConduct a rigorous experimental comparison and statistical validation.

Which camera are you planning to use?

Ordinary RGB camera / webcam / smartphone

NIR camera

High-speed camera

Not decided yet

Submit research direction

The distinction matters because generating a pulse waveform, reconstructing a contact-like PPG waveform, and proving waveform equivalence are three different scientific problems. I can help develop the corresponding methodology and experimental protocol.

# Part-2
### Research methodology: RGB camera-based reconstruction of contact PPG waveforms

Your research should focus on a more ambitious objective than ordinary remote heart-rate monitoring:

Can an ordinary RGB camera capture reflected light from human skin and reconstruct a continuous PPG waveform that preserves the morphological characteristics of a conventional contact-based PPG sensor?

I recommend approaching this as a waveform reconstruction and physiological signal validation study, rather than simply an rPPG heart-rate estimation project.

The distinction is important. Your desired output is not just a heart-rate number. It is a time-series signal that resembles the conventional PPG waveform, including:

* Systolic upstroke.

* Systolic peak.

* Systolic decline.

* Dicrotic notch, when visible.

* Diastolic wave.

* Beat-to-beat interval variation.

![An Overview of the Sensors for Heart Rate Monitoring Used in Extramural Applications | MDPI](https://images.openai.com/static-rsc-4/Z7LWuHZo-bTrCk78g-GpA15wa4LvmribTy2h5in7BvVCwrGS7cb5n7OPxvK3sepZNoiREuFC_nwMKWUSexgA4O4WQQ53VpTc89t73niefjtm7gODcyoAhoq6tCaWdW7yo9CZaiAZJA2vsvIQuu6Cbf6JozcnFZVtL1y3mCMjzOlVDDqCX__q4gFA0sO1uSkk?purpose=fullsize)

I would structure the research around five main contributions:

* Develop an RGB-camera-based PPG acquisition system.

* Extract raw pulsatile information from reflected light.

* Develop an algorithm to reconstruct contact-PPG-like morphology.

* Validate reconstructed waveforms against simultaneous contact PPG.

* Determine the physiological conditions under which camera-based reconstruction is reliable.

### Part I — Literature review

### 1\. Understanding the research gap

Conventional PPG measures changes in optical absorption and scattering associated with changes in blood volume in peripheral tissue.

Remote PPG uses the same underlying physiological phenomenon, but the optical measurement is performed using a camera rather than a skin-contact photodetector.

The research challenge is that camera-derived signals have additional sources of variation:

| Challenge                        | Effect on waveform                              |
| -------------------------------- | ----------------------------------------------- |
| Motion                           | Creates artificial intensity changes            |
| Illumination variation           | Changes the baseline and pulse amplitude        |
| Camera auto-exposure             | Alters intensity independently of physiology    |
| Skin reflectance                 | Changes the optical response                    |
| Compression and video processing | Can distort subtle color changes                |
| Low frame rate                   | Limits temporal resolution                      |
| Spatial averaging                | Can suppress or distort local pulse information |

The central research gap is therefore not whether a camera can detect a pulse. It is whether the camera can preserve the morphology of the underlying pulse waveform sufficiently well to approximate a contact PPG signal.

### 2\. Literature review matrix

These are the papers I would use as the foundation of your literature review.

| Paper                        | Contribution                                             | Relevance to your research                      |
| ---------------------------- | -------------------------------------------------------- | ----------------------------------------------- |
| McDuff et al., 2014          | Remote recovery of systolic and diastolic peak timing    | Direct evidence of waveform morphology recovery |
| Kim et al., 2021             | Restores rPPG using contact-PPG correspondence           | Strong foundation for reconstruction            |
| Ontiveros et al., 2023       | Compares RGB channels against contact PPG                | Establishes channel-level baseline              |
| Lee et al., 2023/2024        | Reviews remote PPG signal processing and limitations     | Supports methodology and research gap           |
| PPG Integrative Review, 2022 | Reviews waveform morphology, noise and signal processing | Supports validation metrics                     |

### Important observations from the literature

McDuff et al. (2014) is particularly important for you. They demonstrated that facial video recorded at only 30 Hz could recover useful systolic–diastolic timing information. Their reported correlation for mean systolic–diastolic peak-to-peak time was 0.94, and the absolute error in that timing was 12 ms. They also found that alternative orange, green and cyan channels could outperform conventional RGB combinations. PubMed +2

Kim et al. (2021) is probably the closest methodological predecessor to your intended project. They explicitly investigated the restoration of blurred remote PPG waveforms using contact PPG correspondence. Their reported Pearson correlation increased from 0.778 before restoration to 0.939 after restoration using their combined model. PMC +1

Ontiveros et al. (2023) provides a useful warning: the green channel performed better than red and blue in their experiments, but performance depended on the recording conditions and participant activity. PMC +1

My interpretation: You should not simply propose another algorithm for estimating heart rate. Your novelty should be the systematic reconstruction and morphological validation of RGB-derived waveforms against a contact reference.

There is also a very recent 2026 systematic review covering 38 rPPG studies. It identifies motion, illumination, camera characteristics and population variability as important unresolved problems. This can help you position your research in the current literature. ScienceDirect

### 3\. Proposed research questions

I suggest using these four research questions.

| ID  | Research question                                                                                                             |
| --- | ----------------------------------------------------------------------------------------------------------------------------- |
| RQ1 | Can RGB video produce a continuous rPPG waveform that preserves the temporal structure of contact PPG?                        |
| RQ2 | Which RGB signal extraction method produces the highest waveform similarity?                                                  |
| RQ3 | Can signal processing improve the visibility and detection of systolic peaks, dicrotic notches and diastolic features?        |
| RQ4 | Can supervised waveform reconstruction improve morphological agreement without introducing artificial physiological features? |

### Research hypotheses

* H1: RGB-derived rPPG contains sufficient pulsatile information to recover the principal systolic waveform structure.

* H2: CHROM and POS will outperform simple green-channel averaging under at least some illumination and motion conditions.

* H3: Waveform reconstruction will improve agreement with contact PPG compared with raw rPPG extraction.

* H4: Performance will decrease with motion, illumination variation and reduced video frame rate.

These are hypotheses to test, not assumed results.

### Part II — Proposed system architecture

### 4\. Overall research system

I recommend developing the system in two parallel branches: a signal-processing branch and a machine-learning reconstruction branch.

### Proposed RGB-to-PPG architecture

RGB camera + reflected light

Facial video acquisition at 30–60 FPS

Face detection and ROI tracking

Forehead and left/right cheek regions

RGB temporal signal extraction

Green, CHROM, POS, ICA

Branch A

Conventional signal processing

Filtering → detrending → artifact removal

Branch B

Waveform reconstruction

Regression / temporal CNN / U-Net

Reconstructed camera-based PPG

Continuous waveform with extracted morphological features

Contact PPG validation

Waveform alignment, morphology, timing, correlation and error analysis

The contact sensor is used as the experimental reference and training target. It is not an input to the final camera-only inference pipeline.

This distinction should be explicit in your thesis.

### Part III — Experimental methodology

### 5\. Hardware and acquisition setup

Your first experimental system should be deliberately simple. Avoid adding unnecessary sensors or expensive cameras until you establish that the RGB signal contains recoverable waveform morphology.

### 5.1 Recommended equipment

![Webcam Logitech BRIO 4K Ultra HD USB](https://images.openai.com/static-rsc-4/TyyYbOKnSWh2xpcm6U8FmyD4FtpagfFxgdnpDaY-zyYpz6ieZjK-RkKxf9UWW1jdPoN7zC5O0-eafZTV1iRjb9YjFFmkJOJpixwGfLbj8uiGWGqwTs-qXoFkwGjGnyXWhPSYKzbbWdE-NUmgjXPNKld-zUxpPSJoNlXyGKMCk0GAwxT3nWC7nfpVPnYHUAht?purpose=fullsize)

RGB camera

Recommended

* Minimum: 30 FPS

* Preferred: 60 FPS

* Resolution: 1920 × 1080

* Manual exposure and white-balance controls preferred

* Uncompressed or minimally compressed recording

![Neewer RGB660 PRO II 660 PRO-II RGB-WW 50W LED – CameraStuff](https://images.openai.com/static-rsc-4/PqlogoNCfhEKdt6HGRfc4PnLrggjhr16j12nlqcGe0dzjpdZPSK-_AcyZ2KQLA3jkgZ8S3t6WSfq7qx5wMdnJ3cMljcHlPMD-oXoNnm7VdJ73j5rMK8xmBlse1NiWWg16b23AhFxIeo_iJnAcSKSmtOWLqbHCi0xrc7aqFUH1oUpBNB0k1wTkwhZQ0YXTkiY?purpose=fullsize)

LED illumination

* Stable, flicker-free white LED

* Fixed distance from participant

* Fixed brightness and color temperature

* Avoid automatic dimming

![Blood pulse sensor for finger photoplethysmography (PPG)](https://images.openai.com/static-rsc-4/xdplOMv6O8091I35hJsoLUJhK0zR3Ikhc4ODLtRix4Tv822NXjooUds40Cpx1HznWhD8QrTZN7yf9atwmxfxk5_O9JEfAXq8tFMKTFBK95jOwyXO1v_Rda9rsgH212BzOwRe73UTNJncPD9raKdnlDlngcWVJlOfcXi1Qc9EVaV8rINmjYraRFXH746Pcm-k?purpose=fullsize)

Contact PPG reference

* Finger-based reflectance or transmission PPG

* Raw waveform output

* Prefer 100–250 Hz or higher sampling

* Avoid relying only on displayed BPM or SpO₂

![Gallery – The Simon Rogers Group for Soft Matter Research](https://images.openai.com/static-rsc-4/z3kF3FjM6wBR4_DVbuobzIW-7oNIZH7aUJWByUIBN2wN_cTurWip3trrn8ctCszv27tMq9dW7_JBbOPBrQFjaMZzE8ndovrCzeZfvRnbK2G1dxUQQJEaH-E1TxhvZnV5hwG3ep2lbuRNa5p4hF39B39XOZ0VTvcKEc2h3XcfYKo-uXOHUFv9ZsxkMLbBDjhR?purpose=fullsize)

Mounting and synchronization

* Stable camera tripod

* Fixed camera-to-face distance

* Common acquisition clock or synchronization event

* Computer for recording both streams

### 5.2 Physical experimental arrangement

![Checking your browser - reCAPTCHA](https://images.openai.com/static-rsc-4/ZWQz6iKy5ojytKg8tgm07yMa4HHgxWjRvHUnHzInfG0pYX8xMnkp1p8RMb_b6hsEMIKP-lcnptp88VTNVB8L1udR1eu7563UpXyAXfUiFujq224BGL9YZECT1rndbycxrrOi9ZzeQGJReH9ZUZJ0otEAaV1ZWnffNog-djGzi9W56oAdEqJOoljRS1MX47we?purpose=fullsize)

My proposed arrangement:

| Parameter          | Initial setting             |
| ------------------ | --------------------------- |
| Camera distance    | 40–80 cm                    |
| Camera position    | Directly facing participant |
| Face region        | Forehead and cheeks         |
| Frame rate         | 60 FPS preferred            |
| Resolution         | 1920 × 1080                 |
| Lighting           | Controlled LED              |
| Recording duration | 2–5 minutes per condition   |
| Reference sensor   | Finger contact PPG          |
| Reference sampling | 100–250 Hz or higher        |

These are starting experimental settings, not universal optimums.

Important experimental consideration: Your facial camera and finger sensor are measuring pulse waves at different body locations. They will have different pulse arrival times and potentially different waveform shapes.

For stronger morphological validation, I would add a second experiment using a contact reflectance PPG sensor placed on an adjacent facial skin region, if a suitable sensor is available. That helps distinguish differences caused by anatomical measurement location from differences caused by the camera itself.

### 6\. Participant recruitment and experimental protocol

### 6.1 Participants

For a preliminary study, I suggest:

* Pilot: 10 participants.

* Main study: 40–60 participants.

* Include variation in skin tone, age and facial characteristics.

* Obtain informed consent and institutional ethics approval.

The final sample size should be justified using a power analysis based on the primary endpoint and pilot variance.

### 6.2 Experimental conditions

You should not collect data only when participants are sitting still. That would make your research less useful.

I recommend four experimental conditions:

![Burton Doll 🪆](https://images.openai.com/static-rsc-4/KV84bDmpixMrKtw5W36PHsFa8Dwa61Px3s8S-9PZv2h8yCKfEg56YxcoM9KlaJxfgMXxEvgqnXpaOtdUgGqTrDLeQG62aCAwUbvGjkxguOZZ8Uh-wbdvrKWnHOxx2C5xw1t3HYyi6jhaxF1ftainkGQ9yRwqAW5DzCqGRiJgyzGC8tscmI84wsuh6-oL9ubb?purpose=fullsize)

Condition 1: Stationary resting

Primary baseline

* Participant sits still.

* Normal breathing.

* No talking.

* Controlled illumination.

Duration: 3 minutes.

![Screen view young male sitting at desk speaking via videocall](https://images.openai.com/static-rsc-4/nbqsM8J2juIt50vJ_beylxHXNfV5vQg2KuwHTrvhkSlh9B41AZupXujSVoy3_3kKpA9kCLft1D_JskSwQfoS-FxZOqf-IJM2pecWkYtV17WCuaqXl8r_67ltEZsW32ZVwiM6NqEmKSDPBF2SzJTFbjtq67ZMCIcX1-1Ujdv2zj4it1eCu2YZqVkv52kJdTDd?purpose=fullsize)

Condition 2: Facial movement

* Talking.

* Blinking.

* Small head movements.

Duration: 2 minutes.

![How to Instantly Improve Your Webcam Quality

        – Fantech World](https://images.openai.com/static-rsc-4/EEbZVqV02FAXM1l8MCSDDbcoSOKpWQSMPjB0mVBAqCJJvXulYKnA81KfYOi2STOboLu4haoW9qAtOrgqNzOF2S1mfgeIGsB8oDstXeSOHxPPZo4vn99mTGaoD7fhIoVhOqE2QgwFumBltnA9NmEJGsMb2F8C3nsc7pGuhZNOZxTQYXeQ_Akl5NQjcsWx2Yr7?purpose=fullsize)

Condition 3: Illumination variation

* Fixed illumination.

* Reduced illumination.

* Moderate illumination changes.

Duration: 2 minutes per setting.

![Young man working out at the gym](https://images.openai.com/static-rsc-4/xZftpJyHyT0CAj9XbsUYPHMOp3f0eYeROCRv_iA-E-lDuvtdvPbJDYPEGZav8X96NAHkKCM9gBj-MHDOUzejPITbWaEmsqk058-NpgTslDYRn-6rNG5CbSGKe1yhn1npJotc32b5RPuXcGx_B3wShohuCRRPlvTVw-RDx94tvpiqFVkBGZZqHt4WsOBwr0Ee?purpose=fullsize)

Condition 4: Physiological variation

* Resting measurement.

* Mild, ethically approved physical activity.

* Post-activity recovery.

Duration: 2–3 minutes per phase.

Keep the reference PPG and camera recording active simultaneously throughout each condition.

The primary analysis should be performed on stationary recordings first. Other conditions should test robustness.

### 6.3 Synchronization

This is one of the most important parts of your experiment.

If the camera records at 30 FPS and the contact sensor records at 100 Hz, their samples will not naturally have matching timestamps.

I recommend:

* Use a common computer clock where possible.

* Record actual frame timestamps rather than assuming perfectly constant FPS.

* Generate a synchronization event visible in the camera and recorded in the reference acquisition system, such as a synchronized LED flash and digital trigger.

* Correct for the known measurement-site pulse delay.

* Resample signals to a common time base only after timestamp alignment.

Do not use peak matching to synchronize the entire test recording and then report the resulting correlation as independent evidence. That risks artificially inflating agreement.

### Part IV — Signal processing and waveform extraction

### 7\. Extracting RGB signals from facial video

This is your first implementation milestone.

For each video frame, extract the average RGB values from the selected skin regions.

Suppose:

I_t(x,y,c)

represents pixel intensity at time , pixel position , and color channel .

For each region of interest:

R(t)=\\frac{1}{N}\\sum_{(x,y)\\in ROI}I_t(x,y,R)G(t)=\\frac{1}{N}\\sum_{(x,y)\\in ROI}I_t(x,y,G)B(t)=\\frac{1}{N}\\sum_{(x,y)\\in ROI}I_t(x,y,B)

You now have three time-series signals.

![Optimal facial regions for remote heart rate measurement during physical and cognitive activities | npj Cardiovascular Health](https://images.openai.com/static-rsc-4/cc-Rx8vBvnfYqEPUNTJJz964Ma_I2od2vP1Xi-9m9VTneZ9puuQUR33Qtwxz5qGCLmqYV5Qg9spyFs00-zWSGs-IPKeZmkm2QzJzITCrdppdk7TIWHdeF49qACaroG0qhdKwA25ctMTZ2uJ0cdD2CxV7314d8mjqPPsh1bgyRqf6F-g6vSq06oW5K6Zw0M3D?purpose=fullsize)

### Recommended ROI selection

Use three independent regions:

* Forehead.

* Left cheek.

* Right cheek.

Do not combine them immediately.

First investigate their individual signal quality. Then compare:

* Forehead rPPG.

* Left-cheek rPPG.

* Right-cheek rPPG.

* Combined facial rPPG.

For face detection and tracking, use MediaPipe Face Mesh or an equivalent landmark-tracking framework.

The Ontiveros study used 468 facial landmarks and combined forehead and cheek regions. This is a good starting point for your implementation. PMC

### 8\. Implement five baseline extraction algorithms

I recommend comparing these methods before developing your own reconstruction model.

Algorithm 1 — GREEN

Implement firstS(t)=G(t)

Simple green-channel intensity extraction.

Advantages:

* Very easy to implement.

* Good baseline.

* Low computational cost.

Limitation: sensitive to illumination changes and motion.

Algorithm 2 — CHROM

Chrominance-based extraction separates color variations that are associated with pulsatile skin changes from some common-mode illumination effects.

Common formulation:

X=3R-2GY=1.5R+G-1.5BS=X-\\alpha Y

Here, is determined from the relative standard deviations of the two components over a window.

Reference: de Haan and Jeanne, 2013.

Algorithm 3 — POS

High priority

Plane-Orthogonal-to-Skin (POS) uses a projection of normalized RGB signals to suppress certain illumination-related variations.

It is an excellent candidate for your baseline comparison.

Reference: Wang et al., 2016.

Algorithm 4 — ICA

Independent Component Analysis separates statistical components from the RGB observations.

The objective is to isolate the component most consistent with the cardiac pulse.

Algorithm 5 — PCA

Principal Component Analysis transforms the three color channels into orthogonal components.

Compare the extracted components against the contact reference using a validation set, not by choosing the best component separately on every test recording.

My recommendation: GREEN, CHROM and POS should be your initial core algorithms. Add ICA and PCA for completeness.

### 9\. Preprocessing

After extraction, apply the following processing pipeline:

* Timestamp correction

    Correct irregular video frame intervals and synchronization offsets.

* Signal normalization

    Remove intensity scaling and slow illumination-related variation.

* Detrending

    Remove baseline wandering.

* Band-pass filtering

    Start with 0.5–5 Hz, corresponding approximately to 30–300 BPM.

* Artifact suppression

    Detect motion, sudden illumination changes and corrupted frames.

* Signal quality assessment

    Identify segments where waveform reconstruction is unreliable.

One important point about filtering: do not blindly apply aggressive smoothing. The dicrotic notch and secondary waveform features can be weakened by excessive filtering.

Also, a 30 FPS camera has a Nyquist frequency of 15 Hz, while 60 FPS gives 30 Hz. Higher frame rates provide more temporal information for morphology. Interpolation cannot recover information that the camera never captured.

### Part V — Contact PPG waveform reconstruction

### 10\. The central contribution: reconstructing the contact-like waveform

This is where your research can become more interesting.

There are two approaches.

### Approach A — Classical signal processing

Start with the raw rPPG output and improve it through:

* Baseline correction.

* Filtering.

* Motion compensation.

* Adaptive noise suppression.

* Beat segmentation.

* Morphological feature enhancement.

The output should remain directly traceable to the optical camera measurements.

### Approach B — Supervised waveform reconstruction

Recommended second research stage

Train a model using paired recordings:

* Input: camera-derived rPPG.

* Target: simultaneous contact PPG.

* Output: reconstructed contact-like PPG waveform.

![PulseGAN | CSY's blog](https://images.openai.com/static-rsc-4/tb2KS84wnIYekEhE_v3qiWuITkZor8Bcihb8VxkvMlsjSiaq6q8E2gI_Is7up4HQ3iWnX_v2cBS4aj4UCnZbtU9Uk9E_qwhvyfWzxB_3yA0YgFm1lwx8jbhPohwjhatBu8oBp5GyBPq9sJPyJqaxKDJ9VEzTzslhXxhL316kCvCqdQGJwKEWwv2SQrV0jQAi?purpose=fullsize)

I would begin with a 1D temporal CNN or U-Net, rather than immediately using a large transformer or GAN.

Why?

* Lower computational requirements.

* Easier to train on limited datasets.

* Easier to interpret.

* More straightforward comparisons against classical processing.

### 10.1 Proposed neural network

Input

X\\in\\mathbb{R}^{N\\times 1}

Raw or POS/CHROM-derived rPPG segment

Conv1D + Batch Normalization + ReLU

Residual temporal blocks

Learn local pulse morphology and temporal patterns

Upsampling / temporal reconstruction

Output

\\hat{Y}\\in\\mathbb{R}^{N\\times 1}

Reconstructed contact-like PPG waveform

You can later investigate a multichannel model that receives GREEN, CHROM and POS signals together.

### 10.2 Training loss function

Do not train your model using only mean squared error.

A model can produce a smooth waveform with low pointwise error while losing important morphological features.

I suggest a composite loss:

L_{\\mathrm{total}}=
\\lambda_1 L_{\\mathrm{waveform}}+
\\lambda_2 L_{\\mathrm{derivative}}+
\\lambda_3 L_{\\mathrm{spectral}}+
\\lambda_4 L_{\\mathrm{peak}}

Where:

1\. Waveform loss

L_{\\mathrm{waveform}}=
\\frac{1}{N}\\sum_{i=1}^{N}
(\\hat y_i-y_i)^2

This measures direct waveform reconstruction error.

2\. Derivative loss

L_{\\mathrm{derivative}}=
\\frac{1}{N-1}
\\sum_{i=1}^{N-1}
(\\Delta\\hat y_i-\\Delta y_i)^2

This encourages preservation of the systolic upstroke and waveform shape.

3\. Spectral loss

Compare frequency-domain representations of the reconstructed and reference signals.

This discourages the model from producing physiologically implausible frequency content.

4\. Peak-related loss

Penalize differences in detected systolic peak timing and amplitude, where the reference peaks are reliably identifiable.

The coefficients should be tuned using training and validation data only.

### Important scientific precaution

A reconstruction network can learn to produce an average-looking PPG waveform even when the camera input contains insufficient physiological information.

That is a serious risk.

I would therefore include:

* An input-quality threshold.

* A confidence score.

* An uncertainty estimate.

* A comparison against a simple non-learning baseline.

* A test for whether the reconstructed morphology is supported by the input signal.

The model must not invent a dicrotic notch when the camera data does not contain enough information to identify one.

### Part VI — Validation and statistical analysis

### 11\. How will you prove that the reconstructed waveform resembles contact PPG?

This is arguably the most important chapter of your research.

You should evaluate waveform-level agreement, not just heart-rate agreement.

### 11.1 Primary validation metrics

| Metric                | Purpose                                   | Priority |
| --------------------- | ----------------------------------------- | -------- |
| Pearson correlation   | Waveform similarity                       | High     |
| Normalized RMSE       | Waveform reconstruction error             | High     |
| Cross-correlation     | Temporal alignment                        | High     |
| DTW distance          | Similarity under local timing differences | High     |
| Cosine similarity     | Overall signal similarity                 | Medium   |
| Bland–Altman analysis | Agreement in derived measurements         | High     |
| SNR                   | Pulse signal quality                      | Medium   |

I recommend making Pearson correlation and normalized RMSE your primary waveform-level metrics, alongside a morphology-specific endpoint.

### 11.2 Morphological validation

![Photoplethysmography Signal Processing and Synthesis | Peter Charlton](https://images.openai.com/static-rsc-4/jv8hByVp-sj1zl8AWScnOCo2KVohW8OMug2UeMoQjgXcM_kql6RCfMZn4ZTzqg6BLP_lbRkOPWkhnxJetHR4e9-jj7SJsgqEE58Jcjl8ibb5tfy4EMcVYhbYrF8bUEs_-u2ajfSDv0dLk4OB_vCbICD_bYsbwsG_gVaPNpoYxPqwIr9YN4JzMN_YL6o6bOSQ?purpose=fullsize)

Extract these features from both signals:

| Feature                  | Description                   |
| ------------------------ | ----------------------------- |
| Systolic peak amplitude  | Maximum pulse amplitude       |
| Systolic rise time       | Pulse onset to systolic peak  |
| Systolic width           | Width of the systolic portion |
| Dicrotic notch timing    | Time to secondary notch       |
| Diastolic wave amplitude | Secondary wave amplitude      |
| Pulse width              | Duration of one pulse         |
| Inter-beat interval      | Time between successive beats |

Not every feature will be reliably visible in every subject or recording. Define rules for excluding unidentifiable landmarks before analysis.

### 11.3 Important distinction: correlation versus agreement

Consider these two waveforms:

Example A — High correlation, different amplitude

Camera PPG

Contact PPG

Illustrative only: same pulse timing, different amplitude.

Example B — Similar frequency, different morphology

Camera PPG

Contact PPG

Illustrative only: similar beat frequency, different pulse morphology.

This is why a study reporting only BPM accuracy is insufficient for your objective.

### 11.4 Alignment strategy

I recommend two separate comparisons:

Comparison 1: Timing agreement

* Align signals using independent synchronization.

* Estimate and report the residual lag.

* Compare pulse timings and inter-beat intervals.

Comparison 2: Morphological agreement

* Use corresponding beat windows.

* Normalize amplitude for shape comparisons.

* Compare systolic rise, peak, decay and secondary features.

* Report the amplitude and morphology analyses separately.

Use DTW as a secondary analysis. Do not use unrestricted DTW to claim precise temporal agreement because it can warp away genuine timing errors.

### 11.5 Statistical analysis

Use:

* Bland–Altman plots for derived feature agreement.

* Intraclass correlation coefficient (ICC) for repeatability/agreement where appropriate.

* Subject-level bootstrap confidence intervals.

* Friedman test for comparing multiple extraction algorithms on the same subjects.

* Appropriate post-hoc tests with multiple-comparison correction.

* Mixed-effects models for repeated measurements across subjects and experimental conditions.

Treat the participant, not every individual video frame, as the independent statistical unit.

### 12\. Proposed experimental comparison matrix

I would organize the main experiment like this:

| Experiment | Camera signal    | Reconstruction               | Reference   |
| ---------- | ---------------- | ---------------------------- | ----------- |
| E1         | GREEN            | None                         | Contact PPG |
| E2         | CHROM            | None                         | Contact PPG |
| E3         | POS              | None                         | Contact PPG |
| E4         | ICA              | None                         | Contact PPG |
| E5         | PCA              | None                         | Contact PPG |
| E6         | Best baseline    | 1D CNN                       | Contact PPG |
| E7         | Multichannel RGB | 1D CNN                       | Contact PPG |
| E8         | Best model       | Quality-aware reconstruction | Contact PPG |

Your principal comparison should be:

Best conventional rPPG algorithm versus reconstructed rPPG.

This establishes whether machine learning actually improves waveform morphology rather than simply improving heart-rate estimation.

### Part VII — Dataset and implementation plan

### 13\. Public datasets to use before collecting your own data

I strongly recommend a two-stage development strategy:

* Develop the algorithm using publicly available synchronized datasets.

* Conduct your own controlled experiment for independent validation.

![Multi-scene low-light remote physiological measurement database | Machine Vision and Applications](https://images.openai.com/static-rsc-4/fJ-GdRmt0L-16ea40IL6YCPDcUs911jSSOfnsLc8APz4eRf41FYymTWP0Oqg7dLO-urEtZks6EPu5eFZ5vbW-ukrx7kyd1c7T39AqRkq4VpZhNxafsphkUa4MyxG4yFPlbQjgBQe6MkLjWJbFqq8uJnd3ye0FWXvIuF4mmRH4Fkmmyx6e9D5IGbBQsCM1DR8?purpose=fullsize)

PURE dataset

Recommended starting dataset

* 10 participants.

* 60 video sequences.

* 30 FPS, 640 × 480.

* Different head-motion conditions.

* Contact PPG reference.

[Dataset access](https://www.tu-ilmenau.de/en/university/departments/department-of-computer-science-and-automation/profile/institutes-and-groups/neuroinformatics-and-cognitive-robotics/data-sets-code/pulse-rate-detection-dataset-pure?utm_source=chatgpt.com)

![UBFC-rPPG数据集下载方式-CSDN博客](https://images.openai.com/static-rsc-4/fZQlIEaNUAgPW1Vwsr-G9eaLeSEmakt1uGJHTywtaZRow15VXx4XBNj7ReVjK-BzFJBKVrs7uDSXO5v6Tbe0BncTEjsAAKEPF2RpQr9-tGBFxU0zfpXtiEjVk8w66mOGYp0sEXSoPnkbYu7TO5vj05r9uXMu0RlX8ynv4GIu8xcfB57ltzA3-ixTxs_grohu?purpose=fullsize)

UBFC-rPPG

* 42 participants.

* 30 FPS.

* 640 × 480.

* Synchronized contact PPG.

* Useful for subject-independent validation.

[Dataset access](https://sites.google.com/view/ybenezeth/ubfcrppg?utm_source=chatgpt.com)

![Heart Rate Measurement Based on 3D Central Difference Convolution with Attention Mechanism | MDPI](https://images.openai.com/static-rsc-4/utgYuCvqYZqCkL1o57b-wvEmwgUvnuhZ0418sGeQQ-CJUdPh7msmUAZ4L1_xm5VqhlIbQYt8u3biey9mJ23FDb5q6tiXrwcC3ymZ2xeXfFLz7gw9c1nezEfjh1fCINe1PZRJTfzXFBLvfIzd28xMGdVmexnv_BWV6yp4Z7FIgKVEgoB-8Is1WktEdEgDVU7Y?purpose=fullsize)

LGI-PPGI

* Multiple activity conditions.

* Facial video.

* Contact PPG reference.

* Useful for testing motion robustness.

[Dataset repository](https://github.com/partofthestars/LGI-PPGI-DB?utm_source=chatgpt.com)

The PURE and UBFC datasets are particularly useful for an initial development pipeline. Their acquisition characteristics and reference signals are described in the comparative RGB study. PMC +1

Important: Before training, inspect the actual dataset files, sampling rates, timestamps, reference sensor characteristics and licensing conditions. Do not assume all contact signals are equivalent or that every dataset provides identical raw waveform quality.

### 14\. Software implementation

I recommend Python as your primary research environment.

| Task                   | Suggested library   |
| ---------------------- | ------------------- |
| Video acquisition      | OpenCV              |
| Face tracking          | MediaPipe           |
| Signal processing      | SciPy               |
| Numerical analysis     | NumPy               |
| Data handling          | Pandas              |
| Visualization          | Matplotlib          |
| Machine learning       | PyTorch             |
| Statistical analysis   | SciPy / Statsmodels |
| PPG feature extraction | NeuroKit2           |
| rPPG algorithms        | pyVHR               |

Useful references:

* [pyVHR — remote PPG processing framework](https://github.com/phuselab/pyVHR?utm_source=chatgpt.com)

* [NeuroKit2 — physiological signal processing](https://github.com/neuropsychology/NeuroKit?utm_source=chatgpt.com)

* [MediaPipe Face Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker?utm_source=chatgpt.com)

### Proposed software structure

```text
RGB_PPG_RESEARCH/
│
├── datasets/
│   ├── PURE/
│   ├── UBFC/
│   └── CUSTOM/
│
├── acquisition/
│   ├── camera_recording.py
│   ├── contact_ppg_recording.py
│   └── synchronization.py
│
├── roi_extraction/
│   ├── face_detection.py
│   ├── forehead_roi.py
│   └── cheek_roi.py
│
├── signal_extraction/
│   ├── green.py
│   ├── chrom.py
│   ├── pos.py
│   ├── ica.py
│   └── pca.py
│
├── preprocessing/
│   ├── detrending.py
│   ├── filtering.py
│   └── motion_removal.py
│
├── reconstruction/
│   ├── cnn_model.py
│   ├── training.py
│   └── inference.py
│
├── validation/
│   ├── waveform_metrics.py
│   ├── morphology.py
│   ├── alignment.py
│   └── statistical_analysis.py
│
└── results/
    ├── waveforms/
    ├── metrics/
    └── figures/
```

### Part VIII — Machine-learning experimental design

### 15\. Training and testing strategy

This is where many rPPG studies can accidentally produce misleading results.

You must split data by participant, not by randomly selecting video frames.

For example, if the same participant appears in both training and testing, the model may learn participant-specific optical characteristics.

I recommend:

| Dataset portion | Participants | Purpose                       |
| --------------- | ------------ | ----------------------------- |
| Training        | 70%          | Learn waveform reconstruction |
| Validation      | 15%          | Hyperparameter optimization   |
| Testing         | 15%          | Independent evaluation        |

Use subject-independent splitting.

An even stronger experiment would be:

* Train on PURE.

* Validate on a subset of PURE participants.

* Test on UBFC-rPPG without retraining.

This provides evidence of cross-dataset generalization, although differences in sensors, lighting and acquisition conditions must be acknowledged.

### Proposed ablation experiments

You should also investigate:

* Does the model perform better with GREEN than POS?

* Does combining forehead and cheek signals improve reconstruction?

* Does including RGB channels improve performance?

* Does derivative-based loss improve systolic morphology?

* Does quality-aware training improve performance under motion?

* Does the model generalize to previously unseen participants?

These experiments will make your research substantially stronger.

### Part IX — Expected research contributions

### 16\. What should your final research demonstrate?

I would aim for the following outputs:

### Expected research deliverables

1\. RGB acquisition system

Core

A working non-contact optical PPG recording system.

2\. Signal extraction comparison

Core

A quantitative comparison of GREEN, CHROM, POS, ICA and PCA.

3\. Waveform reconstruction model

Core

A trained model that converts camera-derived pulse information into a contact-like waveform.

4\. Morphological validation

Core

Evidence of agreement in systolic peaks, timing and secondary waveform features.

5\. Robustness evaluation

Extension

An assessment of illumination, motion, frame-rate and skin-tone effects.

### 17\. Suggested research timeline

A realistic initial research schedule is approximately six months.

| Month | Main activity                                           |
| ----- | ------------------------------------------------------- |
| 1     | Literature review, dataset acquisition, protocol design |
| 2     | Camera acquisition and ROI extraction                   |
| 3     | GREEN, CHROM, POS, ICA and PCA                          |
| 4     | CNN waveform reconstruction                             |
| 5     | Experimental validation and statistical analysis        |
| 6     | Thesis writing, figures and publication preparation     |

### Part X — Proposed thesis formulation

### 18\. Recommended title

My preferred title is:

"Camera-Based Reconstruction of Photoplethysmographic Waveforms Using RGB Video and Deep Learning: A Comparative Study with Contact PPG."

Alternative titles:

* Morphological Reconstruction of Contact Photoplethysmography from Facial RGB Video.

* Non-Contact PPG Waveform Estimation Using Reflected Light and RGB Camera Technology.

* Deep Learning-Based Reconstruction and Validation of Remote Photoplethysmographic Signals.

### 19\. Proposed thesis chapter structure

| Chapter                 | Contents                                                     |
| ----------------------- | ------------------------------------------------------------ |
| 1. Introduction         | Background, motivation, objectives, research questions       |
| 2. Literature Review    | PPG, rPPG, RGB extraction, signal processing, reconstruction |
| 3. Methodology          | Hardware, acquisition, datasets, algorithms, synchronization |
| 4. Proposed Model       | Signal extraction and reconstruction architecture            |
| 5. Experimental Results | Waveforms, morphological comparison, metrics                 |
| 6. Discussion           | Findings, limitations, generalization and implications       |
| 7. Conclusion           | Contributions, future research                               |

### Part XI — Three scientific issues I would pay particular attention to

These are important enough that I would make them explicit in your research proposal.

1\. Are you reconstructing the true physiological waveform or merely predicting a typical PPG shape?

A deep-learning model might generate a visually convincing waveform even when the camera signal is poor. Your validation should demonstrate that the output changes appropriately with the measured pulse and preserves individual beat morphology.

2\. Can RGB camera data resolve the dicrotic notch?

This is a particularly interesting research question. A 30 FPS camera provides a temporal resolution of approximately 33.3 ms per frame. That can be limiting for fine waveform morphology. I would test 60 FPS or higher if hardware permits, and report the effect of frame rate on notch detection.

3\. Are you comparing the same physiological measurement?

A facial camera and fingertip sensor observe different peripheral vascular beds. Their pulse morphology can differ even when both measurements are accurate. This is why I recommend an additional adjacent-site contact reference experiment if feasible.

### My final recommendation: start with these three experiments

Rather than implementing the entire research pipeline at once, I would prioritize these experiments.

Experiment 1 — Start here

Can raw RGB video recover the contact PPG waveform?

* Acquire synchronized RGB and contact PPG.

* Extract forehead and cheek RGB signals.

* Compare GREEN, CHROM and POS.

* Evaluate waveform morphology and timing.

Outcome: Establish whether your camera data contains enough information.

Experiment 2

Can signal processing improve waveform morphology?

* Compare filtering and detrending methods.

* Investigate derivative-based feature detection.

* Evaluate systolic peak and dicrotic notch recovery.

Outcome: Establish the best conventional signal-processing baseline.

Experiment 3

Can deep learning reconstruct contact-like PPG?

* Train a 1D CNN.

* Use paired rPPG and contact PPG.

* Compare reconstructed and original camera waveforms.

* Test on unseen participants.

Outcome: Determine whether reconstruction provides a meaningful improvement.

### 20\. A particularly important research opportunity

I would make one additional experiment a central contribution:

Determine how much waveform morphology can be recovered from RGB video without using contact PPG during inference.

There are three distinct operating modes:

| Mode                      | Contact PPG used?    | Scientific purpose                       |
| ------------------------- | -------------------- | ---------------------------------------- |
| Conventional rPPG         | No                   | Extract pulse directly from video        |
| Supervised reconstruction | During training only | Learn camera-to-contact waveform mapping |
| Final deployment          | No                   | Reconstruct waveform from camera alone   |

Your final system should operate in the third mode.

That gives you a clear and defensible research contribution: a non-contact camera system that produces a continuous PPG-like waveform, with its accuracy and limitations quantified against an independent physiological reference.

### 21\. Three decisions before implementation

I would like to narrow down the hardware and methodology before developing the actual Python implementation.

1\. What RGB camera do you have access to?

Ordinary webcam (Logitech or similar)

- [x] Smartphone camera

- [ ]Industrial RGB camera

- [ ] High-speed RGB camera

- [ ] Not purchased yet

2\. What contact PPG reference can you use?

Finger sensor with raw PPG waveform output

Commercial fingertip pulse oximeter

MAX30102 or similar development module

Clinical-grade PPG monitor

I don't have a contact sensor yet

3\. What computing resources are available?

- [x] NVIDIA GPU
- [ ] CPU-only computer
- [ ] Google Colab
- [ ] Cloud GPU / research server

**Finalize implementation design**

With these decisions, the next step can be a reproducible implementation: first extracting the camera-derived waveform, then comparing it against the raw contact PPG, and finally developing the reconstruction model.

One guiding principle: Do not start by making the camera waveform look like a conventional PPG. First establish what physiological information the camera actually captures. Then demonstrate that your reconstruction preserves that information.

That will make the research scientifically much stronger.

# Part-3 (Finalize implementation design)
### Complete implementation plan: Smartphone RGB camera to reconstructed PPG waveform

Given your available resources:

* Camera: Smartphone RGB camera.

* Reference: Finger sensor providing raw PPG waveform.

* Computing: GPU-enabled computer.

I recommend building a synchronized dual-channel acquisition system, where the smartphone captures facial reflected-light variations and the finger sensor records conventional PPG simultaneously.

The first objective is to demonstrate that the smartphone-derived signal contains enough information to reproduce the temporal and morphological characteristics of the contact PPG.

I would implement this in Python using OpenCV, SciPy, MediaPipe, NumPy and PyTorch.

### Your proposed experimental system

![Contactless pulse measurement falters at high heart rates, finds study](https://images.openai.com/static-rsc-4/2bi9uSU_TKRm4haQ0oehAU3_CBJhDFL0MPxEr9w-44FbOKuDmZCzn6TipLtZfDInUdoRsLi6MAZJPAN9nKuQJ0Dza_xGSgvKQTGbQfoASuZwGE__WaiyIaKwZ478oWJXXPLVe4cKEgRHKym08g_KQsZ0kV63MN-iGMcjzpEJ1SASB6358zCHNRBHHj3JKMSS?purpose=fullsize)

Camera channel

### 30–60

Target FPS

Contact channel

### 100–250

Target PPG samples/second

Recording duration

### 180 s

Initial resting experiment

Processing

### GPU

PyTorch reconstruction

There is one important hardware decision: I would use a smartphone with manual camera controls, rather than relying on the standard automatic camera application.

Auto-exposure, auto-white-balance, variable frame rate and video compression can significantly alter the subtle color changes that carry the PPG information.

### 1\. Hardware acquisition design

### 1.1 Proposed hardware components

![La caméra TrueDepth de l'iPhone peut servir à animer des personnages dans l'Unreal Engine - iGeneration](https://images.openai.com/static-rsc-4/I5dLZEOH59upC7E9_jlkUJCCptJ49vzgrSQjs9okhnySdJZ9lnWPF9vR8cL7Ynt11kOOlXmK5pNbWMx81t0Iv5SlafAnB1QRjMVqX5ROwP7Hy5UV8OxhI8XFo5rU5Mi1yjeiphXX0o7TygIIbDIJKJ4kXcMKVjEKENV4Uky6U_-MVUUMJczRYC3Eo4-WKnTt?purpose=fullsize)

A. Smartphone RGB camera

* 1080p recording.

* 60 FPS preferred, if genuinely supported.

* Manual ISO and exposure.

* Locked focus and white balance.

* Original video file without social-media processing.

![MAX30102 - Optical Heart Rate Sensor - Purple COM55, R24 - Faranux Electronics](https://images.openai.com/static-rsc-4/FLL0Rib-W03OrUnV8HVfzsp0R46nXrrKjU15m7aracplAyQyytHVz1yaxxpZCJrx0LRMa5WCNU025YgEp5v06l7FY6jOJGgSZTaRAE4pn4eojido8XMgfFiZh5jM_huKrFAqX9VaCeDy8EBVoOsjdf7c3QWJn-CleGsMuP8EhdplPr7cfwmA_1dGX54I7YvA?purpose=fullsize)

B. Finger PPG acquisition module

Recommended options:

* MAX30102 development board.

* Raw PPG output through I²C.

* ESP32 or Arduino-based acquisition.

Important: MAX30102 uses red and infrared LEDs. This is suitable as a contact reference, but the reference waveform is not optically identical to facial RGB rPPG.

![Probots ESP32 38-Pin NodeMCU WROOM-32 Dev Board Buy Online India](https://images.openai.com/static-rsc-4/sGtRSc8YEx5nDR_0HIziXbLIE1nGJyIQqfxnS4wLQ9G3bXXvPrr9DgJAU2Mqq-V1Lf90MPGhtmLm2cFbLjYlnAz81EUQaXsPz25H3Uxan25UbgrzRYPcYrzoArsdl1Ak6Ne42FFsd4vfLPVGF7BuYj_NKan0ussI0EU7FohTY4Ur1p_9-RCqVp2QZ219vqDI?purpose=fullsize)

C. Microcontroller

* ESP32 development board.

* Reads contact PPG.

* Records timestamps.

* Generates synchronization markers.

* Streams data to the computer.

![RaLeno LED Video Light 3200-5600K Dimmable White

        –
        Electroeshop](https://images.openai.com/static-rsc-4/nnnocRcVhFKsZuE203NP-X22IDmrkRrq4UEhzi0YTHbuUTsCM87BWtwqbwIsatKfRpRxBE36IG06MvMHVXoULBxMYlvdM9_TxgiQ-JD8YLk-Br4YSNtLYWdhcX9_UXfY0O94Onz_swddvFwwBE50UFzuJ_um4CU0LSv_2CXBwuSN0pYsLVgKFM_0qUtwRCHH?purpose=fullsize)

D. Illumination

* Stable white LED panel.

* Fixed brightness.

* No automatic dimming.

* Avoid visible flicker.

Use the same lighting position throughout the baseline experiment.

![Phone Clamp Aluminum at Kenneth Locke blog](https://images.openai.com/static-rsc-4/nGhsKjoYRYhtWUZuwOEQ83eZudiIy1BnJ86xwydGzx9P7lXWPT_YQtm17MO1892EmProaz8AKADE-efV7fqCB4cTobJhUe7o-yW8EgGhGtkdiiHl4zrgiXzKZ1LPJ_B-pnJdGM9l2nVUAj24bV6gxsIeFXv0PLhMNG8N40prKq44HUjdzUFzXKgDPxDeh8xe?purpose=fullsize)

E. Mounting

* Smartphone tripod.

* Fixed participant position.

* Fixed camera distance.

* Avoid handheld recording.

### 1.2 Physical arrangement

![Evaluation of Remote Photoplethysmography Measurement Conditions toward Telemedicine Applications](https://images.openai.com/static-rsc-4/OIaTVPLaNOJKSkAeWGBjAKhP4ad_itUjMmi2kqbf2aXueRxaun3AuVqomHAYhUsx6-LYoxBCZt4TsYyR5jx_WmigMlT0SgC2IvIRTBKiJY0gf8cZUzxCE5ol5-ld8RulRILRz5Jb6JgK8fht8eTJDzyZNYsnFZXSumZBw_VlzHTjfTqHwH4cbdBm_w1TQuC9?purpose=fullsize)

Recommended initial geometry:

| Component   | Position                                     |
| ----------- | -------------------------------------------- |
| Smartphone  | 50–70 cm from face                           |
| LED panel   | Approximately 30–45 degrees from camera axis |
| Participant | Seated, facing camera                        |
| Finger PPG  | Index finger, comfortably attached           |
| Face ROI    | Forehead and both cheeks                     |
| Background  | Neutral, non-reflective                      |

Keep the camera and light stationary.

The finger sensor must not be too tight, and the participant should avoid unnecessary finger movement.

### 1.3 Smartphone camera application

For this project, I recommend a camera application that supports manual capture controls.

Two possible approaches:

* Android: build a custom application using Camera2 or CameraX with supported manual sensor controls.

* iPhone: use a camera application that supports manual exposure and frame-rate locking, subject to device limitations.

For Android, the Camera2 API gives you better control over exposure time, ISO, frame duration and white balance when the hardware supports them.

Documentation: [Android Camera2 API](https://developer.android.com/media/camera/camera2?utm_source=chatgpt.com).

My preference: Android with Camera2, because you can eventually integrate camera recording and synchronization into one acquisition application.

Do not assume that selecting 60 FPS in a camera application guarantees exactly 60 unique, uniformly timed frames. Verify actual frame timestamps and dropped frames.

### 2\. Synchronization circuit and software

This is a critical part of the experimental design.

You will have two independent data streams:

* Smartphone video.

* Finger-contact PPG.

If they are not synchronized accurately, waveform correlation and morphology measurements can be misleading.

### 2.1 Recommended synchronization architecture

ESP32 microcontroller

Master acquisition clock and synchronization event

MAX30102

Finger PPG samples + timestamps

LED marker

Visible synchronization flash

Computer

USB serial PPG acquisition + synchronization event log

Smartphone camera

Facial video records the same visible LED marker

Offline synchronization

Match the LED event in video to its microcontroller timestamp

### Important: use a visible synchronization LED

The microcontroller can switch an LED on and off at predetermined times.

For example:

* LED OFF for 2 seconds.

* LED ON for 200 milliseconds.

* LED OFF for 2 seconds.

* LED ON for 200 milliseconds.

The smartphone video records these events.

The ESP32 records the exact transition times using its monotonic hardware timer.

This provides an independent synchronization reference.

Do not use the smartphone recording start time as the sole synchronization reference. The camera's internal capture pipeline can introduce unpredictable delays.

### 2.2 Synchronization circuit

![Lezione 14: Sensore di Frequenza Cardiaca e Ossimetro (MAX30102) — SunFounder Universal Maker Sensor Kit  documentazione](https://images.openai.com/static-rsc-4/Nl0hSTIugdAr0tuui_LIQMv2MIvBpmNzqwXDgOArf3COo1IY5z5BV5TvwpMjSb9JvLhu4TwaFg6XRyydpWUAbj2kMssXYilUWghcE7gzVHyoxTAeQhiit7D4QNYpaDWlR4MFTHCJQwZ3R8rD4fju3PFLg6q5SBymX20jhuX5YTERlyh1T-lgr9an3bJWVVmO?purpose=fullsize)

Suggested wiring:

| ESP32   | MAX30102                    |
| ------- | --------------------------- |
| 3.3V    | VIN, if board supports 3.3V |
| GND     | GND                         |
| GPIO 21 | SDA                         |
| GPIO 22 | SCL                         |

Synchronization LED:

| ESP32   | Component                      |
| ------- | ------------------------------ |
| GPIO 18 | LED through 220–330 Ω resistor |
| GND     | LED return                     |

Check your specific MAX30102 breakout board's voltage requirements before connecting it.

For a more precise system, use a transistor-driven LED and a dedicated digital synchronization output. Never connect the LED directly to a high-current supply through a GPIO pin.

Important limitation: The visible LED event synchronizes the camera and sensor clocks, but it does not eliminate uncertainty caused by rolling shutter, exposure integration or variable frame timestamps. Record the event's appearance across multiple frames and quantify the residual synchronization error.

### 2.3 ESP32 firmware design

The firmware should perform four operations:

* Initialize the MAX30102.

* Read raw PPG samples from its FIFO.

* Timestamp every sample using a monotonic microsecond clock.

* Generate synchronization LED events.

A useful serial data format is CSV:

```text
type,timestamp_us,red,ir,green,event
PPG,1000000,123456,654321,0,
PPG,1004000,123470,654315,0,
PPG,1008000,123480,654310,0,
SYNC,3000000,0,0,0,LED_ON
SYNC,3200000,0,0,0,LED_OFF
```

The green column is optional if your particular sensor does not support green acquisition.

For MAX30102, red and infrared are the relevant channels. Do not treat its red/IR output as an RGB reference.

Firmware implementation requirements:

* Configure a fixed sampling frequency, initially 100 or 200 Hz.

* Use the sensor FIFO and check for overflow.

* Preserve sample order and sample counters.

* Timestamp samples at acquisition time, not when serial data reaches the computer.

* Avoid blocking delays while reading the sensor.

* Record sensor configuration in the experiment metadata.

The MAX30102 FIFO and interrupt documentation is available in the [MAX30102 datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/max30102.pdf?utm_source=chatgpt.com).

For the first prototype, use the SparkFun MAX3010x Arduino library or an equivalent driver. The firmware architecture should look like this:

```cpp
// Conceptual firmware structure.
// MAX30102 driver-specific initialization/read functions
// must be adapted to the installed sensor library.

void setup() {
    Serial.begin(921600);

    pinMode(18, OUTPUT);
    digitalWrite(18, LOW);

    initializeMAX30102();
    configureSamplingRate(100);
    configureFIFO();
}

void loop() {
    uint32_t now = micros();

    // Read every available FIFO sample.
    while (sensorDataAvailable()) {
        uint32_t sampleTime = micros();

        uint32_t red = readRed();
        uint32_t ir = readIR();

        Serial.printf(
            "PPG,%lu,%lu,%lu\n",
            sampleTime,
            red,
            ir
        );
    }

    // Generate scheduled synchronization pulses
    // using a non-blocking state machine.
    updateSynchronizationLED(now);
}
```

This is a firmware skeleton rather than a complete MAX30102 driver. The sensor initialization, FIFO handling and LED schedule need to be implemented against the specific library.

For the actual study, use a sample counter as well as the timestamp. This allows you to identify missing samples and FIFO overruns.

### 2.4 Python acquisition software

The computer will collect the serial PPG stream and save it to disk.

I recommend using a dedicated acquisition process.

```python
import serial
import csv
import time

PORT = "COM5"       # Change for your computer
BAUD = 921600

ser = serial.Serial(PORT, BAUD, timeout=1)

with open("contact_ppg.csv", "w", newline="") as f:

    writer = csv.writer(f)

    writer.writerow([
        "type",
        "timestamp_us",
        "red",
        "ir",
        "event"
    ])

    while True:
        try:
            line = ser.readline().decode(
                "utf-8",
                errors="ignore"
            ).strip()

            if not line:
                continue

            fields = line.split(",")

            if fields[0] == "PPG":
                writer.writerow([
                    "PPG",
                    fields[1],
                    fields[2],
                    fields[3],
                    ""
                ])

            elif fields[0] == "SYNC":
                writer.writerow([
                    "SYNC",
                    fields[1],
                    "",
                    "",
                    fields[-1]
                ])

        except KeyboardInterrupt:
            break

ser.close()
```

This gives you a raw contact PPG file.

For a robust implementation, add:

* Serial connection status.

* Missing-sample detection.

* Automatic file naming.

* Session ID.

* Acquisition start and stop events.

* A separate acquisition log.

Do not timestamp samples when they arrive over USB and assume those arrival times are the actual sampling times.

### 3\. Smartphone video acquisition

### 3.1 Recommended acquisition settings

I would use the following initial configuration:

| Setting            | Target                     |
| ------------------ | -------------------------- |
| Resolution         | 1920 × 1080                |
| Frame rate         | 60 FPS                     |
| Exposure           | Locked                     |
| White balance      | Locked                     |
| Focus              | Locked                     |
| ISO                | Fixed                      |
| Flash              | Disabled                   |
| Video encoding     | High-quality H.264 or HEVC |
| Recording duration | 180 seconds                |

If 60 FPS is unavailable, start with 30 FPS. It is better to have stable 30 FPS than nominal 60 FPS with many dropped frames.

The smartphone should record the synchronization LED as well as the participant's face. Position the marker near the camera, but outside the facial ROI.

### 3.2 Video acquisition metadata

For every recording, save:

```json
{
  "session_id": "S001_R001",
  "camera": "smartphone_rgb",
  "resolution": "1920x1080",
  "target_fps": 60,
  "exposure_locked": true,
  "white_balance_locked": true,
  "distance_cm": 60,
  "lighting": "controlled_white_led",
  "duration_seconds": 180,
  "reference_sensor": "MAX30102",
  "reference_sampling_rate": 100
}
```

These are example values, not measurements. Replace them with actual acquisition settings.

### 4\. Dataset structure

I strongly recommend separating raw acquisition data from processed signals.

This is important because you may improve your algorithms several times during the project. You should never need to repeat the experiment just because your processing pipeline changes.

### 4.1 Proposed directory structure

```text
RGB_PPG_PROJECT/
│
├── data/
│   │
│   ├── raw/
│   │   ├── S001/
│   │   │   ├── S001_R001.mp4
│   │   │   ├── contact_ppg.csv
│   │   │   ├── events.csv
│   │   │   └── metadata.json
│   │   │
│   │   ├── S002/
│   │   └── S003/
│   │
│   ├── processed/
│   │   ├── S001_R001/
│   │   │   ├── timestamps.npy
│   │   │   ├── rgb_forehead.npy
│   │   │   ├── rgb_left_cheek.npy
│   │   │   ├── rgb_right_cheek.npy
│   │   │   ├── green.npy
│   │   │   ├── chrom.npy
│   │   │   └── pos.npy
│   │
│   └── reconstructed/
│       ├── S001_R001/
│       │   ├── camera_ppg.npy
│       │   ├── cnn_ppg.npy
│       │   └── quality.npy
│
├── src/
│   ├── acquisition/
│   ├── synchronization/
│   ├── roi/
│   ├── extraction/
│   ├── preprocessing/
│   ├── reconstruction/
│   └── validation/
│
├── models/
│
├── experiments/
│
├── results/
│
└── requirements.txt
```

### 4.2 Required data fields

| File              | Required fields                                             |
| ----------------- | ----------------------------------------------------------- |
| Video             | Original frames and presentation timestamps                 |
| Contact PPG       | Sample counter, timestamp, raw sensor value                 |
| Events            | Synchronization LED transition timestamps                   |
| Metadata          | Camera, sensor, lighting and participant/session conditions |
| RGB traces        | Frame timestamp, ROI RGB means                              |
| Reconstructed PPG | Timestamp and reconstructed waveform                        |
| Quality           | Motion score, signal quality and missing-data indicators    |

Use pseudonymous participant IDs. Keep consent forms and identifying information separate from the research dataset.

### 5\. Complete Python processing pipeline

Now we get to the main implementation.

I would build the first version without deep learning. The first experiment must establish whether the camera signal can recover the waveform at all.

### 5.1 Install the Python environment

On your GPU computer:

```bash
conda create -n rgbppg python=3.11 -y

conda activate rgbppg

pip install numpy scipy pandas matplotlib
pip install opencv-python
pip install mediapipe
pip install pyserial
pip install neurokit2
pip install torch torchvision
pip install scikit-learn
pip install h5py
```

Check GPU availability:

```python
import torch

print("CUDA available:", torch.cuda.is_available())

if torch.cuda.is_available():
    print(torch.cuda.get_device_name(0))
```

You do not need GPU acceleration for basic rPPG extraction. GPU becomes useful when training the reconstruction network.

### 5.2 Step 1 — Extract RGB signals from video

For the first implementation, use a face-landmark-based ROI tracker.

The following code illustrates a simple OpenCV implementation using manually specified rectangular ROIs. This is useful for testing the signal pipeline before integrating automatic face tracking.

```python
import cv2
import numpy as np
import pandas as pd

video_path = "S001_R001.mp4"

cap = cv2.VideoCapture(video_path)

fps = cap.get(cv2.CAP_PROP_FPS)

# Example ROI coordinates.
# Replace with coordinates from your actual video.
rois = {
    "forehead": (500, 150, 300, 100),
    "left_cheek": (400, 350, 120, 100),
    "right_cheek": (700, 350, 120, 100)
}

records = []

frame_index = 0

while True:

    ret, frame = cap.read()

    if not ret:
        break

    timestamp = cap.get(
        cv2.CAP_PROP_POS_MSEC
    ) / 1000.0

    row = {
        "frame": frame_index,
        "timestamp": timestamp
    }

    for name, (x, y, w, h) in rois.items():

        roi = frame[y:y+h, x:x+w]

        if roi.size == 0:
            continue

        mean_bgr = roi.mean(axis=(0, 1))

        blue, green, red = mean_bgr

        row[f"{name}_R"] = red
        row[f"{name}_G"] = green
        row[f"{name}_B"] = blue

    records.append(row)

    frame_index += 1

cap.release()

df = pd.DataFrame(records)

df.to_csv("rgb_signals.csv", index=False)

print(df.head())
```

Note that `CAP_PROP_POS_MSEC` may not provide sufficiently accurate timestamps for all video formats. For final experiments, extract actual presentation timestamps using FFprobe or a timestamp-aware decoder, and preserve dropped-frame information.

For the next version, replace manually specified ROIs with MediaPipe facial landmarks.

### 5.3 Step 2 — GREEN, CHROM and POS extraction

Here is a practical starting implementation.

```python

import numpy as np
from scipy.signal import butter, sosfiltfilt

def normalize_rgb(rgb, eps=1e-8):
    """
    Normalize RGB signals over a window.
    Input shape: (N, 3)
    """

    mean = np.mean(rgb, axis=0)
    return rgb / (mean + eps) - 1.0

def green_method(rgb):
    """
    Green-channel baseline.
    """

    return rgb[:, 1]

def chrom_method(rgb):
    """
    CHROM extraction.
    """

    x = 3 * rgb[:, 0] - 2 * rgb[:, 1]

    y = (
        1.5 * rgb[:, 0]
        + rgb[:, 1]
        - 1.5 * rgb[:, 2]
    )

    alpha = np.std(x) / (np.std(y) + 1e-8)

    return x - alpha * y

def pos_method(rgb):
    """
    POS extraction.
    """

    normalized = normalize_rgb(rgb)

    r = normalized[:, 0]
    g = normalized[:, 1]
    b = normalized[:, 2]

    s1 = g - b
    s2 = -2 * r + g + b

    alpha = np.std(s1) / (np.std(s2) + 1e-8)

    return s1 + alpha * s2

def bandpass(signal, fs, low=0.5, high=5.0):

    sos = butter(
        3,
        [low, high],
        btype="bandpass",
        fs=fs,
        output="sos"
    )

    return sosfiltfilt(sos, signal)

# Example:
#
# rgb = np.column_stack([R, G, B])
#
# green = bandpass(green_method(rgb), fs)
# chrom = bandpass(chrom_method(rgb), fs)
# pos = bandpass(pos_method(rgb), fs)
```

Important implementation detail: CHROM and POS are normally calculated using overlapping temporal windows, with window-specific normalization and overlap-add reconstruction. The code above is a whole-segment baseline, not the final implementation of those methods. Implement the published windowed formulations for your final comparison.

Also, use the actual measured frame timestamps to estimate the sampling frequency. Do not assume that the requested camera frame rate is the actual sampling frequency.

### 5.4 Step 3 — Synchronize the camera and contact PPG

Your synchronization algorithm should use the LED transitions recorded in both systems.

Assume the ESP32 generates several synchronization events at times:

t_{\\mathrm{ESP32}}=\[t_1,t_2,\\ldots,t_n\]

The video processing algorithm detects those events at frame timestamps:

t_{\\mathrm{video}}=\[v_1,v_2,\\ldots,v_n\]

Fit an affine clock mapping:

t_{\\mathrm{ESP32}}=a\\,t_{\\mathrm{video}}+b

The coefficient estimates the clock offset, while accounts for clock-rate differences.

Use multiple synchronization events distributed throughout the recording. This is better than relying on a single flash at the beginning.

For final acquisition, a timestamped LED pulse sequence is preferable to a single flash.

Python synchronization implementation:

```python

import numpy as np

def fit_clock_mapping(video_events, esp_events):
    """
    Fit mapping from video timestamps to ESP32 timestamps.

    Both arrays must contain corresponding LED events.
    """

    video_events = np.asarray(video_events)
    esp_events = np.asarray(esp_events)

    if len(video_events) != len(esp_events):
        raise ValueError("Event counts do not match")

    a, b = np.polyfit(
        video_events,
        esp_events,
        1
    )

    return a, b

def map_video_time(video_time, a, b):
    return a * np.asarray(video_time) + b

# Example with illustrative timestamps:
video_events = np.array([2.0, 12.0, 22.0, 32.0])

esp_events = np.array([10.0, 20.0, 30.0, 40.0])

a, b = fit_clock_mapping(
    video_events,
    esp_events
)

print("Clock rate factor:", a)
print("Clock offset:", b)
```

For actual data, detect the LED state in a small image region around the marker. Use thresholding on brightness and identify transitions.

Do not use facial brightness to detect synchronization because facial illumination itself is part of your measurement.

### What about sensor-to-face pulse delay?

Even after clock synchronization, the finger PPG and facial rPPG pulses will not necessarily peak at exactly the same time.

There are two effects:

* Clock synchronization error.

* Physiological pulse propagation delay between facial and finger measurement sites.

Measure these separately.

For the first experiment, estimate the physiological delay on the calibration subset, then report it and evaluate residual timing errors on independent test data.

Do not silently shift each test beat until the two waveforms match. That would hide the very timing differences you need to measure.

### 5.5 Step 4 — Process the contact PPG reference

For the MAX30102 reference, use the raw red or infrared channel consistently throughout the study.

I would start with the infrared channel if the sensor provides a stable finger waveform, but verify this experimentally.

Example:

```python
import pandas as pd
import numpy as np
from scipy.signal import butter, sosfiltfilt

df = pd.read_csv("contact_ppg.csv")

ppg = df["ir"].to_numpy(dtype=float)

fs = 100  # Example configured sampling frequency

sos = butter(
    3,
    [0.5, 5.0],
    btype="bandpass",
    fs=fs,
    output="sos"
)

contact_ppg = sosfiltfilt(sos, ppg)

contact_ppg = (
    contact_ppg - np.mean(contact_ppg)
) / (np.std(contact_ppg) + 1e-8)
```

For your final system, use the sensor timestamps rather than assuming every sample is exactly 10 ms apart.

Also, retain the unfiltered raw contact waveform. It is important to compare results under more than one reasonable filtering configuration.

### 5.6 Step 5 — Waveform similarity analysis

This is the first point where you can answer your central research question experimentally.

I suggest implementing the following metrics:

```python

import numpy as np
from scipy.signal import correlate
from sklearn.metrics import mean_squared_error

def pearson_correlation(reference, estimated):
    return np.corrcoef(reference, estimated)[0, 1]

def normalized_rmse(reference, estimated):
    rmse = np.sqrt(
        mean_squared_error(reference, estimated)
    )

    return rmse / (
        np.std(reference) + 1e-8
    )

def cosine_similarity(reference, estimated):

    return np.dot(reference, estimated) / (
        np.linalg.norm(reference)
        * np.linalg.norm(estimated)
        + 1e-8
    )

def estimate_lag(reference, estimated, max_lag=None):

    reference = reference - np.mean(reference)
    estimated = estimated - np.mean(estimated)

    corr = correlate(
        reference,
        estimated,
        mode="full",
        method="fft"
    )

    lags = np.arange(
        -len(estimated) + 1,
        len(reference)
    )

    if max_lag is not None:

        valid = np.abs(lags) <= max_lag

        corr = corr[valid]
        lags = lags[valid]

    return lags[np.argmax(corr)]

def evaluate(reference, estimated):

    # Both signals must already be synchronized,
    # resampled onto the same timestamps,
    # and normalized consistently.

    return {
        "pearson": pearson_correlation(
            reference, estimated
        ),
        "nrmse": normalized_rmse(
            reference, estimated
        ),
        "cosine": cosine_similarity(
            reference, estimated
        )
    }
```

Important: correlation-based lag estimation is useful as a diagnostic, but the final primary agreement analysis must retain the independent synchronization and pre-specified physiological delay correction.

For shape analysis, normalize each beat using a pre-defined method and compare corresponding beat segments.

### 6\. The first experiment: feasibility of smartphone-based PPG reconstruction

I would make this your first formal experiment, before training any neural network.

Experiment 01

Title: Feasibility Assessment of Contact PPG Waveform Recovery Using Smartphone RGB Video.

### 6.1 Experimental objective

Determine whether facial RGB video contains sufficient pulsatile information to reconstruct a continuous waveform that resembles a simultaneously recorded contact PPG signal.

### 6.2 Study protocol

Start with 10 participants for the pilot.

Each participant completes:

| Step | Activity                                   | Duration |
| ---- | ------------------------------------------ | -------- |
| 1    | Sit comfortably and rest                   | 5 min    |
| 2    | Attach finger PPG sensor                   | 1 min    |
| 3    | Position smartphone and stabilize lighting | 1 min    |
| 4    | Record synchronized resting video and PPG  | 3 min    |
| 5    | Check signal quality and synchronization   | 1 min    |

Total recording time is approximately 11 minutes per participant, excluding setup and breaks.

For the initial experiment, use only stationary resting recordings.

Why?

Because you first need to establish whether the optical method works under favorable conditions. Adding motion and changing illumination immediately makes it difficult to identify the cause of poor waveform reconstruction.

### 6.3 Experimental variables

| Type        | Variable                   |
| ----------- | -------------------------- |
| Independent | Extraction algorithm       |
| Independent | Facial ROI                 |
| Dependent   | Waveform correlation       |
| Dependent   | NRMSE                      |
| Dependent   | Systolic peak timing error |
| Dependent   | Beat detection agreement   |
| Controlled  | Camera distance            |
| Controlled  | Frame rate                 |
| Controlled  | Exposure                   |
| Controlled  | LED illumination           |
| Controlled  | Participant posture        |

### 6.4 Experimental groups

Run these combinations:

| Experiment | ROI                 | Algorithm            |
| ---------- | ------------------- | -------------------- |
| E01        | Forehead            | GREEN                |
| E02        | Forehead            | CHROM                |
| E03        | Forehead            | POS                  |
| E04        | Left cheek          | GREEN                |
| E05        | Left cheek          | CHROM                |
| E06        | Left cheek          | POS                  |
| E07        | Right cheek         | GREEN                |
| E08        | Right cheek         | CHROM                |
| E09        | Right cheek         | POS                  |
| E10        | Combined facial ROI | Best baseline method |

This will tell you whether the location of the camera measurement matters.

### 6.5 Expected figures for your research paper

I would prepare these six figures from the first experiment.

Figure 1 — Experimental setup

![SympCam: Remote Optical Measurement of Sympathetic Arousal · Sensing, Perception & Interaction Lab](https://images.openai.com/static-rsc-4/w3d1Rx0cS7lEPLI64cZJam-5QOq5dxH1-THD-IJvyI1t4dlUryMECKkI8T538gh4ddkv74SPrTvjWWQGPnpOTrdw50R2O_5GHhnDMiIm7wMASC_DmxbZJsiS3o2GD-EHs0FjSR5ZV4l6Ws8A6-SLlbQYPPs97fcEavRuL5k9YirD0mI3rf_AJ6aSVGpCRVP2?purpose=fullsize)

Show the smartphone, illumination, facial ROI and contact PPG sensor.

Figure 2 — RGB channel signals

![Effectiveness of Remote PPG Construction Methods: A Preliminary Analysis | MDPI](https://images.openai.com/static-rsc-4/Ft8WcVkJ718Ut1z4qmb5GV1g-ogO3IfIzz-p11cIkYyBd7quJoo8tuCJae61-pU5XXvOa69mWPdAemKtESIVxf_pAcqJJgNm-qya97SPjwJwbGL4A386ITa8gTZlDEED7odt1e5BNqnrl5BOLUAex5FYgF2ALLs-Znl66_tgSK1RhxbalHAS7Grzj8qgVdXb?purpose=fullsize)

Plot the R, G and B intensity variations over time.

Figure 3 — Algorithm comparison

![A machine learning-based approach for constructing remote photoplethysmogram signals from video cameras | Communications Medicine](https://images.openai.com/static-rsc-4/_KVs4pz0Pc83p6KNy6HeQag1VAJjRIX-OB07qXmc5wCPkOr-1EgMmcgpXZyUHzX5IKVom1AnYowXHb2eMbDG4D21eiA4XCunyofXxNxyv7hlKP0HdRH6V2TUhZcKG5XTsaUCI5xjhlcA8B8VdGQ80Jv8Npy-66adKVxJ_9EHJjY2ZeBllWKsuBrb5vbdeEmd?purpose=fullsize)

Compare GREEN, CHROM and POS outputs.

Figure 4 — Contact versus camera PPG

![Rice University Researchers Develop a New Camera-Based, Touch-Free Technology for Measuring Vital Signs](https://images.openai.com/static-rsc-4/oIEiwJD34DfNIPf--b7DpncciAaoJYdH-TnyK6U_i74i_sMRNwIDd4zrDA9y0fj_7d3QvxZ3x__JVSEsDN_q93RQjuTfBO4BOiWQ3rdEpWcnXZBkkgCoUtFENuiwvugUwKC7Xnw3uoWjFiUcMYWUmAX1AYhcxHf9vM4Dvx84OWjRA1MbOoJ6weP4sZ8x2xso?purpose=fullsize)

The most important figure: simultaneous reference and camera waveforms.

Figure 5 — Beat morphology comparison

![Photoplethysmography Signal Processing and Synthesis | Peter Charlton](https://images.openai.com/static-rsc-4/jv8hByVp-sj1zl8AWScnOCo2KVohW8OMug2UeMoQjgXcM_kql6RCfMZn4ZTzqg6BLP_lbRkOPWkhnxJetHR4e9-jj7SJsgqEE58Jcjl8ibb5tfy4EMcVYhbYrF8bUEs_-u2ajfSDv0dLk4OB_vCbICD_bYsbwsG_gVaPNpoYxPqwIr9YN4JzMN_YL6o6bOSQ?purpose=fullsize)

Show individual beat shapes and their characteristic features.

Figure 6 — Statistical agreement

![Bland-Altmanプロット ジェネレーター｜CSV・Excel研究グラフ｜SciDraw](https://images.openai.com/static-rsc-4/0774HhuYpp_Umjk0nmIo_L1YwFuE6LzHRfY8IAMmm9VHyTKbnXyTjv7WyOJGwLTVgeGOXgc6Rh2WaSwvg9APguxA7ygdg0WJBLY6Xvs1uZed6VuvX9avQORlYNCEpbFwHz2gtYwYEZQzaF1xpVKgbyDwKcGU16YTNrhLiEZcoXIuECfklsSb6ZOjAvn0-Sp6?purpose=fullsize)

Report beat-level timing and morphology agreement with confidence intervals.

These are figure concepts, not experimental results.

### 7\. How to decide whether Experiment 01 is successful

I recommend defining your acceptance criteria before running the experiment.

Do not select the best algorithm simply because it produces the highest correlation on the entire dataset.

Use participant-level train/validation/test partitions, and report subject-level distributions.

Here is a proposed feasibility framework:

| Evaluation           | What you want to establish                               |
| -------------------- | -------------------------------------------------------- |
| Pulse frequency      | Camera signal contains a cardiac-frequency component     |
| Beat detection       | Camera beats correspond to reference beats               |
| Waveform correlation | Camera signal resembles contact PPG                      |
| Systolic peak        | Principal waveform morphology is recoverable             |
| Dicrotic notch       | Secondary morphology can be recovered where identifiable |
| Repeatability        | Similar results across participants and recordings       |

I would use three outcome categories:

* Promising: Consistent pulse extraction and reproducible waveform morphology across participants.

* Partially successful: Heartbeat timing is recovered, but detailed morphology is unreliable.

* Unsuccessful: Camera signals do not reliably preserve pulse-related information under the controlled conditions.

Do not make dicrotic notch recovery a mandatory success criterion for the initial 30 FPS experiment. It may be beyond the temporal resolution of your camera.

### 8\. Experiment 02 — Deep learning reconstruction

Only proceed to this stage once Experiment 01 demonstrates meaningful correspondence between the camera and contact signals.

### 8.1 Training dataset

Each training example should contain paired time-series segments:

Input: RGB-derived signal

X=\[GREEN,CHROM,POS\]

Example: 600 frames at 60 FPS = 10 seconds

1D CNN / Temporal U-Net

Target: Contact PPG

Y=\[y_1,y_2,\\ldots,y_N\]

Corresponding reference waveform resampled onto the camera time grid

I recommend initially training on 10-second windows with 50% overlap.

However, make sure adjacent windows from the same participant cannot cross training and testing boundaries.

### 8.2 A recommended reconstruction model

Start with this model:

| Layer          | Configuration                 |
| -------------- | ----------------------------- |
| Input          | 3-channel RGB-derived signals |
| Conv1D         | 32 filters                    |
| Residual block | 64 filters                    |
| Residual block | 128 filters                   |
| Residual block | 64 filters                    |
| Conv1D         | 1 output channel              |
| Output         | Reconstructed PPG             |

Train with a combination of:

* Normalized waveform loss.

* First-derivative loss.

* Spectral loss.

* Beat morphology loss.

Use AdamW, early stopping and subject-independent validation.

An important design decision: the model should not receive the contact PPG during inference. Contact PPG is only a training target and evaluation reference.

### 8.3 Important reconstruction experiment

Compare four systems:

| Model | Input                 | Output                |
| ----- | --------------------- | --------------------- |
| M1    | GREEN                 | Filtered rPPG         |
| M2    | CHROM/POS             | Filtered rPPG         |
| M3    | Best baseline         | CNN reconstructed PPG |
| M4    | Combined RGB features | CNN reconstructed PPG |

The primary question is:

Does M3 or M4 improve waveform morphology over M1 and M2 on participants never seen during training?

If not, the complexity of deep learning may not be justified.

### 9\. Quality control and common experimental failures

I would add automatic quality monitoring to your acquisition application.

| Problem                     | Detection                   | Response                            |
| --------------------------- | --------------------------- | ----------------------------------- |
| Face movement               | Landmark displacement       | Flag affected interval              |
| Lighting change             | RGB baseline jump           | Flag affected interval              |
| Frame drops                 | Timestamp gaps              | Preserve gaps; do not invent frames |
| Sensor saturation           | Flat contact PPG            | Repeat acquisition                  |
| Finger movement             | Reference signal distortion | Flag interval                       |
| LED synchronization failure | Missing event               | Reject or reacquire session         |
| Low pulse SNR               | Spectral quality analysis   | Mark low confidence                 |

One particularly important point: do not interpolate long missing video segments and then treat the resulting signal as real measured PPG.

Your quality-control system should distinguish actual measurements from reconstructed or missing data.

Also, facial rPPG and finger PPG should not be assumed to have equal amplitudes. Use amplitude normalization for shape comparisons, but preserve separate raw-amplitude analyses.

### 10\. Final project milestones

Here is the order I would follow in practice.

### Implementation checklist

0 of 14 completed

0%

Acquire smartphone and lock camera settings

Hardware

Build MAX30102 and ESP32 acquisition circuit

Hardware

Implement raw PPG recording in Python

Acquisition

Implement LED synchronization

Acquisition

Record one 3-minute pilot session

Acquisition

Extract actual video timestamps

Processing

Implement facial ROI extraction

Processing

Implement GREEN, CHROM and POS

Processing

Synchronize camera and contact PPG

Processing

Generate waveform comparison plots

Validation

Complete the 10-participant pilot

Validation

Evaluate feasibility and finalize protocol

Analysis

Train subject-independent CNN

Deep learning

Conduct independent test and statistical analysis

Final validation

### 11\. My strongest recommendation for your research

I would make the first experimental result a direct comparison of three signals:

Signal 1

Contact PPG

Your conventional finger-sensor reference.

Signal 2

Raw camera PPG

Extracted using GREEN, CHROM or POS.

Signal 3

Reconstructed camera PPG

Output of your reconstruction algorithm.

Your eventual research paper should show all three signals on the same time axis, together with an enlarged view of several individual beats.

This will make the research contribution immediately understandable.

There is one limitation I want to emphasize: a smartphone camera does not measure the same optical quantity as a finger sensor, and the face and finger have different vascular beds. Therefore, your claim should initially be reconstruction of a contact-PPG-like waveform, not exact recovery of the original finger PPG.

If you eventually demonstrate reliable morphological agreement across independent participants and recording conditions, that would be a meaningful research result.

### 12\. What I would build first

My suggested first deliverable is a small Python application that takes:

* `video.mp4`

* `contact_ppg.csv`

* `events.csv`

And automatically produces:

### Expected software output

01_rgb_channels.png

R/G/B

02_extracted_rppg.png

GREEN / CHROM / POS

03_contact_vs_camera.png

Waveforms

04_morphology_comparison.png

Beat analysis

05_metrics.csv

Statistics

This is the first software milestone I would complete before spending time on neural-network development.

One final hardware consideration: If you can choose the smartphone, prioritize one that supports true 60 FPS video with locked exposure and accessible original frame timestamps. This will be more valuable to your waveform research than simply purchasing a smartphone with a higher megapixel count.
