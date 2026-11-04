# Heart Sound (PCG) Dataset Resources for Disease-Specific Classification

**Prepared:** 2026-11-05\
**Goal:** Multiclass classification from WAV phonocardiograms (PCG),
especially congenital heart disease (ASD, VSD, PDA) and valvular
disease.

> **Critical distinction:** "Murmur present" or "abnormal" is not
> equivalent to a confirmed diagnosis. Use clinically confirmed disease
> labels for disease-specific training. Keep diagnosis labels and
> acoustic phenotype labels in separate columns.

## 1. Best disease-labelled WAV resources

### 1.1 BUET Multi-disease Heart Sound (BMD-HS) --- start here

-   **GitHub repository / files:**
    https://github.com/sani002/BMD-HS-Dataset
-   **README:** https://github.com/sani002/BMD-HS-Dataset#readme
-   **Paper:** Ali et al. (2024), *BUET Multi-disease Heart Sound
    Dataset: A Comprehensive Auscultation Dataset for Developing
    Computer-Aided Diagnostic Systems*, arXiv:2409.00724 ---
    https://arxiv.org/abs/2409.00724
-   **Format:** Repository README reports 872 WAV recordings, 20 seconds
    each, sampled at 4 kHz.
-   **Cohort:** 59 patients, recorded at 8 auscultation positions (as
    described in the repository).
-   **Labels:** Aortic stenosis (AS), aortic regurgitation (AR), mitral
    regurgitation (MR), mitral stenosis (MS), multi-disease (MD), and
    normal.
-   **Annotations:** Patient-level CSV labels and additional metadata
    are provided.
-   **Why useful:** This is a directly relevant multi-valvular dataset
    collected at the National Institute of Cardiovascular Diseases in
    Dhaka.
-   **Important checks:** Inspect the CSV and metadata before training.
    The repository describes MD as a multi-disease label; do not assume
    it specifies every disease combination unless the supplied metadata
    does. Confirm the repository license and citation requirements
    before reuse.

### 1.2 Heart sound regurgitation dataset (2025) --- strong clinical labels

-   **Direct data download (Mendeley Data):**
    https://data.mendeley.com/datasets/jfbdvjw6sf/1
-   **Paper:** *A dataset of heart sound regurgitation of patients with
    heart valve disorders*, Data in Brief (2025), 63, 112081.
-   **DOI:** https://doi.org/10.1016/j.dib.2025.112081
-   **Open full text:**
    https://pmc.ncbi.nlm.nih.gov/articles/PMC12504997/
-   **PubMed:** https://pubmed.ncbi.nlm.nih.gov/41070265/
-   **Format:** WAV, raw and filtered audio.
-   **Labels:** Aortic regurgitation (AR), mitral regurgitation (MR),
    tricuspid regurgitation (TR), and healthy/normal.
-   **Clinical grounding:** The paper says diagnoses were confirmed by
    an experienced cardiologist and participants were assessed using
    echocardiography. Metadata includes age, sex, regurgitation type,
    echocardiographic grade, and recording location.
-   **Use:** A valuable disease-specific source for regurgitation
    classification.
-   **License/access:** Check the Mendeley Data landing page for the
    current license, version, and download files.

## 2. Congenital heart disease (ASD, VSD, PDA)

### 2.1 Teaching Heart Auscultation --- congenital heart sound cases

-   **Download page:**
    https://teachingheartauscultation.com/heart-sounds-mp3-downloads
-   **Listed congenital cases include:** ASD, pulmonary stenosis, PDA,
    aortic stenosis/regurgitation, normal, bicuspid aortic valve,
    innocent murmur/S3, and VSD.
-   **Format:** MP3, not WAV.
-   **Use:** Supplementary listening examples, educational reference, or
    qualitative testing---not a substitute for a large clinical cohort.
-   **Caveats:** This is a teaching collection, not a balanced
    patient-level research cohort. Confirm provenance, terms, and
    permission for machine-learning use. Convert to WAV only if
    permitted, and retain the original MP3.

### 2.2 CHD-HSY / other ASD-VSD-PDA datasets --- verify before relying on them

A previously circulated reference to a "CHD-HSY" dataset with ASD, VSD,
and PDA labels could not be independently verified to a primary dataset
page and paper in this search. Do not rely on an unverified dataset name
or quoted sample count. Search for the original publication and
repository using: - `"CHD-HSY" heart sound dataset` -
`"ASD" "VSD" "PDA" phonocardiogram dataset` -
`"congenital heart disease" PCG dataset WAV`

For a thesis or paper, only include such a resource after confirming the
original source, clinical label definitions, audio files, patient
counts, and license.

## 3. Useful WAV benchmarks (not disease-specific)

### 3.1 CirCor DigiScope Phonocardiogram Dataset

-   **Download / PhysioNet:**
    https://physionet.org/content/circor-heart-sound/1.0.1/
-   **DOI:** https://doi.org/10.13026/7bkn-d780
-   **Original paper:** Oliveira et al. (2021), *The CirCor DigiScope
    Dataset: From Murmur Detection to Murmur Classification*, IEEE
    Journal of Biomedical and Health Informatics.
    https://doi.org/10.1109/JBHI.2021.3137048
-   **Format:** WAV plus CSV metadata and annotations.
-   **Population:** Pediatric.
-   **Labels:** Murmur presence/absence/unknown and murmur attributes
    such as timing, shape, pitch, quality, grade, and auscultation
    location; clinical outcome information is also included.
-   **Use:** Pediatric murmur detection and characterization.
-   **Caveat:** Murmur labels do not automatically establish ASD, VSD,
    or PDA for each recording. Read the outcome/diagnosis fields and
    their definitions before assigning disease classes.

### 3.2 PhysioNet / Computing in Cardiology Challenge 2016

-   **Download:** https://physionet.org/content/challenge-2016/1.0.0/
-   **Challenge page:** https://moody-challenge.physionet.org/2016/
-   **Original paper:** Liu et al. (2016), *An open access database for
    the evaluation of heart sound algorithms*, Physiological
    Measurement, 37(12), 2181--2213.
    https://doi.org/10.1088/0967-3334/37/12/2181
-   **Format:** WAV, resampled to 2 kHz.
-   **Labels:** Normal, abnormal, and unsure / signal-quality
    annotations.
-   **Conditions mentioned in documentation:** Mitral valve prolapse,
    mitral regurgitation, aortic stenosis, and valvular surgery occur
    among abnormal cases.
-   **Critical caveat:** The dataset explicitly does not provide
    specific disease labels for abnormal recordings. Use it for binary
    normal/abnormal benchmarking, not disease-level multiclass training.

### 3.3 PASCAL Classifying Heart Sounds Challenge

-   **Starting point:** https://www.peterjbentley.com/heartchallenge/
-   **Commonly reported classes:** Normal, murmur, extrasystole, and
    artifact.
-   **Format/access:** Verify the currently available archive and actual
    audio format at the original resource.
-   **Use:** Sound-phenotype classification and external benchmarking.
-   **Caveat:** These are acoustic categories, not confirmed diagnoses
    such as ASD or aortic stenosis.

## 4. Other educational audio reference

### Heart Sound Library

-   **Resource:**
    https://www.llmsfordoctors.com/education/semantic-qualifiers/sounds/
-   **Listed categories include:** ASD, VSD, PDA, aortic stenosis,
    aortic regurgitation, mitral regurgitation, mitral stenosis,
    tricuspid regurgitation, and others.
-   **Description:** Narrated teaching recordings, including recordings
    from a patient-simulator teaching collection.
-   **Use:** Educational/qualitative reference only unless clinical
    provenance and labels are verified.
-   **Caveat:** Confirm format, access rights, and whether a sound is a
    simulator recording or a patient recording before using it for model
    training.

## 5. At-a-glance suitability

  ------------------------------------------------------------------------------
  Dataset                         WAV?          Disease labels? Recommended role
  --------------- -------------------- ------------------------ ----------------
  BMD-HS                  Yes, 872 WAV      AS, AR, MR, MS, MD, Primary
                              reported                   normal multi-valvular
                                                                candidate

  Regurgitation                    Yes       AR, MR, TR, normal Primary
  2025                                                          regurgitation
                                                                candidate

  CirCor                           Yes  Murmur annotations; not Pediatric murmur
                                        specific CHD labels for benchmark
                                                   every record 

  PhysioNet 2016                   Yes                      No; Binary benchmark
                                         normal/abnormal/unsure 

  Teaching Heart                   MP3      Case-level teaching Supplementary
  Auscultation                                        diagnoses ASD/VSD/PDA
  CHD cases                                                     examples

  PASCAL                        Verify         Acoustic classes Sound-pattern
                                                                benchmark

  Heart Sound                   Verify      Teaching categories Educational
  Library                                                       reference
  ------------------------------------------------------------------------------

## 6. Recommended research workflow

1.  **Audit each download:** Record source URL, access date, version,
    license, checksum, number of patients, number of recordings, file
    extensions, sample rates, and label definitions.
2.  **Create a patient-level manifest:** Suggested fields:
    `dataset, patient_id, recording_id, filepath, sample_rate, duration_sec, auscultation_site, diagnosis_label, murmur_label, severity, label_source, split`.
3.  **Separate diagnosis from phenotype:** For example, `diagnosis=VSD`
    and `murmur_present=yes` are distinct variables.
4.  **Split by patient:** Never put recordings from the same patient
    into both train and test sets. This is essential when a patient has
    recordings from multiple chest positions.
5.  **Do not invent disease labels:** Never map generic "abnormal" to a
    specific disease. Do not infer ASD/VSD/PDA solely from a murmur
    class.
6.  **Harmonize audio:** Preserve originals. Create processed copies at
    a common sample rate only after documenting anti-alias filtering,
    resampling, normalization, segmentation, and channel handling.
7.  **Address class imbalance:** Report both patient and recording
    counts per class; consider class-weighted loss and training-only
    resampling.
8.  **Evaluate at patient level:** Report per-class sensitivity,
    specificity, macro-F1, balanced accuracy, confusion matrix, and
    confidence intervals. Use external validation only after checking
    label compatibility.
9.  **Respect dataset terms:** Publicly accessible does not mean
    unrestricted redistribution or unrestricted use. Follow licenses and
    cite original papers.

## 7. Suggested project directory

``` text
heart-sound-disease-research/
├── README.md
├── data/
│   ├── raw/
│   │   ├── BMD-HS/
│   │   ├── regurgitation-2025/
│   │   ├── CirCor/
│   │   ├── PhysioNet-2016/
│   │   └── CHD-teaching-MP3/
│   ├── processed/
│   └── manifests/
│       └── master_manifest.csv
├── notebooks/
├── src/
├── models/
└── reports/
```

Do not commit restricted or large audio files to a public Git
repository. Keep raw data read-only and version-control only scripts,
manifests (without sensitive patient data), and acquisition notes.

## 8. Key references

1.  Ali, S. N. et al. (2024). *BUET Multi-disease Heart Sound Dataset: A
    Comprehensive Auscultation Dataset for Developing Computer-Aided
    Diagnostic Systems.* arXiv:2409.00724.
    https://arxiv.org/abs/2409.00724
2.  *A dataset of heart sound regurgitation of patients with heart valve
    disorders* (2025). Data in Brief, 63, 112081.
    https://doi.org/10.1016/j.dib.2025.112081
3.  Oliveira, J. et al. (2021). *The CirCor DigiScope Dataset: From
    Murmur Detection to Murmur Classification.*
    https://doi.org/10.1109/JBHI.2021.3137048
4.  Liu, C. et al. (2016). *An open access database for the evaluation
    of heart sound algorithms.*
    https://doi.org/10.1088/0967-3334/37/12/2181
5.  Teaching Heart Auscultation. *Heart Sounds MP3 Downloads.*
    https://teachingheartauscultation.com/heart-sounds-mp3-downloads

## 9. Practical starting recommendation

Start by downloading **BMD-HS** and the **2025 regurgitation dataset**:
they offer the clearest disease-specific WAV labels found in this
search. Add **CirCor** for pediatric murmur research and **PhysioNet
2016** for binary benchmarking. For ASD/VSD/PDA, the located teaching
resource is MP3 and should be treated as supplementary---not as a
replacement for a clinically labelled, patient-level cohort.

This README is a curated research starting point, not a guarantee that
every resource remains available or permits every type of reuse.
Re-check each source page, license, and current files before publication
or redistribution.
