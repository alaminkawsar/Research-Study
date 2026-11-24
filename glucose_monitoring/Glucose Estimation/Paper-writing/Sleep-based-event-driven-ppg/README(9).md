# Sleep-Based Event-Driven PPG Analysis of CGM Glucose Excursions

> **Pilot research blueprint** --- exploratory investigation of whether
> PPG-derived features are associated with CGM-defined glucose events
> during sleep, when motion-related interference is reduced.

## Research Blueprint

### Working research question

**Are changes in photoplethysmography (PPG) waveform morphology and
derived features associated with CGM-detected glucose excursions during
sleep, after accounting for relevant physiological confounders?**

### Core idea

Use continuous glucose monitoring (CGM) data to identify meaningful
glucose events (peaks, valleys, rising and falling excursions). Then
extract synchronized PPG windows around those events and compare PPG
features against matched or nearby stable-glucose periods.

### Proposed hypothesis

PPG-derived features may exhibit measurable temporal associations with
glucose excursions during sleep. Such associations may be indirect and
may reflect physiological pathways or confounders rather than a
glucose-specific signal.

### Objectives

-   Characterize overnight CGM excursions and identify event timestamps.
-   Extract and quality-check synchronized PPG segments around
    CGM-defined events.
-   Explore PPG morphology, amplitude, pulse timing and variability
    features.
-   Compare event windows with stable-glucose control windows.
-   Evaluate associations while accounting for motion, heart rate, sleep
    stage and other available covariates.
-   Assess feasibility, repeatability and limitations; do not assume
    glucose-estimation performance.

### Novelty framing

PPG-based glucose estimation and multimodal PPG--CGM datasets already
exist. The potentially distinctive contribution is **CGM-driven
event-centered characterization of PPG during sleep**, including
comparison with stable-glucose control windows and confounder-aware
analysis. Novelty must be checked through a systematic literature search
before claiming it.

### Pilot scope

Start with a feasibility pilot, subject to resources and ethics
approval. A small pilot can test synchronization, signal quality, event
detection, feature extraction and analysis feasibility; it is not
sufficient by itself to establish clinical accuracy or generalizability.

### Data to collect (ideally)

-   PPG, continuously sampled with device settings documented
-   CGM readings and timestamps
-   Accelerometry/motion (if available)
-   Sleep/wake or sleep-stage information (if available)
-   Heart rate (if available or derived reliably)
-   Skin temperature, respiration or SpO₂ (optional, depending on
    resources)
-   Context: device details, sensor placement, participant metadata
    appropriate to the approved protocol

### Candidate CGM events

-   Local peaks and valleys (after appropriately validated
    preprocessing)
-   Rapid rising and falling excursions, defined using prespecified
    criteria
-   Stable-glucose periods for comparison

Avoid treating noise-driven local extrema as events. Prespecify event
definitions, smoothing, thresholds and sensitivity analyses. CGM
measures interstitial glucose; event times may not exactly correspond to
blood-glucose timing.

### Candidate PPG features

**Time-domain / pulse morphology:** pulse amplitude, pulse width, rise
and decay times, pulse area, pulse intervals, pulse morphology ratios,
systolic peak and dicrotic-notch-related features where reliable.

**Derived / variability:** heart rate, HRV measures where beat detection
and context support interpretation, first/second derivatives (including
SDPPG) where appropriate.

**Signal quality:** quality indices, motion/artifact flags, missing-data
handling and exclusion criteria.

## Research Roadmap

1.  **Phase 1 --- Define the research question**\
    Finalize the question, hypothesis and objectives.\
    *Deliverable:* one-page research brief.

2.  **Phase 2 --- Literature review**\
    Review PPG-based glucose studies, simultaneous PPG--CGM datasets,
    sleep physiology and event-based signal analysis. Search and
    document databases, terms, screening and gaps.\
    *Deliverable:* annotated literature matrix and evidence-based gap.

3.  **Phase 3 --- Write a pilot protocol**\
    Define eligibility, recruitment, sensors, recording duration,
    synchronization, event definitions, control windows, variables and
    analysis plan. Seek ethics approval and informed consent before
    human-subject data collection.\
    *Deliverable:* protocol and ethics materials, as applicable.

4.  **Phase 4 --- Collect data**\
    Record overnight PPG, CGM and supporting signals. Start with a
    feasibility pilot.\
    *Deliverable:* organized, synchronized dataset and data dictionary.

5.  **Phase 5 --- Signal processing**\
    Preprocess signals, assess PPG quality, identify pulses, extract
    features and detect CGM events. Document processing decisions.\
    *Deliverable:* reproducible processing pipeline.

6.  **Phase 6 --- Statistical analysis**\
    Visualize event-centered trajectories; evaluate associations, lagged
    relationships and event/control comparisons; adjust for available
    confounders; account for repeated observations and participant-level
    variation.\
    *Deliverable:* analysis results, figures and tables.

7.  **Phase 7 --- Evaluate scientific validity**\
    Assess robustness, repeatability, sensitivity to event/window
    definitions, missingness, confounding and generalization. Interpret
    negative results honestly.\
    *Deliverable:* validity assessment and limitations.

8.  **Phase 8 --- Write the manuscript**\
    Structure as Abstract, Introduction, Methods, Results, Discussion,
    Limitations and Conclusion; include transparent reporting and
    reproducibility details.\
    *Deliverable:* manuscript draft.

9.  **Phase 9 --- Submit**\
    Select a journal appropriate to the scope and evidence, follow its
    instructions, prepare figures, references, supplementary materials
    and submission documents.\
    *Deliverable:* submitted manuscript.

## Analysis outline

1.  Synchronize CGM and PPG timestamps and document device/sample
    timing.
2.  Establish sleep periods and flag wake/motion or low-quality periods
    where data permit.
3.  Preprocess CGM cautiously; detect events with prespecified
    definitions.
4.  Extract event-centered PPG windows (for example, a prespecified
    interval before and after each event; evaluate window length in
    pilot sensitivity analysis).
5.  Extract PPG features per window and calculate signal-quality
    measures.
6.  Select stable-glucose comparison windows, ideally matched on
    time-of-night, sleep stage, movement and signal quality where
    possible.
7.  Analyze feature trajectories, associations and event/control
    contrasts.
8.  Use participant-aware statistical approaches and validation that
    avoids leakage across the same participant.
9.  Report uncertainty, effect sizes, data limitations and exploratory
    analyses clearly.

## Key cautions

-   Sleep reduces some motion-related interference but does **not**
    isolate glucose from autonomic, temperature, vascular, respiratory,
    sleep-stage or circadian effects.
-   PPG is not a glucose-specific sensor; correlations do not establish
    causation or measurement accuracy.
-   Avoid selecting PPG windows based on the PPG outcome itself; define
    CGM events independently and retain prespecified windows.
-   CGM is an interstitial-glucose measurement and has timing
    limitations relative to blood glucose.
-   Obtain appropriate ethics approval, consent, privacy protections and
    safety oversight before collecting human data.
-   Do not make clinical claims from a feasibility pilot.

## Skills to build gradually

-   Research design and critical literature reading
-   Python: NumPy, Pandas, SciPy, Matplotlib
-   Signal processing: filtering, pulse detection, signal-quality
    assessment and feature extraction
-   Statistics: correlation, regression, repeated measures and
    mixed-effects models
-   Scientific writing, reproducibility, research ethics and data
    management

## Suggested project folders

``` text
project/
├── README.md
├── literature/
│   └── literature_matrix.csv
├── protocol/
├── data/
│   ├── raw/          # access-restricted; do not commit identifiable data
│   └── processed/
├── notebooks/
├── src/
│   ├── preprocessing/
│   ├── event_detection/
│   ├── feature_extraction/
│   └── analysis/
├── figures/
├── results/
└── manuscript/
```

## Project status checklist

-   [ ] Research question and hypothesis refined
-   [ ] Literature search strategy documented
-   [ ] Research gap assessed (no premature novelty claim)
-   [ ] Protocol drafted
-   [ ] Ethics and consent requirements addressed
-   [ ] Device/data feasibility tested
-   [ ] Data dictionary and synchronization plan prepared
-   [ ] CGM event definitions prespecified
-   [ ] PPG quality/exclusion criteria prespecified
-   [ ] Analysis plan drafted
-   [ ] Pilot data collected
-   [ ] Pipeline reproducible
-   [ ] Statistical analysis completed
-   [ ] Results and limitations evaluated
-   [ ] Manuscript drafted
-   [ ] Journal selected and submission prepared

------------------------------------------------------------------------

*This README is a living blueprint. Update it as the protocol and
analysis decisions are refined. It is a research plan, not a clinical
validation protocol.*
