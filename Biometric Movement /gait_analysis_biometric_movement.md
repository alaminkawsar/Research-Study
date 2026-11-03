### Deep research: Gait analysis & biometric movement datasets

There are several major categories of publicly available gait and human movement datasets. The best choice depends on whether your research focuses on biometric identification, gait recognition, clinical gait assessment, human movement analysis, or AI-based movement classification.

I have identified research datasets, academic repositories, clinical datasets, and multimodal sensor databases. Below is a curated starting list, prioritizing datasets with actual downloadable data and useful research documentation.

### 1\. Major gait and biometric recognition datasets

These are particularly relevant to computer vision, machine learning, deep learning, and identifying individuals through their walking patterns.

| Dataset   | Scale                                       | Data type                                               | Best application                  |
| --------- | ------------------------------------------- | ------------------------------------------------------- | --------------------------------- |
| CASIA-B   | 124 subjects                                | Silhouettes, 11 views, clothing and carrying variations | Gait identification               |
| OU-ISIR   | Up to 10,307 subjects in multi-view dataset | Video, silhouettes, gait sequences                      | Large-scale biometrics            |
| GREW      | 26,345 identities                           | Silhouettes, optical flow, 2D/3D keypoints              | Real-world gait recognition       |
| Gait3D    | 4,000 subjects, 25,000+ sequences           | 2D silhouettes, 3D SMPL meshes, keypoints               | 3D gait biometrics                |
| SUSTech1K | 1,050 subjects, 25,239 sequences            | Video-based gait sequences                              | Cross-view recognition            |
| CCPG      | 200 identities, 16,000+ sequences           | Indoor/outdoor video                                    | Clothing-invariant identification |

Sources and dataset access:

* [IAPR TC4 – Gait Dataset Directory](https://iapr-tc4.org/gait-datasets/?utm_source=chatgpt.com) — excellent index of established and newer datasets. IAPR TC4 +1

* [CASIA Gait Database – NIST catalog](https://tsapps.nist.gov/BDbC/Search/Details/574?utm_source=chatgpt.com) — documentation of CASIA-A, B and C. Biometrics Research Database Catalog

* [OU-ISIR – Osaka University](http://www.am.sanken.osaka-u.ac.jp/BiometricDB/?utm_source=chatgpt.com) — official database portal. Biometrics Research Database Catalog +1

* [GREW – ICCV 2021 paper](https://openaccess.thecvf.com/content/ICCV2021/html/Zhu_Gait_Recognition_in_the_Wild_A_Benchmark_ICCV_2021_paper.html?utm_source=chatgpt.com) — research benchmark and methodology. Open Access CVF

* [Gait3D – official project](https://gait3d.github.io/?utm_source=chatgpt.com) — 3D gait representation and recognition. Open Access CVF +1

Important: Some large-scale biometric datasets require academic registration, research-purpose approval, or acceptance of usage terms. A paper being open access does not necessarily mean its raw dataset is unrestricted.

### 2\. Wearable biometric movement datasets (IMU, accelerometer, gyroscope)

These are particularly valuable if you want to develop systems that identify or characterize individuals using their movement signatures rather than cameras.

![A multi-level annotated sensor dataset of gait freezing manifestations and severity in Parkinson’s disease | Scientific Data](https://images.openai.com/static-rsc-4/-_jo7SAfuyMaxCK8-7WqLurjhE8zuOtgr8mxVrBV_N4F9HG_kfz0EOeVfUKZ43awD5ctDmJZOGu26oFcW2YE5dVRvYBtKbxwirep5BBtKuZdxbLYAoYQ8br3zW5W8DDwyFdo0f-NVAMPDy1Q6_tdboXCw1c9WvVllc7qztQZOOmfjeBvjxJQOUe0Qg85BGCL?purpose=fullsize)

1\. Smartphone-based unconditioned gait identification (2026)

Highly relevant to biometrics

* 390 participants

* 3,900 walking recordings

* Accelerometer, gyroscope and magnetometer

* 30 Hz sampling

* Nine sensor channels

[Research paper and dataset](https://www.frontiersin.org/journals/computer-science/articles/10.3389/fcomp.2026.1752141/full?utm_source=chatgpt.com) Frontiers

![Placement of markers and IMU sensors. Each IMU sensor was mounted on... | Download Scientific Diagram](https://images.openai.com/static-rsc-4/zR7ylzZHIsQud7aezhVMfRbUiurzKlQSrpvDh2aSg13fg-z8hUGOmoEKxDylhDifByphKsIBuhXnLjzM_3r6RNnGq6nZwkUFxv_XdQJKVJgjy9iBTzg7cDcqujvll6WHhcNWik8jTCCJ4KN_ezQ5K6KWgnWyK-F2zUyHkZaMvvTCjsdLzf-b8dSjW6XSgzdz?purpose=fullsize)

2\. Clinical Gait Signals Dataset (2025)

* 260 participants

* 1,356 gait trials

* Four IMUs on head, lower back and feet

* More than 11 hours of gait recordings

* Healthy, neurological and orthopedic cohorts

[Dataset record and access information](https://datasetcatalog.nlm.nih.gov/dataset?q=0001203950&utm_source=chatgpt.com) Dataset Catalog +1

![A Dataset of Clinical Gait Signals with Wearable Sensors from Healthy, Neurological, and Orthopedic Cohorts | Scientific Data](https://images.openai.com/static-rsc-4/3xyDmQ9kFG2ugUThqvuL37j70FLdMxvUjd2dBRA3XpbL0Jj8BMgwF3_nEKkXxDz2FNwJ203n7ZxlWpUunKAprEdCs2nHtbMQgFRVKlCiZK_2YNI1_nV_XkkQAVjyi5RXYmesXSCScWpryQ438SxLfovonteGMZgOlisNsm6YqF4DBJUl9_7v4h0BbtxlgXSo?purpose=fullsize)

3\. Real-world uneven-surface gait dataset

* 30 participants

* Six wearable IMUs

* Nine outdoor walking conditions

* Stairs, slopes, grass and uneven surfaces

* Useful for robust movement classification

[Open research paper and data](https://pmc.ncbi.nlm.nih.gov/articles/PMC7343872/?utm_source=chatgpt.com) PMC

![WearGait-PD: An Open-Access Wearables Dataset for Gait in Parkinson’s Disease and Age-Matched Controls | Scientific Data](https://images.openai.com/static-rsc-4/cT8x45vCTQbvkpF_oM7frbdxDX8U9gTtsGUmf84ROHrnd3LAygOwe31iOrJdF8x-RrLon_h77zxtzwW7tIMjWYMoIfLKxSOVHEnMIjvxpj-k4sQSlhRkfj37nPKXXuGcwn6g1jZTC3nDKKMIuDO6SpgSbP0YCiQ8ZjLxgw0yVbV0H6CCiCfZrVNjrHIB3w4F?purpose=fullsize)

4\. WearGait-PD (2026)

* 100 people with Parkinson's disease

* 85 age-matched controls

* 13 wearable IMU sensors

* Sensorized insoles

* Synchronized reference walkway measurements

[Open-access dataset paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC13009270/?utm_source=chatgpt.com) PMC

![Movement Laboratory | Metropolia UAS](https://images.openai.com/static-rsc-4/TYANSNVfDI4Ap_UlXdwAMFjTw4hsCS3va-gucs-HeZNOj2t4ragCOODRbaPXRwZrCEStWUc31Ez0CsZ0NMWX2Q3sDzBr-EeaC2rwUQ6f03RQnCul-c1z8LyjzNiZkIQtuFNnW9orIRmEKVeuYVGDnf69HJNPDQhhtvNwND5bL3P7weh9dAmzXM8jEMF6hpWc?purpose=fullsize)

5\. FDA Open-Access Wearables Gait Dataset

* Smartphone IMU measurements

* Reference Xsens IMUs

* Pressure-sensing walkway

* Different phone positions and orientations

* Useful for sensor validation and gait metrics

[FDA dataset resource](https://www.fda.gov/medical-devices/regulatory-science-tools-catalog/open-access-wearables-dataset-evaluate-factors-impacting-accuracy-smartphone-gait-metrics?utm_source=chatgpt.com) FDA

### 3\. Multimodal biomechanics and movement datasets

These are useful if you need more than walking identification—for example, joint angles, muscle activation, body posture, force distribution and full-body kinematics.

| Dataset                          | Participants / scale | Available measurements                      |
| -------------------------------- | -------------------- | ------------------------------------------- |
| NONSD-Gait (2025)                | 23                   | MoCap, depth camera, IMU, 3D joints         |
| Multimodal Gait PhysioNet (2026) | 59                   | EEG, EMG, IMU, force plates, kinematics     |
| GAITEX (2025)                    | 19                   | Nine IMUs, 68 markers, OpenSim models       |
| Asymptomatic Human Gait (2023)   | Study cohort         | Markers, IMUs, insoles, force plates        |
| AddBiomechanics                  | 461 participants     | 8,139 trials, MoCap, ground reaction forces |
| Wearable Motion Capture (2026)   | 10                   | IMUs, egocentric video, joint angles        |

Research links:

* [NONSD-Gait – Dryad download](https://datadryad.org/dataset/doi:10.5061/dryad.2rbnzs7z3?utm_source=chatgpt.com). Scientific Data +1

* [Multimodal Gait Dataset – PhysioNet](https://physionet.org/content/multimodal-gait-dataset/1.0.0/?utm_source=chatgpt.com). PhysioNet

* [GAITEX – Scientific Data](https://www.nature.com/articles/s41597-025-06439-x?utm_source=chatgpt.com). Scientific Data

* [Asymptomatic Human Gait – Scientific Data](https://www.nature.com/articles/s41597-023-02077-3?utm_source=chatgpt.com). Scientific Data

* [AddBiomechanics – Stanford FAIR Center](https://faircenter.stanford.edu/resources/datasets/?utm_source=chatgpt.com). faircenter.stanford.edu

* [Wearable Motion Capture – Scientific Data (2026)](https://www.nature.com/articles/s41597-026-07657-7?utm_source=chatgpt.com). Scientific Data

### 4\. Best research repositories for discovering additional datasets

These directories are especially useful for finding datasets beyond the famous benchmarks.

| Repository           | What to search for                    | Link                    |
| -------------------- | ------------------------------------- | ----------------------- |
| JMNS Dataset Library | 296 verified gait datasets            | Browse gait datasets    |
| PhysioNet            | Clinical gait, EEG, EMG, IMU          | PhysioNet               |
| Dryad                | Biomechanics and movement recordings  | Dryad                   |
| Zenodo               | IMU, MoCap, human movement            | Zenodo                  |
| Figshare             | Gait signals and sensor datasets      | Figshare                |
| IEEE Biometrics      | Gait and forensic biometric databases | IEEE database directory |
| Stanford FAIR Center | Large-scale biomechanics datasets     | Stanford datasets       |

The JMNS library is particularly interesting: it reports 296 gait datasets, 11,621 participants, 121 wearable/IMU datasets and 174 motion-capture/kinematics datasets. JMNS

### 5\. My research recommendations

Depending on your research objective, I would prioritize:

| Research objective                   | Recommended starting datasets          |
| ------------------------------------ | -------------------------------------- |
| Gait-based individual identification | CASIA-B, GREW, OU-ISIR                 |
| Deep learning gait recognition       | GREW, Gait3D, SUSTech1K                |
| Smartphone gait biometrics           | 2026 Smartphone Gait Identification    |
| Wearable biometric authentication    | Smartphone Gait, Clinical Gait Signals |
| Clinical gait abnormality detection  | WearGait-PD, GAITEX                    |
| Joint-angle prediction               | NONSD-Gait, Wearable Motion Capture    |
| Full-body movement analysis          | AddBiomechanics, PhysioNet             |
| Sensor fusion                        | NONSD-Gait, Multimodal Gait PhysioNet  |

One important research distinction: Gait biometrics can mean identifying who a person is from their walking pattern, whereas gait analysis can mean measuring how a person moves. These require different labels, evaluation protocols and datasets.

### 6\. Let's narrow the research to your intended application

I can take this further and build a much more targeted dataset catalogue, including download links, dataset size, file formats, sensor specifications, participant demographics, labels, licenses, publications and access restrictions.

Which research direction are you interested in?

1\. Primary research objective

Gait biometrics / human identification

Clinical gait analysis / disease detection

Human movement recognition / activity classification

Biomechanics / joint kinematics

AI-based gait prediction

All of the above

2\. Preferred data modality

All modalities

Video / RGB / silhouette

IMU / accelerometer / gyroscope

3D skeleton / pose estimation

Motion capture / force plates / EMG

Multimodal sensor fusion

3\. Dataset access

Free and publicly downloadable

Free or academic registration

Include commercial and restricted datasets

4\. Preferred dataset scale

Large-scale datasets preferred

Any dataset size

Small datasets with rich biometric measurements

Start targeted deep research

My recommendation is to investigate gait biometrics combined with wearable IMU data and video-based gait recognition. This offers a particularly interesting research direction for AI-based human movement identification.
