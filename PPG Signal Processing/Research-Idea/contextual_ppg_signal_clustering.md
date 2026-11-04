# Context-Aware Discovery of Personalized PPG Morphology Patterns
## Longitudinal Wearable Photoplethysmography, Self-Reported Daily Context, and Transition Dynamics

**Research manuscript and study-protocol draft**  
**Version:** 0.1 — 4 November 2026  
**Status:** Conceptual manuscript scaffold. No experimental findings are claimed. Replace all bracketed fields after data collection and analysis.

> **Scope note:** This draft develops a research proposal around continuous PPG, recurring waveform morphology, time-stamped daily-life descriptions, and context-linked transitions. It is not evidence that PPG can read thoughts, identify emotions, or uniquely infer a task. Self-reports provide contextual annotations; PPG provides physiological measurements that are influenced by multiple interacting factors.

---

## Manuscript information

- **Proposed title:** Context-Aware Discovery of Personalized PPG Morphology Patterns Using Longitudinal Physiological and Self-Reported Behavioral Data
- **Alternative title:** Beyond Activity Labels: Personalized PPG Waveform States and Their Associations With Daily-Life Context
- **Short title:** Context-Aware PPG Pattern Discovery
- **Article type:** Original research article (longitudinal observational study; optionally combined with controlled repeated-measures experiments)
- **Keywords:** photoplethysmography; PPG; wearable sensors; waveform morphology; unsupervised learning; clustering; longitudinal monitoring; ecological momentary assessment; self-report; activity context; personalized physiology; transition dynamics

## Abstract (structured template)

**Background:** Wearable photoplethysmography (PPG) enables continuous monitoring of pulse-related optical signals in daily life. Beyond pulse rate, PPG waveforms contain morphology and amplitude information influenced by cardiac dynamics, peripheral vascular tone, respiration, temperature, posture, movement, sensor coupling, and other factors. Unsupervised methods may identify recurring waveform patterns, but the physiological and behavioral contexts associated with those patterns are often incompletely characterized.

**Objective:** To investigate whether recurring, personalized PPG waveform patterns can be discovered from longitudinal wearable recordings and meaningfully characterized using synchronized physiological signals and time-stamped self-reported daily-life context. A secondary objective is to characterize transitions between waveform-pattern states and assess whether those transitions are associated with changes in activity, task, and reported experience.

**Methods:** [Describe participants, recording duration, wearable device, PPG sampling frequency, additional sensors, diary/EMA protocol, data synchronization, preprocessing, pulse segmentation, representation learning, clustering, context coding, and statistical analysis.] PPG pulses or short windows will be quality-screened and represented using morphology features and/or learned embeddings. Clustering will be conducted using participant-specific and, where justified, pooled representations. Time-stamped diary annotations will be aligned to PPG windows using prespecified temporal rules. Associations will be evaluated using repeated-measures statistical models and participant-wise validation.

**Results:** [Complete after data collection. Report participant flow, recording coverage, quality-screened data yield, number and stability of waveform families, context associations, transition findings, and uncertainty.]

**Conclusion:** [Complete only after analysis.] The study will assess whether longitudinal PPG contains reproducible personalized waveform patterns whose occurrence and transitions are associated with recorded daily-life context, while distinguishing physiological interpretation from measurement artifact and self-report uncertainty.

---

# 1. Introduction

## 1.1 Background

Photoplethysmography (PPG) is an optical technique that measures changes in light absorption or reflection associated with pulsatile blood-volume changes in tissue. PPG is widely integrated into smartwatches, fitness bands, and clinical monitoring devices. Although it is commonly used to estimate pulse rate and oxygen saturation, the pulse waveform also contains information about pulse morphology, peripheral perfusion, vascular tone, and cardiovascular dynamics.

The morphology of a PPG pulse is not fixed. It can vary with heart rate, stroke volume, vascular compliance and tone, respiration, temperature, posture, sleep, exercise, emotional arousal, and local peripheral circulation. It is also sensitive to non-physiological influences, including motion, sensor displacement, contact pressure, ambient light, skin properties, wavelength, and device-specific processing.

Longitudinal wearable recording offers an opportunity to study this variation in natural settings. A recording spanning several weeks may contain repeated examples of similar physiological and behavioral circumstances. Rather than relying exclusively on predefined labels such as walking, sitting, or sleeping, unsupervised learning may reveal recurring waveform families that are not obvious from conventional summary statistics.

However, a waveform cluster is initially only a statistical grouping. It is not automatically a distinct physiological state. To interpret recurring clusters, they must be examined alongside independent context: activity and posture, ECG-derived timing, temperature, respiration, signal-quality measures, and time-stamped self-reports.

## 1.2 Motivation: from waveform clustering to context-aware discovery

A purely signal-driven analysis might identify multiple recurring PPG waveform shapes. Yet it may not explain why a particular shape appears, whether it is reproducible, or whether it reflects physiology rather than measurement conditions.

This study proposes combining three information layers:

1. **Physiological measurements:** continuous PPG and, where available, accelerometry, ECG, skin temperature, respiration, and electrodermal activity.
2. **Daily-life context:** time-stamped descriptions of activities, tasks, perceived stress, mood, sleep, meals, caffeine, and other relevant events, collected with participant consent and a low-burden diary or ecological momentary assessment (EMA) method.
3. **Pattern discovery:** waveform representation, clustering, cluster stability assessment, temporal sequence analysis, and context association.

The objective is not to infer a person's private thoughts from PPG. Instead, it is to test whether waveform patterns show reproducible associations with recorded contexts after accounting for observable confounders and signal quality.

## 1.3 Research problem

Current wearable analytics often reduce continuous physiological data to a small set of metrics or activity labels. Such summaries can miss within-person waveform diversity and the temporal relationship between daily-life events and physiological changes.

Two windows may both be labelled “sitting,” yet one may occur during quiet reading and another during a demanding work task. Conversely, similar PPG morphology may appear in different contexts. This raises several questions:

- Are there recurring, participant-specific PPG waveform families?
- Are those families stable across days and repeated circumstances?
- Do they occur disproportionately in particular recorded contexts?
- Do transitions between waveform families align with activity changes, task changes, or reported experiences?
- Can contextual information improve interpretation without overclaiming causality or emotion detection?

## 1.4 Aim

To discover and characterize recurring personalized PPG waveform patterns in longitudinal wearable recordings and evaluate their associations with synchronized physiological measurements and time-stamped self-reported daily-life context.

## 1.5 Objectives

1. Collect and curate longitudinal PPG recordings over [e.g., 30 days], with synchronized contextual sensor data where available.
2. Develop a reproducible pipeline for PPG pulse segmentation, signal-quality assessment, morphology representation, and normalization.
3. Identify recurring waveform families using unsupervised clustering or representation-learning methods.
4. Evaluate the reproducibility and stability of waveform families across days, sessions, and recording conditions.
5. Align waveform patterns with time-stamped activity, task, and self-reported experience annotations.
6. Quantify associations between waveform families and recorded contexts while controlling for relevant physiological and measurement covariates.
7. Characterize transitions between waveform families and their relationship to transitions in activity or context.
8. Assess whether contextual features improve the prediction or interpretation of waveform patterns beyond sensor-derived context alone.

## 1.6 Research questions

- **RQ1:** Can recurring PPG waveform morphology families be identified from longitudinal wearable recordings within an individual?
- **RQ2:** Are the discovered waveform families reproducible across different days and repeated observations?
- **RQ3:** Are waveform families associated with particular activities, tasks, postures, or self-reported experiences?
- **RQ4:** Do context associations remain after accounting for heart rate, movement, temperature, respiration, time of day, and signal quality?
- **RQ5:** Do transitions between waveform families correspond to transitions in activity or reported context?
- **RQ6:** Does adding time-stamped self-report improve contextual interpretation compared with using physiological sensors and activity labels alone?
- **RQ7:** How much do waveform families and their context associations vary between individuals?

## 1.7 Hypotheses

These hypotheses are provisional and should be refined before confirmatory analysis.

- **H1:** Longitudinal PPG recordings contain recurring within-person waveform morphology patterns that can be identified using quality-controlled unsupervised representations.
- **H2:** Some waveform families recur across separate days and are not merely one-off clusters caused by isolated artifacts.
- **H3:** The probability of observing particular waveform families differs across recorded activity, posture, and task contexts.
- **H4:** Some context associations remain after adjustment for heart rate, movement, temperature, respiration, time of day, and signal quality.
- **H5:** Waveform-family transitions contain temporal information about changes in activity or context beyond static cluster frequencies.
- **H6:** Personalized representations provide more reproducible or interpretable patterns than a single population-wide clustering model.

**Exploratory rather than confirmatory:** Associations with self-reported stress, mood, or emotional experience. These are subjective, context-dependent labels and must not be treated as ground truth for a physiological or psychological diagnosis.

---

# 2. Related Work and Literature Review

The following papers are useful starting points. They cover long-term PPG diary collection, daily-life morphology and quality, PPG stress monitoring, unsupervised waveform morphology analysis, and repeated self-report methods. They do not collectively prove the proposed contribution; a systematic literature review is required.

## 2.1 Longitudinal PPG with a daily activity diary

**Charlton, P. H., Kyriacou, P., Mant, J., & Alastruey, J. (2020). “Acquiring Wearable Photoplethysmography Data in Daily Life: The PPG Diary Pilot Study.”**  
*Engineering Proceedings, 2*(1), 80.  
DOI: https://doi.org/10.3390/ecsa-7-08233  
Full text: https://pmc.ncbi.nlm.nih.gov/articles/PMC7610437/  
PubMed: https://pubmed.ncbi.nlm.nih.gov/33778803/

A single participant wore a wrist-worn PPG device for four weeks and recorded daily activities in a diary. The study reported practical challenges in long-term acquisition and found that signal quality varied markedly by activity. It also illustrated changes in PPG pulse shape during exercise recovery and sleep onset.

**Relevance:** This is a particularly close methodological precedent for combining multi-week PPG with activity diaries. It supports feasibility while showing that wear time, data capture, and signal quality can be limiting.

**Difference:** It was a one-participant feasibility pilot, not a systematic unsupervised discovery of personalized waveform families linked to rich, time-stamped task and self-report context.

## 2.2 PPG quality and morphology in daily life

**“Quality Assessment and Morphological Analysis of Photoplethysmography in Daily Life.” (2022)**  
Open access: https://pmc.ncbi.nlm.nih.gov/articles/PMC9300860/

This study analysed 24-hour PPG and accelerometer recordings from 31 participants using Empatica E4 wristbands. It investigated signal quality and PPG morphology under daily-life conditions.

**Relevance:** It demonstrates that daily-life PPG morphology can be studied at scale beyond a single participant, while emphasizing the strong dependence of signal quality on activity and movement.

**Difference:** The primary focus is quality assessment and morphological analysis, rather than aligning discovered waveform clusters with detailed personal diary descriptions.

## 2.3 Wearable PPG and stress monitoring

**“Photoplethysmography Enabled Wearable Devices and Stress Detection: A Scoping Review.” (2022)**  
Open access: https://pmc.ncbi.nlm.nih.gov/articles/PMC9695300/

This scoping review summarizes wearable PPG-based stress-detection research and discusses ground-truth approaches, including self-report questionnaires and physiological measurements.

**Relevance:** It helps frame the use and limitations of self-reported stress labels, and highlights contextual confounding in wearable stress research.

**Difference:** Stress detection is not the same as discovering waveform morphology families. The proposed study should avoid claiming that a cluster is a stress state merely because it appears during a self-reported stressful task.

## 2.4 Personalized stress monitoring in everyday settings

**“Personalized Stress Monitoring using Wearable Sensors in Everyday Settings.” (2021)**  
PubMed: https://pubmed.ncbi.nlm.nih.gov/34892791/

This work investigated personalized stress monitoring in everyday environments using wearable physiological data and self-reported stress labels collected over periods of one to three months. It highlights the importance of personalized models and context-aware label collection.

**Relevance:** Supports the feasibility and importance of personalized physiological modelling using self-reports in natural settings.

**Difference:** Its focus is stress prediction from HR/HRV-related measures rather than unsupervised PPG waveform morphology discovery.

## 2.5 Unsupervised learning of PPG waveform morphology

**Ho, Y.-C., et al. (2024). “Variability of morphology in photoplethysmographic waveform quantified with unsupervised wave-shape manifold learning for clinical assessment.”**  
*Physiological Measurement, 45*(9).  
DOI: https://doi.org/10.1088/1361-6579/ad7779  
PubMed: https://pubmed.ncbi.nlm.nih.gov/39231468/

This study used unsupervised wave-shape manifold learning to quantify PPG morphology variation in patients undergoing surgery. It emphasizes both the potential clinical information in waveform variation and the need for meticulous artifact processing.

**Relevance:** Strong precedent for unsupervised analysis of PPG waveform morphology and latent shape representations.

**Difference:** It studies perioperative clinical recordings and outcomes, rather than long-term free-living PPG associated with time-stamped self-reported daily context.

## 2.6 Wearable PPG in daily life

**Ikarashi, A. (2023). “Wearable photoplethysmography in daily life.”**  
*Japanese Journal of Applied Electrophysiology and Medicine, 31*(4), 504–509.  
DOI: https://doi.org/10.14243/jsaem.31.504  
Article: https://www.jstage.jst.go.jp/article/jsaem/31/4/31_504/_article/-char/en

This article discusses short-term and long-term wearable PPG measurements in daily scenarios, including pulse-interval variation associated with lifestyle differences and potential stress assessment.

**Relevance:** Provides context for interpreting long-term PPG time series and lifestyle-related variability.

## 2.7 Ecological momentary assessment and smartwatch self-report

**“Feasibility and Utility of Multimodal Micro Ecological Momentary Assessment on a Smartwatch.” (2025; CHI 2025 proceedings).**  
DOI: https://doi.org/10.1145/3706598.3714086  
Open access: https://pmc.ncbi.nlm.nih.gov/articles/PMC12718675/  
PubMed: https://pubmed.ncbi.nlm.nih.gov/41431709/

This study examined brief smartwatch-based self-report using touch or speech. In a seven-day field study with 20 participants, prompts asked participants to label posture and/or activity at high frequency. The work illustrates the feasibility and burden trade-offs of collecting frequent context labels.

**Relevance:** Helps design a low-burden diary/EMA protocol rather than relying entirely on retrospective free-text descriptions.

## 2.8 Provisional research gap

The related work suggests that:
- Longitudinal PPG and activity diaries can be collected, but signal quality and adherence are challenging.
- PPG morphology varies during daily life and can be studied using quality-aware methods.
- Unsupervised learning can quantify waveform morphology variation in clinical data.
- Wearable PPG has been used in personalized stress research with self-reported labels.
- EMA methods can collect frequent contextual self-reports, but prompt burden and compliance must be managed.

**Provisional gap statement:** There is an opportunity to investigate whether personalized recurring PPG waveform families discovered from multi-week wearable recordings can be reproducibly characterized by time-aligned daily-life context and self-reported experiences, and whether transitions between those families provide additional information beyond static activity labels and standard physiological summaries.

This gap is provisional. Before claiming novelty, search PubMed, IEEE Xplore, Scopus, Web of Science, ACM Digital Library, and Google Scholar for studies combining long-term PPG morphology, unsupervised clustering, diary/EMA, and within-person context association.

---

# 3. Conceptual Framework

## 3.1 Three-layer framework

![Context-aware PPG discovery framework](figures/context_aware_framework.svg)

### Layer A: Physiological signal stream

- PPG waveform
- Accelerometer and gyroscope
- ECG, where available
- Skin temperature
- Respiration
- EDA, where available
- Contact pressure or sensor-fit information, where available

### Layer B: Time-stamped contextual annotations

- Activity and posture
- Task category (e.g., reading, typing, meeting, cooking, commuting)
- Self-reported stress or workload
- Self-reported mood or affect
- Sleep and wake events
- Meals, caffeine, exercise, and other relevant exposures
- Optional short free-text notes

### Layer C: Pattern discovery and interpretation

- PPG quality assessment
- Beat segmentation
- Morphology feature extraction
- Learned waveform embeddings
- Unsupervised clustering
- Cluster stability and recurrence analysis
- Context association
- Transition sequence analysis
- Personalized reference profiles

## 3.2 Unit of analysis

The project may analyse data at several levels:

1. **Beat-level:** one segmented PPG pulse.
2. **Window-level:** a short interval containing multiple beats, summarized by robust morphology statistics.
3. **Episode-level:** a contiguous period with a recurring waveform family or context.
4. **Event-level:** a diary/EMA event or activity transition.
5. **Day-level:** daily summaries and recurrence patterns.
6. **Participant-level:** personalized distributions and models.

The primary unit should be chosen based on the scientific question. Beat-level clustering can produce huge sample counts but risks treating adjacent, highly correlated beats as independent observations. Window- or episode-level summaries may be more robust for context association.

## 3.3 What is a “waveform pattern”?

A cluster is a group of pulses or windows that are similar under a selected representation and distance metric. It should initially be called a **waveform morphology cluster** or **waveform family**, not a physiological state.

A cluster may reflect:
- genuine morphology variation;
- heart-rate-related changes;
- peripheral vascular changes;
- respiration-related modulation;
- sensor location or contact changes;
- movement artifact;
- signal quality;
- device-specific characteristics;
- a mixture of these factors.

Physiological interpretation requires independent evidence and repeatability.

## 3.4 Personalized versus population-level discovery

Two strategies should be considered:

**Personalized clustering:** Build a representation and clusters for each participant. This can capture individual morphology and anatomy, but cluster IDs are not directly comparable between people.

**Population-level clustering:** Learn a shared representation across participants, then test whether it generalizes. This can support group-level comparisons but may obscure individual differences.

**Recommended approach:** Start with personalized discovery for the primary exploratory question. Then investigate whether a common embedding or harmonized cluster taxonomy can be learned across participants. Never assume that “cluster 3” means the same thing for two people unless cross-person correspondence is explicitly established.

---

# 4. Study Design

## 4.1 Overall design

A prospective longitudinal observational study is recommended, with continuous wearable recording for approximately 30 days per participant. A controlled protocol may be added to collect repeated examples of selected contexts and transitions.

The study has two complementary components:

1. **Free-living longitudinal component:** captures naturally occurring waveform patterns and daily-life context.
2. **Optional controlled component:** repeats selected activities or transitions under standardized conditions to test repeatability and improve interpretability.

The free-living component supports ecological validity. The controlled component helps distinguish physiological variation from uncontrolled differences in environment and behavior.

## 4.2 Participants

- Target population: [define].
- Inclusion criteria: [define].
- Exclusion criteria: [define].
- Planned sample size: [determine from pilot data and power analysis].
- Recording duration: [e.g., 30 consecutive days].
- Ethics approval: [committee and approval number].
- Consent: written informed consent.

A one-person 30-day dataset can be useful for algorithm development and hypothesis generation, but it cannot establish generalizability. For a publishable group-level study, recruit multiple participants and plan repeated observations per person. A pilot may begin with a small cohort to estimate wear-time, quality, and diary adherence; use those data to justify the main sample size.

## 4.3 Sensor configuration

| Signal | Role | Suggested use |
|---|---|---|
| PPG | Primary outcome stream | Raw waveform, pulse morphology, amplitude, pulse intervals |
| Accelerometer | Essential context | Movement intensity, activity, motion artifact indicators |
| Gyroscope | Useful | Wrist orientation and movement characterization |
| ECG | Strongly recommended in validation subset | Independent cardiac timing reference |
| Skin temperature | Recommended | Peripheral thermal context |
| Respiration | Recommended if feasible | Respiratory rate and respiratory modulation |
| EDA | Optional | Additional arousal-related context, not a direct emotion label |
| Contact pressure | Valuable if available | Sensor coupling and fit changes |

Record device model, sensor site, wavelength, sampling frequency, resolution, firmware, strap tightness, skin contact, charging schedule, and all data gaps.

## 4.4 Data acquisition requirements

- Prefer raw PPG access rather than only device-derived heart rate.
- Record sampling frequency and timestamps accurately.
- Preserve raw data without overwriting.
- Synchronize all sensors and diary timestamps.
- Record device removal, charging, sensor adjustment, and data transfer failures.
- Monitor wear compliance and participant burden.
- Record ambient temperature or environmental conditions where feasible.
- Ensure the sensor is comfortable and safe for prolonged wear.

A previous four-week PPG diary pilot showed that signal acquisition and quality can be much lower than nominal wear time, with marked differences across activities. Plan for missingness and quality loss rather than assuming 30 days of recording equals 30 days of usable PPG.

---

# 5. Daily-Life Diary and Ecological Momentary Assessment

## 5.1 Why use self-reported context?

Sensor-derived activity labels cannot fully describe what a person is doing or experiencing. Accelerometry may indicate that someone is sitting, but not whether they are reading, studying, attending a meeting, or relaxing. Self-report can provide contextual information that sensors cannot directly observe.

The diary is not intended to capture every thought. It should collect only information relevant to the research questions and should be designed to minimize participant burden.

## 5.2 Recommended context fields

### Core fields (high priority)

- Timestamp
- Start and end time, if recording an episode
- Activity category
- Posture
- Task category
- Whether the entry is retrospective or near-real-time

### Optional self-report fields

- Perceived stress (brief ordinal scale)
- Mental workload or concentration (brief ordinal scale)
- Mood/affect (short validated scale or a small set of carefully defined items)
- Perceived exertion after exercise
- Sleep quality or wake event
- Caffeine/meal/exercise event, if relevant to the hypotheses

### Free-text description

A short optional note may help identify unusual context, for example:
- “Preparing for an exam”
- “Had a difficult meeting”
- “Walking quickly to catch a bus”
- “Relaxing and reading”

Do not require participants to describe private thoughts or every activity. Free text may contain highly sensitive personal information and should be minimized, access-controlled, and retained only when necessary.

## 5.3 Collection strategy

A practical hybrid design:

1. **Event-based logging:** participant records major events such as exercise, meals, waking, stressful tasks, or sensor removal.
2. **Low-frequency prompts:** brief prompts at a manageable interval during waking hours (e.g., several times per day, or a pilot-tested schedule).
3. **End-of-day review:** participant can correct broad activity intervals, without reconstructing every minute.
4. **Passive sensing:** accelerometry and other sensors provide continuous objective context where possible.

Avoid very frequent prompts unless a pilot demonstrates acceptable compliance. Prompt burden can reduce adherence and may itself alter behavior.

## 5.4 Context coding

Convert diary text into a structured taxonomy before confirmatory analysis.

Example categories:

| Domain | Example categories |
|---|---|
| Activity | sedentary, walking, exercise, household activity, commuting |
| Posture | sitting, standing, supine, other |
| Task | work/study, meeting, reading, eating, leisure, social interaction |
| Self-reported stress | low, moderate, high, missing |
| Affect | use a validated short instrument where possible |
| Exposure | caffeine, meal, exercise, medication change if ethically justified |
| Sleep | asleep, awake, time since waking |

Free-text coding may be performed by trained annotators using a predefined codebook. If automated NLP or language models are used, validate the labels against human coding, document errors, and do not send identifiable diary content to third-party services without appropriate consent and data governance.

## 5.5 Temporal alignment

For each PPG window, determine which context annotation applies. Use explicit rules:

- If an event has start and end times, align the PPG window to the interval.
- If only a point timestamp is available, define a prespecified association window before and after the report.
- Record uncertainty when diary timestamps are approximate.
- Avoid assigning a precise context label to long periods based on a single retrospective note.
- Keep “unknown / not reported” as a valid category.

Test multiple plausible alignment windows in sensitivity analysis. Context associations may weaken or change when timestamps are imprecise.

---

# 6. PPG Signal Processing and Morphology Representation

## 6.1 Preprocessing pipeline

1. Validate timestamps, sampling frequency, and data integrity.
2. Detect missing segments, clipping, saturation, and flatline intervals.
3. Identify likely sensor-off and gross displacement periods.
4. Apply filtering appropriate to the target feature and device.
5. Detect pulse onsets and segment individual pulses.
6. Calculate beat-level signal-quality indices.
7. Reject or flag unreliable pulses/windows using prespecified rules.
8. Extract morphology features or learn waveform embeddings.
9. Store raw, processed, and quality-flagged data separately.

Filtering and normalization must not distort morphology. Report filter type, order, cutoff frequencies, phase response, resampling, pulse detection algorithm, and edge handling.

## 6.2 Signal quality assessment

Quality assessment is essential because an unsupervised algorithm may cluster artifacts into apparently distinct waveform families.

Potential quality indicators:
- beat detector confidence;
- pulse shape plausibility;
- signal clipping or saturation;
- baseline drift;
- high-frequency noise;
- motion intensity;
- abrupt discontinuities;
- beat-to-beat morphology consistency;
- ECG–PPG timing consistency, where ECG is available.

Analyse quality by context. If low-quality clusters occur mostly during walking or cooking, they may represent motion/coupling artifacts rather than novel physiology.

Do not simply discard all movement. Preserve a quality label and report both the full dataset and a high-quality subset, where possible.

## 6.3 Beat segmentation

Segment individual pulses using a validated onset detector. Inspect representative examples manually. Pulse segmentation errors can create false morphology clusters.

For each beat, retain:
- start/end timestamp;
- pulse onset and peak;
- beat duration;
- amplitude;
- quality score;
- associated sensor context;
- participant and recording-day identifiers.

## 6.4 Morphology feature engineering

Start with interpretable features before moving to complex embeddings.

Potential features:
- normalized pulse amplitude;
- pulse width at 25%, 50%, and 75% of amplitude;
- systolic rise time;
- pulse duration;
- pulse area;
- maximum upstroke slope;
- maximum downstroke slope;
- augmentation or secondary peak descriptors, if reliably detectable;
- first- and second-derivative features;
- beat-to-beat morphology similarity;
- pulse interval and pulse-rate summary.

Feature definitions must be consistent and robust to sampling rate. Not every feature is reliable for every sensor site or wearable device.

## 6.5 Waveform normalization

Normalization is a major design decision. It can remove meaningful physiological information if applied carelessly.

Consider at least two representations:

**Shape-focused representation:** normalize amplitude and duration to emphasize morphology independent of scale and pulse interval.

**Physiology-preserving representation:** retain amplitude, pulse interval, and selected scale-related features alongside normalized shape.

Do not use only min-max normalization if absolute amplitude or DC level may be biologically meaningful. Preserve raw values and test whether clustering changes under different normalization strategies.

---

# 7. Unsupervised Pattern Discovery

## 7.1 Candidate approaches

Start with simple, interpretable methods and establish a robust baseline.

| Method | Strength | Limitation / consideration |
|---|---|---|
| K-means | Simple, scalable baseline | Requires choosing K; assumes roughly compact clusters |
| Gaussian mixture model | Soft membership probabilities | Distribution assumptions; can be sensitive to feature scaling |
| Hierarchical clustering | Reveals multi-scale structure | Can be computationally expensive |
| DBSCAN | Finds dense groups and noise | Sensitive to distance and density parameters |
| HDBSCAN | Variable-density clusters and noise assignment | Parameter choices still require sensitivity analysis |
| UMAP + clustering | Useful visualization / nonlinear representation | Visualization distances can be misleading; avoid treating 2-D plot as proof |
| Autoencoder embeddings | Learns waveform representations | Needs careful training and validation; may encode artifacts |
| Contrastive/self-supervised learning | Can learn useful representations from unlabeled signals | Positive/negative pair design and invariance assumptions matter |

**Recommendation:** Build a baseline using interpretable morphology features and HDBSCAN or hierarchical clustering. Then compare with a learned embedding. Avoid starting with a target of 1,000 clusters. The number of clusters should emerge from data structure and validation, not from a desired count.

## 7.2 Personalized clustering strategy

For each participant:

1. Build quality-controlled beat/window representations.
2. Normalize using a prespecified strategy.
3. Fit clustering on a training portion of the recording.
4. Assign held-out days to learned clusters.
5. Evaluate whether clusters recur across different days.
6. Compare cluster centroids/prototypes and context distributions.
7. Identify noise/outlier observations rather than forcing every pulse into a cluster.

A cluster should be considered a candidate recurring waveform family only if it has adequate support, meaningful separation, and repeatability across time.

## 7.3 How many clusters?

There is no scientifically justified universal number. One thousand clusters may simply fragment a continuous morphology distribution into many tiny groups.

Assess:
- cluster size distribution;
- silhouette or density-based validity measures, used cautiously;
- stability under resampling and parameter changes;
- recurrence across days;
- within-cluster waveform similarity;
- between-cluster separability;
- relationship with quality indicators;
- interpretability and usefulness for the research question.

Use multi-resolution analysis: a small number of broad waveform families may be useful at one level, with subclusters explored only if they are stable and meaningful.

## 7.4 Cluster stability and reproducibility

Recommended tests:
- bootstrap/resampling stability;
- train on earlier days, test on later days;
- compare clusters across separate recording days;
- perturb preprocessing and normalization choices;
- assess whether clusters are dominated by device state or signal quality;
- compare within-person recurrence across similar contexts.

Randomly splitting adjacent beats or overlapping windows into train and test sets creates leakage. Split by day, session, event, or participant depending on the intended generalization.

## 7.5 Cluster interpretation

For each candidate cluster, report:
- representative waveform/prototype;
- median and spread of morphology features;
- cluster size and temporal distribution;
- signal-quality distribution;
- heart-rate and movement distributions;
- temperature and respiration context, where available;
- diary/EMA context proportions;
- recurrence across days.

Do not assign physiological names such as “stress waveform” or “vasoconstriction cluster” without independent validation. Use neutral labels such as `Cluster A`, `Morphology family 1`, or a descriptive shape label.

---

# 8. Context Association Analysis

## 8.1 Primary analysis

Test whether waveform-cluster occurrence is associated with recorded context.

For each participant and time window, derive:
- cluster assignment or soft membership probabilities;
- activity/posture;
- task category;
- self-report scores;
- physiological covariates;
- signal-quality measures;
- time of day and day index.

Potential analyses:
- cluster frequency by context;
- context distribution within each cluster;
- odds/probability of cluster membership by context;
- within-person comparisons of similar activity but different task context;
- repeated-measures models with participant-level random effects;
- permutation tests preserving temporal structure.

## 8.2 Important confounders

A cluster associated with “work” may actually be associated with:
- sitting posture;
- low or high movement;
- time of day;
- caffeine intake;
- recent walking;
- ambient temperature;
- stress/workload;
- sensor contact;
- heart rate or respiration.

Use a causal diagram or prespecified analysis plan to decide which variables are confounders, mediators, or outcomes. Do not indiscriminately adjust for every available variable: adjusting for a mediator can remove part of the relationship being studied.

## 8.3 Context-specific comparisons

Particularly useful comparisons include:

- Same posture, different task (e.g., sitting while reading versus sitting during a demanding task).
- Same task, different posture.
- Same activity, different self-reported stress.
- Same context across different days.
- Same person, similar heart rate but different morphology cluster.
- Same cluster occurring under multiple contexts.

These within-person comparisons reduce confounding by stable anatomy and baseline physiology, although time-varying confounding remains.

## 8.4 Statistical modelling

For cluster membership, a mixed-effects multinomial logistic model may be considered:

\[
P(C_{it}=k) =
\operatorname{softmax}\left(
\beta_{0k} + \boldsymbol{\beta}_{k}^{T}\mathbf{x}_{it}
+ b_{ik}
\right)
\]

where:
- \(C_{it}\) is cluster membership for participant \(i\) at time \(t\);
- \(\mathbf{x}_{it}\) contains context and physiological covariates;
- \(b_{ik}\) is a participant-level random effect.

For continuous morphology features, use linear or generalized mixed-effects models with participant-level random effects and appropriate temporal correlation.

For within-person association, consider person-mean centering of time-varying predictors. This separates whether a person is generally more stressed than others from whether that person is more stressed than their own average at a given time.

## 8.5 Temporal dependence

Adjacent PPG windows are highly correlated. Do not treat each beat as an independent sample for inference. Aggregate to episodes or use models that account for temporal autocorrelation and participant clustering.

Permutation tests should preserve blocks or episodes rather than randomly shuffling individual beats.

---

# 9. Waveform-Cluster Transition Analysis

## 9.1 Why transitions matter

A static cluster frequency tells how often a waveform family occurs. A transition analysis examines how the signal moves between waveform families over time.

For example, a participant may repeatedly show:
- cluster A during quiet sitting;
- cluster B during a demanding work episode;
- cluster A again after the task ends.

Such a sequence is potentially informative, but it must be evaluated against heart rate, movement, temperature, and signal quality.

## 9.2 Defining a cluster episode

Avoid treating every single-beat label change as a real state transition. Cluster assignments may flicker because of noise or borderline morphology.

Define an episode using:
- minimum duration or minimum number of consecutive windows;
- optional temporal smoothing or hysteresis;
- minimum cluster-membership confidence;
- a separate unknown/noise state;
- explicit handling of gaps and poor-quality intervals.

Specify these rules before testing associations.

## 9.3 Transition metrics

- transition frequency per hour/day;
- dwell time in each waveform family;
- transition probabilities;
- transition entropy;
- cluster sequence motifs;
- time from context event to cluster change;
- return-to-prior-cluster probability;
- transition duration and uncertainty.

A transition matrix can summarize the probability of moving from cluster \(i\) to cluster \(j\), but a Markov assumption should be tested rather than assumed. Higher-order or semi-Markov models may be useful if dwell time and history matter.

## 9.4 Aligning transitions with diary events

For each diary event:
1. identify the event timestamp and uncertainty;
2. inspect cluster state before and after the event;
3. define a prespecified event window;
4. compare with matched control times from the same participant;
5. account for activity, posture, heart rate, movement, temperature, and quality;
6. report whether the cluster transition precedes, follows, or coincides with the reported event.

Temporal alignment does not establish causation. A diary event may be reported after it occurred, and the physiological response may precede the report.

---

# 10. Distinguishing Physiology, Context, and Artifact

This is one of the most important parts of the study.

| Pattern observation | Possible physiological interpretation | Possible artifact/context explanation | Checks |
|---|---|---|---|
| A cluster appears during walking | Exercise-related cardiovascular/peripheral change | Motion artifact or sensor displacement | ACC, ECG timing, quality metrics, repeated trials |
| A cluster appears during stressful work | Autonomic/cardiovascular change may contribute | Sitting, caffeine, time of day, task posture | Self-report, HR/IBI, respiration, temperature, matched comparisons |
| A cluster appears during sleep | Sleep-stage/autonomic/perfusion variation | Low movement improves quality; sensor pressure changes | Sleep stage if available, temperature, quality, position |
| Amplitude changes with temperature | Peripheral vasomotor response | Optical coupling or skin-contact variation | Skin temperature, pressure, repeated stable measurements |
| Cluster changes abruptly | Sudden physiological event or posture change | Strap shift, impact, clipping, dropout | ACC, signal discontinuity, contact, ECG |
| Cluster changes gradually | Gradual physiological adaptation | Baseline drift, slow sensor movement | Quality indices, temperature, repeated observations |

### ECG interpretation

ECG can help validate cardiac timing and identify missed/extra PPG pulse detections. It does not independently validate PPG amplitude or morphology as a vascular measurement.

### Avoid overclaiming psychological inference

PPG is not a direct sensor of thoughts, intentions, or emotions. Self-reported stress or mood may be associated with autonomic changes, but the same PPG response can occur for many reasons. The paper should use phrases such as:
- “associated with self-reported stress”;
- “occurred more frequently during the reported task context”;
- “context-linked waveform pattern”.

Avoid:
- “PPG detected the participant's thoughts”;
- “this cluster proves stress”;
- “the waveform reveals emotion”.

---

# 11. Privacy, Ethics, and Data Governance

Diary descriptions can reveal sensitive information about work, relationships, location, mental state, health, and personal routines. This makes the data more sensitive than physiological sensor data alone.

Minimum safeguards:
- collect only context needed for the research question;
- explain exactly what diary data are collected and why;
- obtain explicit informed consent;
- make free-text entries optional;
- avoid collecting names, exact addresses, or third-party identifying details;
- pseudonymize participant IDs;
- store the identity key separately;
- encrypt data at rest and in transit;
- restrict access by role;
- define retention and deletion schedules;
- document any cloud or third-party processing;
- do not use external AI services on identifiable diary content without appropriate approval and consent;
- publish only appropriately de-identified data, subject to consent and ethics approval.

Participants should be able to skip prompts or withdraw without penalty. Avoid designs that demand continuous self-disclosure.

---

# 12. Evaluation and Validation

## 12.1 Primary endpoints

Choose one primary endpoint before confirmatory analysis. Candidate:
- reproducibility of personalized waveform families across held-out days.

Alternative primary endpoint:
- incremental association between time-stamped context and cluster membership after accounting for measured physiological and signal-quality covariates.

## 12.2 Secondary endpoints

- number and size of stable waveform families;
- cluster stability across resampling and preprocessing choices;
- context enrichment by cluster;
- within-person context association;
- cluster transition frequency and dwell time;
- prediction improvement from diary context;
- quality-related cluster distribution;
- between-person variability.

## 12.3 Baseline comparisons

Compare:
1. **Signal-only model:** PPG morphology features/embeddings.
2. **Signal + quality model:** adds signal-quality and motion features.
3. **Sensor-context model:** adds activity, posture, temperature, respiration, ECG-derived timing.
4. **Diary-context model:** adds structured self-report context.
5. **Combined model:** all permitted inputs.

This tests whether diary information adds value beyond what can already be inferred from wearable sensors.

## 12.4 Validation splits

- **Within-person temporal validation:** train on earlier days, test on later days.
- **Leave-one-day-out validation:** test day-to-day stability.
- **Participant-wise validation:** for population-level models, hold out entire participants.
- **Event-wise validation:** hold out complete diary events or episodes.

Do not randomly split adjacent pulses or overlapping windows. This causes severe data leakage and overstates performance.

## 12.5 Negative controls and sensitivity analyses

Useful checks:
- shift diary timestamps by a random offset to test whether associations depend on correct alignment;
- compare reported context with matched time periods from the same participant;
- test whether cluster identity is predicted by quality indicators alone;
- repeat clustering with alternative normalization methods;
- vary context-alignment windows;
- analyse high-quality PPG separately;
- compare raw and quality-corrected feature representations;
- exclude periods with sensor removal or obvious displacement.

---

# 13. Expected Contributions (Not Results)

If demonstrated by the experiments, the study could contribute:

1. **Personalized waveform discovery:** a longitudinal method for identifying recurring PPG morphology families within individuals.
2. **Contextual characterization:** a framework for associating waveform families with time-aligned behavioral and self-reported context.
3. **Temporal pattern analysis:** characterization of transitions and dwell times between waveform families.
4. **Multimodal interpretation:** integration of motion, ECG timing, temperature, respiration, and signal quality to distinguish candidate physiological patterns from artifacts.
5. **Methodological resource:** a reproducible approach to collecting and aligning long-term PPG with low-burden diary/EMA annotations.

These are proposed contributions. The completed manuscript should report only those supported by the data.

---

# 14. Figures and Tables for the Final Paper

## Proposed figures

1. Study overview: physiological stream + diary/EMA stream → quality control → morphology representation → clustering → context association.
2. Example day timeline showing PPG, activity, and time-stamped diary annotations.
3. Raw and quality-screened PPG examples across different contexts.
4. Waveform cluster prototypes with within-cluster variability.
5. Cluster recurrence across days.
6. Context distribution for each waveform family.
7. Example cluster-state sequence and diary-event alignment.
8. Transition matrix or dwell-time distribution.
9. Validation comparison: signal-only vs sensor-context vs diary-context vs combined models.
10. Participant-level variability in cluster structure and context association.

## Proposed tables

1. Participant characteristics and device specifications.
2. Diary/EMA fields, scales, and prompt schedule.
3. PPG preprocessing and quality criteria.
4. Morphology feature definitions.
5. Clustering algorithms and hyperparameter sensitivity.
6. Cluster stability and recurrence metrics.
7. Context association estimates with confidence intervals.
8. Cluster transition statistics.
9. Missingness and data-quality summary by context.
10. Sensitivity and negative-control analyses.

---

# 15. Limitations and Threats to Validity

Anticipate the following limitations:

- **Unsupervised cluster ambiguity:** clusters are mathematical groupings, not necessarily physiological states.
- **Artifact-driven clusters:** movement, sensor fit, and signal quality may dominate the discovered structure.
- **Normalization choices:** amplitude and duration normalization may remove meaningful information.
- **Diary inaccuracies:** self-report can be delayed, incomplete, retrospective, or socially biased.
- **Context overlap:** tasks, posture, time of day, caffeine, and emotional experience are correlated.
- **Temporal misalignment:** reported event times may not match physiological onset.
- **Within-person dependence:** many pulses do not equal many independent participants.
- **Cluster drift:** morphology and sensor coupling may change over weeks.
- **Device specificity:** wavelength, site, sampling rate, and firmware affect morphology.
- **Generalizability:** personalized clusters may not transfer between participants.
- **Privacy constraints:** rich diary data limit data sharing and may affect participant willingness.
- **Causal inference:** observational associations do not establish that a task or reported emotion caused a waveform pattern.

---

# 16. Reproducibility and Data Management

Record:
- raw device data and metadata;
- timestamp synchronization;
- preprocessing parameters and software versions;
- quality flags and exclusion reasons;
- pulse detection and segmentation outputs;
- feature definitions and normalization;
- embedding model and training settings;
- clustering method and hyperparameters;
- diary codebook and timestamp uncertainty;
- statistical model specifications;
- train/test split rules;
- ethics and data governance constraints.

Suggested project structure:

```text
context-aware-ppg/
├── README.md
├── manuscript/
│   ├── draft.md
│   ├── references.bib
│   └── figures/
├── protocols/
│   ├── sensor_protocol.md
│   ├── diary_ema_protocol.md
│   ├── annotation_codebook.md
│   └── transition_definitions.md
├── data/
│   ├── raw/                 # restricted, pseudonymized
│   ├── processed/
│   ├── annotations/
│   └── metadata/
├── src/
│   ├── quality_control/
│   ├── pulse_segmentation/
│   ├── morphology_features/
│   ├── representation_learning/
│   ├── clustering/
│   ├── context_alignment/
│   ├── transition_analysis/
│   └── statistics/
├── results/
│   ├── tables/
│   └── figures/
└── environment/
    └── requirements.txt
```

---

# 17. Recommended Research Plan

1. **Literature review:** map studies on daily-life PPG, morphology clustering, wearable stress/context monitoring, and EMA.
2. **Pilot feasibility:** record a small number of days and quantify signal availability, diary burden, and timestamp quality.
3. **Define data units:** decide whether clustering beats, windows, or episodes.
4. **Build quality pipeline:** identify artifacts before unsupervised discovery.
5. **Establish baselines:** morphology features plus interpretable clustering.
6. **Test stability:** train on early days and test recurrence on later days.
7. **Add context annotations:** start with activity, posture, task, and a small number of self-report fields.
8. **Perform within-person analysis:** compare similar activity/posture contexts with different reported tasks or experiences.
9. **Analyse cluster transitions:** define episodes and transition rules.
10. **Scale to multiple participants:** test which findings are personalized and which generalize.
11. **Preregister confirmatory analyses:** choose primary endpoint, hypotheses, exclusions, and statistical models.
12. **Complete manuscript:** report null findings, uncertainty, limitations, and reproducible methods.

---

# 18. Publication Positioning

## 18.1 What is not enough by itself?

- Running K-means on PPG pulses and reporting a chosen number of clusters.
- Claiming that each cluster represents a unique physiological state without validation.
- Associating clusters with diary text using only timestamp overlap.
- Calling a cluster “stress” based only on self-reported stress at one time.
- Reporting thousands of windows as independent observations.
- Ignoring signal quality, movement, or device coupling.
- Using random window splits that leak adjacent time-series information.

## 18.2 What would strengthen the contribution?

- Demonstrate cluster recurrence across separate days.
- Quantify cluster stability under resampling and preprocessing changes.
- Show that clusters are not explained primarily by signal quality or motion.
- Use within-person comparisons and repeated observations.
- Show the incremental value of diary context beyond sensor-derived context.
- Include transition/dwell-time analysis.
- Validate across participants or clearly position the work as personalized.
- Make the diary protocol low burden and ethically robust.
- Release code and appropriately de-identified derived data where permitted.

## 18.3 Potential publication areas

Depending on the final contribution, relevant journal scopes may include biomedical signal processing, physiological measurement, wearable computing, ubiquitous computing, digital health, and biomedical engineering. Select a venue based on methodological fit, indexing, peer-review quality, data policy, fees, and author guidelines—not impact factor alone.

---

# 19. Literature Search Strategy to Confirm Novelty

Search multiple databases and document exact queries, dates, and screening decisions.

### Suggested queries

```text
("photoplethysmography" OR PPG) AND
("daily life" OR "free living" OR longitudinal) AND
(diary OR "ecological momentary assessment" OR self-report)

(PPG OR photoplethysmography) AND
(morphology OR waveform shape) AND
(clustering OR "unsupervised learning" OR manifold)

(wearable PPG) AND
(stress OR mood OR workload OR affect) AND
(personalized OR "within-person" OR longitudinal)

("pulse waveform" OR PPG) AND
("activity context" OR task OR behavior) AND
(wearable)

("photoplethysmography" OR PPG) AND
("cluster transition" OR "state transition" OR "temporal pattern")
```

Databases:
- PubMed / MEDLINE
- IEEE Xplore
- Scopus
- Web of Science
- ACM Digital Library
- Google Scholar

For each paper, record:
- PPG sensor site, wavelength, sampling rate, and duration;
- whether raw waveform was available;
- whether morphology or only HR/HRV was analysed;
- whether clustering was used;
- whether diary/EMA was collected;
- whether context was time-aligned;
- whether within-person or between-person models were used;
- whether cluster stability and signal quality were evaluated;
- whether transition sequences were analysed.

---

# 20. References and Starting Resources

1. Charlton, P. H., Kyriacou, P., Mant, J., & Alastruey, J. (2020). **Acquiring Wearable Photoplethysmography Data in Daily Life: The PPG Diary Pilot Study.** *Engineering Proceedings, 2*(1), 80. https://doi.org/10.3390/ecsa-7-08233  
   Full text: https://pmc.ncbi.nlm.nih.gov/articles/PMC7610437/

2. **Quality Assessment and Morphological Analysis of Photoplethysmography in Daily Life.** (2022).  
   Full text: https://pmc.ncbi.nlm.nih.gov/articles/PMC9300860/

3. **Photoplethysmography Enabled Wearable Devices and Stress Detection: A Scoping Review.** (2022).  
   Full text: https://pmc.ncbi.nlm.nih.gov/articles/PMC9695300/

4. **Personalized Stress Monitoring using Wearable Sensors in Everyday Settings.** (2021).  
   PubMed: https://pubmed.ncbi.nlm.nih.gov/34892791/

5. Ho, Y.-C., et al. (2024). **Variability of morphology in photoplethysmographic waveform quantified with unsupervised wave-shape manifold learning for clinical assessment.** *Physiological Measurement, 45*(9). https://doi.org/10.1088/1361-6579/ad7779  
   PubMed: https://pubmed.ncbi.nlm.nih.gov/39231468/

6. Ikarashi, A. (2023). **Wearable photoplethysmography in daily life.** *Japanese Journal of Applied Electrophysiology and Medicine, 31*(4), 504–509. https://doi.org/10.14243/jsaem.31.504

7. **Feasibility and Utility of Multimodal Micro Ecological Momentary Assessment on a Smartwatch.** (2025). *Proceedings of the ACM CHI Conference on Human Factors in Computing Systems.* https://doi.org/10.1145/3706598.3714086  
   Full text: https://pmc.ncbi.nlm.nih.gov/articles/PMC12718675/

8. **Longitudinal User Engagement with Microinteraction Ecological Momentary Assessment (μEMA).** *Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies.* https://doi.org/10.1145/3749541

9. PPG-DaLiA dataset (useful for multimodal activity and PPG pipeline development): https://archive.ics.uci.edu/dataset/495/ppg+dalia

10. WESAD dataset (wearable stress and affect context; not a direct long-term PPG diary dataset): https://ubicomp.eti.uni-siegen.de/home/datasets/icmi18/

---

# 21. Final Research Position

The strongest framing is not that PPG can reveal a person's thoughts or uniquely identify emotions. It is:

> **Can recurring personalized PPG waveform morphology patterns be discovered from longitudinal wearable recordings, and can their occurrence and transitions be meaningfully characterized by time-aligned behavioral, physiological, and self-reported context?**

The potential contribution is the combination of:
- longitudinal personalized waveform discovery;
- explicit signal-quality and artifact assessment;
- low-burden time-stamped context collection;
- within-person context association;
- waveform-family transition analysis;
- validation of reproducibility across days and participants.

**Recommended first-paper scope:** Begin with one or a few participants for pipeline feasibility, but plan a multi-participant study for generalizable conclusions. Use a small, predefined diary taxonomy (activity, posture, task, and one or two self-report measures) rather than collecting unrestricted personal narratives. Demonstrate that the waveform families are stable and not simply artifacts before interpreting their context associations.
