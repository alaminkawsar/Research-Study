### Lesson 2 — Related Work: Where Does Pulse-PPG Fit in Existing Research?

Since you have an advanced ML background, we'll approach this differently from a beginner tutorial.

I want you to read this section with one central research question:

What is genuinely new about Pulse-PPG compared with existing representation-learning methods, and what limitations remain that we could address in a new paper?

We'll use five perspectives:

* Research landscape and competing approaches.

* Technical comparison of existing PPG foundation models.

* Limitations of conventional contrastive learning for PPG.

* Why motif-based relative contrastive learning is interesting.

* Research gaps and potential extensions.

First, let's establish what the authors actually claim.

The paper's related-work section identifies an important gap: existing PPG foundation models either lack public accessibility, are trained primarily on clinical signals, or have not demonstrated sufficient generalization to wearable field conditions.

The authors position Pulse-PPG as an open-source foundation model trained exclusively on real-world field PPG data. arXiv

### Step 1 — Understand the research landscape

Let's classify the existing approaches into four families.

Family A — Supervised PPG learning

![An Overview of the Sensors for Heart Rate Monitoring Used in Extramural Applications | MDPI](https://images.openai.com/static-rsc-4/Z7LWuHZo-bTrCk78g-GpA15wa4LvmribTy2h5in7BvVCwrGS7cb5n7OPxvK3sepZNoiREuFC_nwMKWUSexgA4O4WQQ53VpTc89t73niefjtm7gODcyoAhoq6tCaWdW7yo9CZaiAZJA2vsvIQuu6Cbf6JozcnFZVtL1y3mCMjzOlVDDqCX__q4gFA0sO1uSkk?purpose=fullsize)

Train a neural network using PPG signals and task-specific labels.

Example: predict blood pressure using PPG and blood pressure ground truth.

Limitation: Requires labeled data and can overfit to the dataset and acquisition environment.

Family B — Self-supervised representation learning

![Day 22/100: Contrastive Learning — Teaching Models by Comparing | by Sebastian Buzdugan | Medium](https://images.openai.com/static-rsc-4/IP13CMtzwMfv0ZX-htG_MzyEasBcK8juylQNsx_RR-5hOA410yBUgDubhEiUjiuszzIxaBCMRUh05hoLbSQB-MoI921GBRZvz8PMVcKgjmHUjUtdNNwwSzV3fVL8oDdKCCvbef-T9or7txPPCSNMmJxJKcz7whA9bRVTLrv2ow45DwV_MsNpoH5uQ4P72RQV?purpose=fullsize)

Learn representations from unlabeled signals through pretext tasks.

Example: contrastive learning, reconstruction, or temporal prediction.

Limitation: The quality of learned representations depends heavily on the pre-training objective and assumptions about invariance.

Family C — PPG-specific foundation models

![Improved PPG Peak Detection Using a Hybrid DWT-CNN-LSTM Architecture with a Temporal Attention Mechanism](https://images.openai.com/static-rsc-4/PIpMZ1WXZeTOKVZ3E-lmx4Cyd4FnASXmD1RSqu9MXkDOM2wr2JRKXJhvtFOOX_L5_3bPH9oX8rBrTNvwgfruqc527yeJU_MBtpUkw2ioe_P9YGXpS1uSyFaOEqg3RqxM6Kxp980Fq7_rhHBb53GuhG1oXhwyue2IP0UK1eHyUGtjmf7tQwog5WHA7Eb-1ZHa?purpose=fullsize)

Learn reusable representations specifically for physiological PPG signals.

Examples include PaPaGei and SiamQuality.

Limitation: Data domain, accessibility, and generalization may restrict their usefulness.

Family D — General time-series foundation models

![Description of image](https://images.openai.com/static-rsc-4/8eQmnGYkN0qgUEZHtG1hdMfhbeQF6EhdUzh2cdGRHg5BYaK4b5R9qQA4uV7gVkR8sXYAb6dbrnTaYYY5NuXtrE1PaJI2Lw_JBblRt04oMQJpGW5-W4u9un3tCorPRCz8OimjcnAFvtX4dCG-NN3kXAJc59IKcIvFAKxL77ur58XQpl8qjs5sB2OUk8Q0alDe?purpose=fullsize)

Models designed for general time-series applications.

Examples include MOMENT and Chronos.

Limitation: General-purpose temporal representations may not capture the physiological structure of PPG optimally.

Notice something important: Pulse-PPG is not simply another neural network for heart-rate prediction.

It is a domain-specific representation-learning framework.

That distinction matters when evaluating its novelty.

### Step 2 — Compare the existing PPG models

Let's examine the papers mentioned in the related-work section.

### 2.1 PaPaGei

![6 Modern Cardiac Technologies for Heart Monitoring —](https://images.openai.com/static-rsc-4/dJIH6EbMUI3WJM7mPBKoMNes1l69zpSOr57vgru3p8DdCM0Xn_FagzzJrnUYnIHaWwEKZmvYU_ZgRElKSSSoDESPxY0MYn_h1bvtoEbf4vpnxVzCZWCb63b1p4Q37NyBljWwqAyeISLOFEZQ8W9Ip-7NLw1Vau-QZi0G4_MhOQicb36BoD-g4KLksji-vjKG?purpose=fullsize)

PaPaGei

Pillai et al. (2024).

An open-source PPG foundation model trained on clinical PPG data.

Why is it important?

PaPaGei provides a direct comparison for Pulse-PPG because both aim to learn reusable PPG representations.

The fundamental difference is their training-data domain.

| Dimension       | PaPaGei                    | Pulse-PPG                       |
| --------------- | -------------------------- | ------------------------------- |
| Input           | PPG                        | PPG                             |
| Training domain | Clinical                   | Wearable field                  |
| Signal quality  | Relatively clean           | Naturally noisy                 |
| Main objective  | General PPG representation | Robust field PPG representation |
| Public model    | Yes                        | Yes                             |

Research insight: The difference is not merely the neural network architecture. It is also the distribution of the pre-training data.

This raises a deeper question:

If two models have similar architectures but are trained on different data distributions, how much of their downstream performance difference is attributable to data versus the learning objective?

That is an important experimental question.

### 2.2 Private field-trained PPG foundation model

The authors also discuss the work by Abbaspourazad et al. (2023).

This is particularly interesting because it already explores large-scale field PPG pre-training.

The limitation identified by Pulse-PPG is accessibility: the earlier model and its training data are not publicly available in the same way.

Research insight: Pulse-PPG's contribution is partly scientific and partly infrastructural: it makes a field-trained PPG representation available to other researchers.

### 2.3 SiamQuality

![An Overview of the Sensors for Heart Rate Monitoring Used in Extramural Applications | MDPI](https://images.openai.com/static-rsc-4/WzwzSjzx1PvJZQChFOzSD-3jyp8J43bpiotPvjOkfI4F6ZVSTmWwnDF6XhFBL9UaS0MCCAq0aL7t4kYJrdMf2NsZUO6Ba3dad4cvpSHJNBf1SVu76gOdg_d2ciTAMWd_pbv5ZWG3S8P2KfA-dV1bB8MPdShkKmZkJhKqMg0Iye_rbja2JCkj2BfXMoD41Zq8?purpose=fullsize)

SiamQuality

Ding et al. (2024).

A PPG foundation-model approach that the authors discuss as another private model.

Its relevance is that it explores generalizable PPG representations, but is not as accessible for independent experimentation.

This is important when selecting a baseline for future research.

### 2.4 Other representation-learning approaches

The authors also mention several related approaches:

| Method | Main idea                                      | Research distinction           |
| ------ | ---------------------------------------------- | ------------------------------ |
| REGLE  | Autoencoder-based disentangled representations | Clinical PPG                   |
| TS2TC  | Generative self-supervised learning            | Clinical PPG                   |
| PPG-PT | Pre-training for PPG                           | Narrower downstream evaluation |

The important lesson is that self-supervised learning is not one method.

Different methods impose different assumptions about what a useful representation should preserve.

arXiv

### Step 3 — Why conventional contrastive learning can be problematic for PPG

Now we get to the most interesting part.

You probably already know the standard contrastive-learning objective, such as InfoNCE.

Let's briefly reconstruct the idea.

Suppose we have a PPG sequence:

X \\in \\mathbb{R}^{T}

We generate two augmented views:

X_1 = \\mathcal{A}_1(X)X_2 = \\mathcal{A}_2(X)

An encoder maps them into representations:

z_1=f_\\theta(X_1), \\qquad
z_2=f_\\theta(X_2)

The objective is to make positive pairs similar and negative pairs dissimilar.

A simplified InfoNCE loss is:

\\mathcal{L}_{NCE}
=
-\\log
\\frac{
\\exp(\\operatorname{sim}(z_i,z_i^+)/\\tau)
}{
\\sum_j \\exp(\\operatorname{sim}(z_i,z_j)/\\tau)
}

Where:

* : anchor representation.

* : positive representation.

* : other representations.

* : temperature parameter.

* : similarity function.

### The problem: What is a valid augmentation for PPG?

Consider these common augmentations.

| Augmentation       | Potential problem                              |
| ------------------ | ---------------------------------------------- |
| Amplitude scaling  | Can change physiological amplitude information |
| Temporal shuffling | Destroys temporal structure                    |
| Strong jittering   | May distort pulse morphology                   |
| Cropping           | May remove meaningful cardiac cycles           |
| Time warping       | May alter timing characteristics               |

In computer vision, many transformations preserve semantic identity.

For example, horizontally flipping a cat image usually still produces a cat.

But in physiological signals, a transformation that looks mathematically harmless can destroy information.

Consider amplitude scaling:

X'(t)=\\alpha X(t)

If is large, the amplitude characteristics change.

Those characteristics may contain useful physiological information.

The question becomes:

How can we learn representations without imposing potentially incorrect augmentation invariances?

### My interpretation

This is an important conceptual motivation behind Pulse-PPG.

Rather than relying on conventional augmentation-generated positive pairs, the authors exploit the temporal structure already present in PPG.

That structure is the repeated cardiac-cycle morphology.

### Step 4 — Understand the motif-based representation idea

This is where we need to slow down and think mathematically.

A PPG signal is approximately periodic, although its cycles are not perfectly identical.

A simplified signal can be represented as:

X(t)=\\sum_{k=1}^{N} b_k(t)+\\epsilon(t)

Where:

* represents a local pulse pattern.

* is the number of cardiac cycles.

* represents noise and other variations.

Within a cardiac cycle, we can identify local patterns.

For example:

![Frontiers | Quality Assessment and Morphological Analysis of Photoplethysmography in Daily Life](https://images.openai.com/static-rsc-4/pnkP0ITEkH9ARi60XEG7HcBe14uDjczwpggT0_QNHdWHVY2IUUrEPOHEta4uGm6of9ZigBAcqqPzrwkLh3Vy1gBQ3rDNkGd4U_1JSvr_eD4gQnPbFu1Tlfte_KQmR2zEsfoNJNflqiDx8XrEO2fWyr6N1QaY9oe5-Riiz76Z2lUYw9Idhqn1ZQBGFAa-sncg?purpose=fullsize)

These local patterns are called motifs in the paper.

The authors' important observation is:

Two complete PPG sequences may differ significantly at the signal level while still containing similar local patterns.

For example:

* Sequence A contains a particular pulse morphology.

* Sequence B contains a similar morphology, but at a different temporal location.

* Their point-by-point Euclidean distance may be large.

* Their local motif similarity may still be high.

This suggests that the comparison should be based on matching local patterns rather than requiring exact temporal alignment.

### 4.1 Formalizing the idea

Let:

X_a \\in \\mathbb{R}^{T}

be an anchor sequence and:

X_c \\in \\mathbb{R}^{T}

be a candidate sequence.

The conceptual motif-based distance is:

d(X_a,X_c)
\\approx
\\sum_{i=0}^{T}
\\min_{j\\in\[0,T\]}
d_m\\left(
M(X_a\[i\]),M(X_c\[j\])
\\right)

Here:

* extracts a local motif.

* measures the difference between two motifs.

* indexes anchor positions.

* searches for a matching candidate position.

Notice the asymmetry:

d(X_a,X_c) \\neq d(X_c,X_a)

in general.

Why?

Because every anchor motif searches for its best match in the candidate. Reversing the roles changes the matching operation.

This is an important property to remember when designing extensions.

### 4.2 Why this is interesting

Think about the difference between two similarity concepts:

Pointwise similarity

Compare the signals at corresponding time positions.

d_{\\text{point}}(X_a,X_c)
=
\\sum_t
\\|X_a(t)-X_c(t)\\|^2

Motif similarity

For each local anchor pattern, search for its best matching local pattern in the candidate.

This allows a degree of temporal flexibility.

The second idea is especially attractive for noisy physiological time series.

However, motif matching also introduces potential problems:

* A motif might match an unrelated artifact.

* Repeated patterns can create ambiguous matches.

* Matching may ignore the global order of patterns.

* Asymmetric distance may complicate downstream geometry.

These are not reasons to reject the approach. They are opportunities to investigate it.

### Step 5 — The critical innovation: Relative contrastive learning

Now let's distinguish two different learning objectives.

Ordinary contrastive learning asks:

Are these two examples similar or dissimilar?

Relative contrastive learning asks:

How should the similarity of these examples compare with the similarity of other examples?

Imagine three PPG sequences:

* : anchor.

* : relatively similar to A.

* : relatively different from A.

A binary approach might simply classify B as positive and C as negative.

A relative approach uses the ordering:

d(A,B)<d(A,C)

This is richer supervision.

It provides relational information instead of just binary labels.

The general idea is closely related to metric learning and ranking objectives.

Example: Relative similarity

Anchor A

Reference

PPG sequence A

Smaller learned distance

Sequence B

More similar to A

Larger learned distance

Sequence C

Less similar to A

d(A,B)<d(A,C)

This is a useful abstraction for noisy PPG because similarity can be learned from the data's internal structure rather than requiring manually annotated physiological classes.

Important distinction: This illustration explains the relative-learning principle, not the complete mathematical training objective used by Pulse-PPG. We'll derive the actual objective from the paper in Lesson 4.

### Step 6 — Identify research gaps

Now let's think like researchers rather than readers.

A good research extension should not simply replace ResNet with a Transformer. It should identify a limitation in the existing scientific formulation.

I see six promising directions.

Research direction 1

Disentangling physiological information from motion artifacts

The central hypothesis of Pulse-PPG is that field noise can provide useful contextual information.

But there is a fundamental problem: how do we distinguish useful contextual variation from nuisance variation?

Potential approach:

z = z_{\\text{phys}} + z_{\\text{context}} + z_{\\text{noise}}

Develop a representation-learning framework that explicitly models these components.

Possible contribution: a disentangled field-robust PPG foundation model.

Research direction 2

Multi-modal contrastive learning

PPG alone may not be sufficient to distinguish motion-induced artifacts from physiological changes.

Introduce accelerometer signals:

X_{\\text{PPG}}, X_{\\text{ACC}}

Learn cross-modal representations:

z_p=f_p(X_{\\text{PPG}})z_a=f_a(X_{\\text{ACC}})

Potential contribution: motion-aware physiological representation learning.

This is particularly interesting for smartwatch applications.

Research direction 3

Temporal-order-aware motif learning

Pulse-PPG's motif matching allows local patterns to match across different temporal positions.

However, matching local motifs does not necessarily preserve their global temporal order.

Consider two sequences containing the same motifs but in different orders.

Could they represent different physiological states?

Potential approach: combine motif matching with temporal-order constraints.

\\mathcal{L}
=
\\mathcal{L}_{\\text{motif}}
+
\\lambda\\mathcal{L}_{\\text{order}}

Potential contribution: temporally structured motif representation learning.

Research direction 4

Cross-device and cross-population generalization

Wearable devices differ in:

* Sensor hardware

* Sampling frequency

* Optical characteristics

* Sensor placement

* Skin-device interaction

Develop device-invariant representations and evaluate generalization on completely unseen devices and populations.

Potential contribution: device-independent PPG foundation models.

Research direction 5

Uncertainty-aware PPG representations

A model should recognize when a PPG signal is unreliable.

For example, a heavily corrupted signal should not necessarily produce a confident physiological prediction.

Potential approach: incorporate uncertainty estimation and signal-quality-aware representation learning.

Potential contribution: safer and more reliable wearable inference.

Research direction 6

Efficient real-time foundation models

The original Pulse-PPG model has approximately 28.5 million parameters.

Could we achieve comparable representation quality with:

* Knowledge distillation

* Quantization

* Lightweight temporal encoders

* Streaming inference

Potential contribution: deployable PPG foundation models for resource-constrained wearables.

These are proposed research directions, not established improvements. The paper itself discusses limitations involving demographic diversity, additional modalities, broader pre-training data, and deployment feasibility. arXiv

### Step 7 — Critically evaluate the paper

An important research habit is to distinguish between what a paper demonstrates and what it assumes.

Here are questions I want you to keep in mind:

| Question                                                                          | Why it matters                                                   |
| --------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Is field noise always useful?                                                     | Noise can also obscure physiological information.                |
| Does motif similarity imply physiological similarity?                             | Similar local waveforms may have different causes.               |
| Is the learned distance a true metric?                                            | It may be asymmetric and may not satisfy triangle inequality.    |
| Does field-to-lab generalization imply universal generalization?                  | Different devices and populations may still create domain shift. |
| Does better linear-probe performance imply better representations for every task? | Evaluation depends on task and downstream protocol.              |

One particularly important observation: the authors report superiority over PaPaGei on 10 of 11 downstream tasks, not every task.

Therefore, don't interpret their results as proof that field pre-training is universally superior.

Also, consider the relatively small number of participants in the pre-training cohort compared with the enormous number of signal segments. Millions of windows do not necessarily represent millions of independent physiological subjects.

That distinction matters when evaluating generalization.

### Step 8 — Your research assignment

I want you to attempt a small research-design exercise.

Imagine you are writing a follow-up paper to Pulse-PPG.

Your goal is to propose a new learning objective, not just a different architecture.

Research proposal exercise

1\. Which research direction interests you most?

Physiological and noise disentanglement

Multi-modal PPG + accelerometer learning

Temporal-order-aware motif learning

Cross-device generalization

Uncertainty-aware representations

Efficient wearable foundation models

2\. What is your research hypothesis?

Local motif matching can ignore important temporal ordering information.

3\. What would you change in the methodology?

Combine motif matching with a temporal-order prediction objective.

4\. How would you evaluate the proposed improvement?

Cross-dataset linear probing and subject-independent evaluation.

Submit my research idea

### What comes next: Lesson 3

Next lesson

### Pulse-PPG Methodology: Deep Technical Breakdown

![TCN–Transformer Spatio-Temporal Feature Decoupling and Dynamic Kernel Density Estimation for Gas Concentration Fluctuation Warning](https://images.openai.com/static-rsc-4/kCVk5xlofflQF4xLUBumEy85DYUxvyS6-Pir-Ls0CCbNw2vGPjCiO61qp2bq1rbU_B5sfxorlcO-5d5LH_DpIbWlwl6xfeRrrH6ixdbZjNw8REKqbSrpsxJBlQmuXj2s6YA0FUVLFJnOmKbM10EDxZLdbLbJyiO-ZrC5QgU_t5OrxOy2iM1239qH445zTXNL?purpose=fullsize)

We'll investigate the actual methodology in Section 3.2 and reconstruct:

* Why PPG-specific pre-training is needed.

* How local motifs are represented.

* How the learnable distance function works.

* Why the authors use dilated convolution networks.

* How cross-attention performs motif matching.

* How relative contrastive learning uses the learned distances.

Mathematical depth: We'll derive the equations rather than just describe them.

My recommendation is to pay particular attention to temporal-order-aware motif learning. It creates a concrete research question directly connected to the central mathematical mechanism of Pulse-PPG.

We should understand the original mechanism completely before modifying it.
