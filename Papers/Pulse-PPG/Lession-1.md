Absolutely! Let's read this paper together, step by step, like a research supervisor teaching a student—not just summarizing it.

Our goal is that by the end, you will be able to:

* Explain the paper in your own words.

* Understand its mathematical equations and model architecture.

* Understand why the authors made their design decisions.

* Interpret the experiments, graphs, and results.

* Critically evaluate the paper and identify possible research extensions.

* Eventually, understand how to implement the proposed model.

### Paper: Pulse-PPG

![Using Smartwatches in Stress Management, Mental Health, and Well-Being: A Systematic Review](https://images.openai.com/static-rsc-4/mwyji_fLugjo6URUm1zPxjhGdaJ7lhRulIpNoL7U6yB7xLTcvdURJCjlvnpoXOQ-i_-Xu9ynq8V5qe4Z2EYNHeWo2SFL2IFOLcoZf5irFQx6XKEAoEqO7llcnCbSxKL6qFtrDzUdZL8nca0Wd7SGifFUUWIh6KcDFucF-4pEfEB6Wi7xNLHpDCKnF0SLjbzQ?purpose=fullsize)

Pulse-PPG: An Open-Source Field-Trained PPG Foundation Model for Wearable Applications Across Lab and Field Settings

* Authors: Mithun Saha, Maxwell A. Xu, and colleagues

* Published: 2025

* Field: Wearable computing, biomedical signal processing, deep learning, foundation models.

* Paper: [Read the original paper](https://arxiv.org/html/2502.01108v2?utm_source=chatgpt.com)

* Code: [Official GitHub repository](https://github.com/maxxu05/pulseppg?utm_source=chatgpt.com)

### Our learning roadmap

We'll divide the paper into eight lessons.

* Lesson 1 — Background and research problem

    Understand PPG signals, wearable sensors, foundation models, and why this research matters.

    Starting now

* Lesson 2 — Related work

    Understand existing PPG foundation models and their limitations.

* Lesson 3 — Core methodology

    Understand motif-based learning, contrastive learning, and the main idea behind Pulse-PPG.

* Lesson 4 — Mathematical formulation

    Derive and understand the equations, attention mechanism, and distance function.

* Lesson 5 — Model architecture and training

    Understand the encoder, pre-training procedure, datasets, and implementation.

* Lesson 6 — Experiments and results

    Understand baselines, evaluation datasets, metrics, tables, and figures.

* Lesson 7 — Discussion and limitations

    Identify what the paper demonstrates and what remains unsolved.

* Lesson 8 — Research implementation

    Explore the code and discuss how to reproduce, modify, and extend the model.

### Lesson 1 — Understanding the research problem

### 1\. First, what is PPG?

PPG stands for Photoplethysmography.

It is an optical technique used to measure changes in blood volume beneath your skin.

For example, your smartwatch uses green light to measure changes in blood flow in your wrist.

![Using Smartwatches in Stress Management, Mental Health, and Well-Being: A Systematic Review](https://images.openai.com/static-rsc-4/mwyji_fLugjo6URUm1zPxjhGdaJ7lhRulIpNoL7U6yB7xLTcvdURJCjlvnpoXOQ-i_-Xu9ynq8V5qe4Z2EYNHeWo2SFL2IFOLcoZf5irFQx6XKEAoEqO7llcnCbSxKL6qFtrDzUdZL8nca0Wd7SGifFUUWIh6KcDFucF-4pEfEB6Wi7xNLHpDCKnF0SLjbzQ?purpose=fullsize)

![An Overview of the Sensors for Heart Rate Monitoring Used in Extramural Applications | MDPI](https://images.openai.com/static-rsc-4/Z7LWuHZo-bTrCk78g-GpA15wa4LvmribTy2h5in7BvVCwrGS7cb5n7OPxvK3sepZNoiREuFC_nwMKWUSexgA4O4WQQ53VpTc89t73niefjtm7gODcyoAhoq6tCaWdW7yo9CZaiAZJA2vsvIQuu6Cbf6JozcnFZVtL1y3mCMjzOlVDDqCX__q4gFA0sO1uSkk?purpose=fullsize)

![New High Performance Optical Sensor for Heart Rate Monitoring Ideal for Wearables---Class-leading power consumption and high detection accuracy contributes to device evolution | ROHM Co., Ltd.](https://images.openai.com/static-rsc-4/hj-nlkEkI3i_ZmfDuKOAov_99mb9QYWKJiRX8mTfRoTGy4sIhRgIvZzjIYKWm0ezf4_sIiDn1GtvUmC-_VWBiIUvz3N56535KB2J5-IP7LkFTghM_zYFusMHkJpEEhQNIIjO3BIdsWhr0emR3_zCTFWtIUN6ku30gd_KabMvA394RkVBcXOrLXf8UcjBCeCb?purpose=fullsize)

Here's how it works:

* The smartwatch emits light into your skin.

* Some light is absorbed by blood and surrounding tissue.

* The reflected light changes as blood volume changes.

* The optical sensor measures those changes.

* The device produces a time-series signal.

That time-series signal is called a PPG signal.

For example, a simplified signal might look like this:

![An Overview of the Sensors for Heart Rate Monitoring Used in Extramural Applications | MDPI](https://images.openai.com/static-rsc-4/Z7LWuHZo-bTrCk78g-GpA15wa4LvmribTy2h5in7BvVCwrGS7cb5n7OPxvK3sepZNoiREuFC_nwMKWUSexgA4O4WQQ53VpTc89t73niefjtm7gODcyoAhoq6tCaWdW7yo9CZaiAZJA2vsvIQuu6Cbf6JozcnFZVtL1y3mCMjzOlVDDqCX__q4gFA0sO1uSkk?purpose=fullsize)

Each pulse is associated with a cardiac cycle.

PPG can provide information useful for estimating:

* Heart rate

* Heart rate variability

* Blood oxygen saturation (with appropriate measurement methods)

* Blood pressure (with additional modeling and calibration)

* Physiological responses associated with stress and activity

Important: PPG is not a direct measurement of all these health indicators. Different applications require different models, validation, and sometimes additional sensors.

### 2\. What is the actual problem?

Imagine two scenarios.

![Masimo - Pleth Variability Index (PVi)](https://images.openai.com/static-rsc-4/xRPfKSUyAhO4SVXCVS3Xi0KVE_KY_I9o3GuBWR3T-ilSoAQtcvbg6oT0-MPYqAwZik2vNuyW9THDEILHLAlc_v76VVY63uIl4ihcNIsoTihAyxaC2KfDlCv9WImewxbKDDRim8vmHc-UyciLzlRbPadwwnjWnKQPBkIglYvA7khNdkOScLOqDNxmR0iyiti2?purpose=fullsize)

Scenario A: Laboratory/clinical environment

* Controlled conditions

* Less movement

* Better sensor contact

* Relatively clean signals

![Masimo - Home](https://images.openai.com/static-rsc-4/08DTVTEZhiBNv24GA8mLwW3s4Tb9xblwBUG7Zy5OPxDLK8KSAVPMruxu9JMxScJoQm8Sh7pUN7CqqI5VC9pdjcooU70d5kFFw7SnA3eF2SclBLnFxKcGwCJCLsDVNwobmNzV4nJhPOJHfMvh7KvckuS6ntTNB-ZVV7MF-nWI1lkxMEINcbpqoZL7Ia_aKGbp?purpose=fullsize)

Scenario B: Real-world environment

* Walking and running

* Wrist movement

* Changing lighting

* Loose watch contact

* Motion artifacts

Consider this example:

You train a deep learning model using clean hospital PPG data.

It achieves excellent accuracy in the laboratory.

But when you deploy it on a smartwatch, the accuracy drops.

Why?

Because the training and deployment data have different distributions.

This is called domain shift.

For example:

P_{\\text{lab}}(X) \\neq P_{\\text{field}}(X)

Here:

* = PPG signal

* = distribution of laboratory PPG signals

* = distribution of real-world PPG signals

This is one of the central problems addressed by the paper.

### 3\. What is a foundation model, and why do we need one?

Before understanding Pulse-PPG, you need to understand this concept.

Suppose you want to build three applications:

* Application A: Heart rate estimation.

* Application B: Stress detection.

* Application C: Activity recognition.

The traditional approach is to train three separate models.

Traditional approach

Raw PPG data

Model A

Heart rate

Model B

Stress

Model C

Activity

Each application requires its own representation-learning process.

A foundation model takes a different approach.

First, train one large model to learn general representations from a large amount of unlabeled PPG data.

Then reuse its learned representations for different applications.

Foundation model approach

Large-scale raw PPG dataset

Unlabeled wearable signals

Pulse-PPG foundation model

Learns general physiological representations

Heart rate

Stress

Activity

The important concept is transfer learning.

The foundation model learns useful features first. Then downstream models can use those features for specific tasks.

### 4\. What exactly does Pulse-PPG propose?

Now we can understand the main contribution.

The authors propose something interesting:

> Instead of training a PPG foundation model using only clean clinical signals, train it using noisy, real-world wearable PPG signals.

Their pre-training dataset comes from the MOODS study:

| Property                  | Description                |
| ------------------------- | -------------------------- |
| Participants              | 120 with PPG recordings    |
| Study duration            | Up to 100 days             |
| Unique segments           | 822,247                    |
| Segment duration          | 4 minutes                  |
| Sampling rate of segments | 50 Hz                      |
| Total raw data            | Approximately 55,000 hours |

The authors intentionally preserve real-world noise rather than applying conventional signal filtering.

Why?

Because noise is not always completely useless.

For example:

* Walking may introduce motion artifacts.

* Running may produce different waveform distortions.

* Loose sensor contact may change the signal.

* Environmental conditions may influence measurements.

Some of these variations may contain contextual information.

However, an important distinction: the model is not guaranteed to understand every artifact correctly. The authors' hypothesis is that learning from this variability can improve robustness.

### 5\. The three main technical innovations

This is probably the most important part of the entire paper.

The methodology addresses three challenges.

![Frontiers | Analysis on Four Derivative Waveforms of Photoplethysmogram (PPG) for Fiducial Point Detection](https://images.openai.com/static-rsc-4/FiqjXrL0aEaBn2YqrcOIHRaPbZBkmaZXlBEhAv0XDRjit7ogepQaPoMxPcUAuSm5ewMTYYO-6cUYXEh7nkkD4x6Hzyp_cHBU88UM2MynDc1noA9fscESU7woPgrGGj36DQBFNdCqPi2K5SsN5OpSjbmsMmBCPv23t14yxZSJmONSisQzeOefDNXiOPxvyzJb?purpose=fullsize)

Innovation 1: Motif-based distance function

Instead of comparing two complete signals only, learn to identify similar local waveform patterns, called motifs.

![Frontiers | Photoplethysmogram Analysis and Applications: An Integrative Review](https://images.openai.com/static-rsc-4/yRsGl3YaRHk0AI31TaaxTEJFaORPH8U8iMff6t8TTCXiVmR3OmzxRMQ7qfmfg_VUpyUli-xdftgpNzN5vw7g3E_sCK2GnuJsQIkpxsR8AemcXSa2Rbjq8jPtNBV6c8wdQbvJsohkQ0a2cnQNLInkJqC_VXuZR1GGhnV0BXjf2V_tsojDmS5CKuIyodAeQ8vt?purpose=fullsize)

Innovation 2: Learning from noisy field data

Preserve real-world waveform characteristics rather than assuming that all noise must be removed.

![Contrastive Learning for Audio Embeddings | AI Tutorial | Next Electronics](https://images.openai.com/static-rsc-4/PqNYwtM0sdoRV5INnEh8iWQjH7EcxYXyZGsPjjVbpFr96OryI_vrxMFlQ-CUM5Ptq768Feyg0pQSnpUiS9-nBe7vVquaocjMo6E5vo-9o9c9AsMYKqcJC5_ukPl4J8rh_fqVmIgYLv5OIG4yesmi1u_ggRrrAMwH87RSGNGXccOkTPYhlq-XMtRNN_0F8fqH?purpose=fullsize)

Innovation 3: Relative contrastive learning

Learn not only which signals are similar, but also how similar or dissimilar different signals are relative to one another.

We'll spend considerable time on these three ideas in Lessons 3 and 4.

For now, remember this:

Pulse-PPG = Field PPG data + Learnable motif similarity + Relative contrastive learning.

### Lesson 1 — Check your understanding

Before we move forward, let's check whether the foundational concepts are clear.

Knowledge check

0/4 answered

Question 1. What does PPG measure?

Electrical activity of the brain

Changes in blood volume using optical measurements

Body temperature

Muscle electrical activity

Question 2. Why might a model trained on clinical PPG perform poorly on smartwatch data?

Smartwatches cannot measure PPG

The model has too few layers

Clinical and field signals have different data distributions

PPG contains no physiological information

Question 3. What is the primary purpose of a foundation model?

Solve only one specific task

Learn reusable representations for multiple downstream tasks

Remove every noisy measurement

Replace all wearable sensors

Question 4. Why do Pulse-PPG authors preserve noisy field signals?

Noise always improves accuracy

Noise can contain contextual information and realistic variability

Filtering is mathematically impossible

Their model does not use raw signals

Check my answers

### 6\. What should you remember from Lesson 1?

You should now understand these five concepts:

| Concept          | Meaning                                            |
| ---------------- | -------------------------------------------------- |
| PPG              | Optical measurement of blood-volume changes        |
| Domain shift     | Difference between training and deployment data    |
| Foundation model | A model learning reusable representations          |
| Pre-training     | Initial learning from a large dataset              |
| Downstream task  | A specific application using the pre-trained model |

These concepts establish the motivation and foundation of the paper. arXiv +1

### 7\. A little preparation for Lesson 2

We'll need some knowledge of these topics:

* CNN and ResNet

* Self-supervised learning

* Contrastive learning

* Attention mechanisms

* Time-series representation learning

Don't worry if you don't know them yet. I'll explain each when we encounter it.

One question before we continue:

What is your current background in machine learning?

1\. Your machine learning experience

Beginner — I know basic ML concepts

Intermediate — I know CNNs, RNNs, and deep learning

Advanced — I have research experience in deep learning

2\. Your mathematical background

Basic — algebra and basic calculus

Some — linear algebra, calculus, probability

Strong — comfortable with mathematical derivations

3\. Your main goal

Understand the paper for research

Implement the model using PyTorch

Reproduce the experiments

Develop a new research idea based on this paper

Continue to Lesson 2

My teaching approach will be: intuition → technical explanation → mathematics → paper-specific implementation → critical thinking.

We'll take our time. The goal isn't to finish reading the paper quickly; it's to genuinely understand the research.

7

7

7
