### Lesson 6 — Experimental Results: Does Pulse-PPG Actually Work?

Welcome to one of the most important lessons.

So far, we've understood the motivation, methodology, mathematics, and training process. Now we need to answer the question that matters most in research:

Does the proposed method actually work, and does the experimental evidence support the authors' claims?

We'll examine the paper's four main experiments, reconstruct the important results, and identify opportunities for a follow-up publication.

Our source is Section 6 of the paper, including Tables 2 and 3 and Appendix Tables 6–9.

[Open the experimental results](https://arxiv.org/html/2502.01108v2?utm_source=chatgpt.com#sec-experimental-results).

### Part 1 — Understand the experimental design

The authors conduct four major experiments.

* Experiment 1 — Pulse-PPG vs. PaPaGei

    Does field-trained PPG representation learning outperform an existing PPG foundation model?

* Experiment 2 — General time-series foundation models

    How does Pulse-PPG compare with Chronos, MOMENT, and supervised baselines?

* Experiment 3 — Field-to-lab generalization

    Does pre-training on noisy wearable data help with clean laboratory and clinical applications?

* Experiment 4 — Downstream use cases

    How well does Pulse-PPG perform across its eleven specific downstream tasks, using linear probing and fine-tuning?

The five evaluation datasets are:

| Dataset   | Environment    | Main tasks                               |
| --------- | -------------- | ---------------------------------------- |
| MOODS     | Wearable field | Stress, activity                         |
| PPG-DaLiA | Wearable lab   | Heart rate, activity                     |
| WESAD     | Wearable lab   | Stress                                   |
| SDB       | Clinical       | Sleep disturbance                        |
| PPG-BP    | Clinical       | Blood pressure, heart rate, hypertension |

There are eleven downstream tasks in total.

An important distinction: the first three experiments mainly investigate the quality of frozen representations, while Experiment 4 also investigates task-specific fine-tuning.

arXiv +1

### Part 2 — Experiment 1: Pulse-PPG vs. PaPaGei

### 2.1 Why is PaPaGei an important baseline?

![Frontiers | Analysis on Four Derivative Waveforms of Photoplethysmogram (PPG) for Fiducial Point Detection](https://images.openai.com/static-rsc-4/FiqjXrL0aEaBn2YqrcOIHRaPbZBkmaZXlBEhAv0XDRjit7ogepQaPoMxPcUAuSm5ewMTYYO-6cUYXEh7nkkD4x6Hzyp_cHBU88UM2MynDc1noA9fscESU7woPgrGGj36DQBFNdCqPi2K5SsN5OpSjbmsMmBCPv23t14yxZSJmONSisQzeOefDNXiOPxvyzJb?purpose=fullsize)

PaPaGei

An open-source PPG foundation model trained on clean clinical PPG signals.

It is an important comparison because it learns representations for the same physiological signal modality.

The authors compare:

* Pulse-PPG: field-trained.

* PaPaGei: clinical-data-trained.

Both produce 512-dimensional embeddings.

Both are evaluated using linear probing.

This is important because the encoder weights are frozen during evaluation. The comparison therefore focuses on the usefulness of the learned representations rather than the capacity of a downstream deep network.

### 2.2 The main result

10 out of 11 tasks

Pulse-PPG outperforms PaPaGei in 10 of the 11 downstream tasks.

The only exception is sleep disturbance.

Why?

MOODS participants were instructed to wear the smartwatch during waking hours. Consequently, Pulse-PPG did not receive sleep PPG during pre-training.

PaPaGei, in contrast, included sleep-study data in its pre-training.

This is a very useful scientific finding:

A foundation model's performance depends not only on its architecture, but also on whether its pre-training data contains the physiological conditions relevant to the downstream task.

### 2.3 Quantitative examples

The paper reports the following comparisons:

| Task                             | Pulse-PPG vs. PaPaGei      |
| -------------------------------- | -------------------------- |
| Wearable instant HR              | 6.28 lower MAE             |
| Wearable activity classification | Substantial F1 improvement |
| Field stress classification      | Better F1                  |
| Systolic BP regression           | About 0.5 lower MAE        |
| Diastolic BP regression          | About 0.5 lower MAE        |
| Average HR regression            | About 0.5 lower MAE        |
| Sleep disturbance                | PaPaGei performs better    |

Remember:

* Lower MAE is better.

* Higher F1 is better.

The wearable-task improvements are particularly interesting because noisy field PPG is generally more difficult to model than clean clinical PPG.

arXiv

### 2.4 A critical interpretation

Does this prove that relative contrastive learning is superior to PaPaGei's learning objective?

No.

Why?

Because two things change simultaneously:

* Pre-training dataset.

* Pre-training methodology.

The comparison alone cannot isolate the contribution of each.

This is a fundamental causal-inference issue in ML experiments.

To isolate the effects, we need controlled experiments.

For example:

| Experiment | Dataset  | Objective           |
| ---------- | -------- | ------------------- |
| A          | Clinical | Pulse-PPG objective |
| B          | Field    | Pulse-PPG objective |
| C          | Clinical | PaPaGei objective   |
| D          | Field    | PaPaGei objective   |

This is effectively a factorial experimental design.

It would let us estimate:

* Dataset effect.

* Objective effect.

* Dataset-objective interaction.

The authors conduct additional field-versus-clinical pre-training comparisons in Experiment 3, which help address this question.

### Part 3 — Experiment 2: Comparison with general time-series foundation models

This experiment asks:

Does a domain-specific PPG foundation model offer advantages over much larger general-purpose time-series foundation models?

The authors compare Pulse-PPG against:

![GitHub - amazon-science/chronos-forecasting: Chronos: Pretrained Models for Time Series Forecasting | Riccardo Gatti, PhD](https://images.openai.com/static-rsc-4/-YuSJRcYqYJKyxLGdz15wS_oUQV2doGBuS4RM-p-7Sp0oUuxbJ4u9VmQc6CtNdL8hoTkpGcEJJAO_htnYumQPpegQplNyLPMkXk3KHaTDkgwv89pILIrJGJL1Jyxwxu-e0dO6LyA-tE0xgVgkEOodjgvXR3m9HoGvNpJnPMqhVQLUNLdrqxB5Qm9aZaUssOI?purpose=fullsize)

Chronos

### 200M parameters

A general-purpose time-series foundation model.

![ICML 2024 时间序列（Time Series）和时空数据（Spatial-Temporal）论文总结【抢先版】-腾讯云开发者社区-腾讯云](https://images.openai.com/static-rsc-4/FuGS4dXnKK_U9hx1MVV_sJVRALVaBgkUDqbUGl9gZr2nuclF5YQjDIjaUo5R5NEYNCccCcDHGr6NbDNus_l8UT2EQcSmdUowbl1cN5IHYhiWfj_9sMctZ1LmGH1O9bBY2VcSi1j7uSTq672lvstYyTnQ9g698cCk8I0QeruiCVVvoVOopu0yrBVJnTZAEBHx?purpose=fullsize)

MOMENT

### 385M parameters

A general-purpose time-series foundation model.

![Frontiers | Residual and bidirectional LSTM for epileptic seizure detection](https://images.openai.com/static-rsc-4/eRVEXEBrf_iw9cw9v8lqynr3LSGBqKp7zI0ZrzwNEP-eeq-ZTrH6Ohz6HSlK19krXg2CARxFM-uba2MVy96zqtgMto9s2AwYRezmfp06oajXhaceVctF9VhXx8Lvq3T2MQzhTdsJg463YN8iMQMtvCLQsi8HM5oW883wT3jEHZ26jCpys852uS417fqX7C1Z?purpose=fullsize)

1D ResNet-26

A supervised baseline trained separately on downstream datasets.

Pulse-PPG has only 28.5 million parameters.

That is approximately:

* 7 times smaller than Chronos.

* 13.5 times smaller than MOMENT.

### 3.1 Compare average classification performance

Higher is better. Values are averages across classification tasks.

| Model             | F1     | Accuracy | AUROC  |
| ----------------- | ------ | -------- | ------ |
| Pulse-PPG         | 0.5870 | 0.6840   | 0.7481 |
| PaPaGei           | 0.4994 | 0.6361   | 0.6840 |
| Chronos           | 0.5845 | 0.6755   | 0.7329 |
| MOMENT            | 0.5456 | 0.6691   | 0.7241 |
| Supervised ResNet | 0.4623 | 0.6212   | 0.6224 |
| Random Forest     | 0.4152 | 0.5911   | 0.5977 |

Pulse-PPG achieves the best average F1 score.

But notice something interesting:

Chronos is very close.

0.5870-0.5845=0.0025

This is a difference of only 0.0025 in average F1.

We should not automatically interpret this as a statistically significant advantage.

The authors report mean and standard deviation across tasks, but a proper significance analysis would need paired task-level or participant-level comparisons.

### 3.2 Compare regression performance

Lower is better. Values are averages across regression tasks.

| Model             | MAE     | MSE      | MAPE   |
| ----------------- | ------- | -------- | ------ |
| Pulse-PPG         | 8.8593  | 145.255  | 0.1009 |
| PaPaGei           | 10.7488 | 204.6825 | 0.1288 |
| Chronos           | 9.1902  | 162.1719 | 0.1054 |
| MOMENT            | 8.5742  | 139.6036 | 0.0988 |
| Supervised ResNet | 17.2733 | 580.3867 | 0.1803 |
| Random Forest     | 12.5655 | 268.2220 | 0.1495 |

Here MOMENT outperforms Pulse-PPG on all three average regression metrics.

This is important.

The correct interpretation is:

* Pulse-PPG has the best average classification F1.

* MOMENT has the best average regression performance.

* Pulse-PPG remains competitive with substantially larger general-purpose models.

It would be incorrect to claim that Pulse-PPG is the best model on every metric.

arXiv

### Part 4 — Experiment 3: Does field pre-training improve laboratory performance?

This is arguably the most scientifically important experiment.

The authors want to test the following hypothesis:

H_1:
\\text{Field pre-training}
>
\\text{Clinical pre-training}

Not just on wearable field data, but also on laboratory and clinical downstream tasks.

### 4.1 Experimental design

The authors perform two controlled comparisons.

Comparison A — Pulse-PPG

Model A

Pre-trained on MOODS field PPG

Model B

Pre-trained on MIMIC-III clinical PPG

Same model architecture and training procedure.

Comparison B — PaPaGei

Model A

Pre-trained on MOODS field PPG

Model B

Pre-trained on clinical PPG

The authors also retrain PaPaGei using its original training procedure.

The clinical dataset used for Pulse-PPG pre-training contains:

* 151,738 PPG segments.

* Five-minute recordings.

* 100 Hz sampling.

* 18,210 patients.

The authors then evaluate both models with the same linear-probing pipeline.

This is a stronger design than simply comparing two independently developed models.

### 4.2 Results

10/11 tasks favor field-trained Pulse-PPG

The field-trained Pulse-PPG performs better than its clinical-pretrained counterpart on 10 of 11 downstream tasks.

Two especially interesting results are:

| Field downstream task | Improvement |
| --------------------- | ----------- |
| MOODS stress F1       | +0.0848     |
| MOODS activity F1     | +0.1218     |

The clinical downstream results also improve:

* Approximately 0.10 F1 improvement in hypertension classification.

* Approximately 1 MAE improvement in systolic and diastolic BP regression.

The sleep disturbance task remains the exception.

### 4.3 What about PaPaGei?

The same general pattern appears for PaPaGei, but with a smaller advantage.

Field-trained PaPaGei performs better than clinical-trained PaPaGei in 6 out of 11 tasks.

This is a particularly important observation.

It suggests that the benefits of field pre-training are not necessarily exclusive to the Pulse-PPG architecture.

The training-data distribution itself may play a substantial role.

arXiv

### 4.4 The deeper scientific interpretation

Let's separate two hypotheses.

Hypothesis A — Domain-matching hypothesis

Training on field PPG improves field performance because the model sees similar noise and acquisition conditions during pre-training.

P_{\\text{pretrain}}(X)
\\approx
P_{\\text{deployment}}(X)

Hypothesis B — General physiological diversity hypothesis

Field data contains a broader variety of motion, environmental conditions, and physiological responses.

Consequently, it may also improve performance on clean laboratory or clinical data.

The experiment supports both possibilities, but it does not completely separate them.

For a follow-up paper, I would design a dataset-controlled experiment that explicitly measures:

* Signal quality distribution.

* Activity distribution.

* Physiological state distribution.

* Participant diversity.

* Device diversity.

Then we could test which factors actually drive transfer performance.

### Part 5 — Experiment 4: How useful is Pulse-PPG for individual applications?

Now let's examine the actual downstream tasks.

The authors evaluate two settings:

* Linear probing (LP).

* Fine-tuning (FT).

The linear probe keeps the foundation encoder frozen.

Fine-tuning updates the complete network using task-specific data.

This gives us a way to assess both general-purpose representations and downstream adaptability.

### 5.1 The most interesting individual results

F1 for classification and MAE for regression.

| Task                       | Naive  | Linear probe | Fine-tuned |
| -------------------------- | ------ | ------------ | ---------- |
| PPG-DaLiA instant HR MAE   | 19.34  | 8.936        | 3.705      |
| PPG-DaLiA activity F1      | 0.0455 | 0.3039       | 0.3648     |
| WESAD binary stress F1     | 0.4065 | 0.8759       | 0.9392     |
| WESAD four-class stress F1 | 0.1496 | 0.5431       | 0.5582     |
| MOODS binary stress F1     | 0.3859 | 0.5398       | 0.5872     |
| MOODS activity F1          | 0.4574 | 0.6859       | 0.7992     |
| SDB sleep disturbance F1   | 0.3945 | 0.4630       | 0.5782     |
| PPG-BP hypertension F1     | 0.4459 | 0.6975       | 0.7213     |

The most striking result is WESAD binary stress detection:

F1_{\\text{LP}}=0.8759F1_{\\text{FT}}=0.9392

This indicates that the frozen representations already contain substantial information useful for the task.

Fine-tuning improves performance further.

### 5.2 Why does fine-tuning help more on some tasks?

Consider instantaneous heart-rate estimation on PPG-DaLiA:

MAE_{\\text{LP}}=8.936MAE_{\\text{FT}}=3.705

The error decreases substantially.

But for systolic blood pressure:

MAE_{\\text{LP}}=13.62MAE_{\\text{FT}}=12.33

The improvement is smaller.

One explanation proposed by the authors is the difference in downstream data availability.

PPG-DaLiA contains approximately 1,545 subject-minutes, whereas PPG-BP contains only approximately 36.5 subject-minutes.

More task-specific data can provide more opportunities for the network to adapt.

But remember: this is an interpretation, not proof that sample size alone explains the difference.

Other factors include label quality, task difficulty, physiological variability, and the relationship between PPG and the target variable.

arXiv +1

### Part 6 — Additional experiments: What do the ablations tell us?

The appendix contains two especially useful experiments.

### 6.1 Experiment 5: Is the advantage just because Pulse-PPG is larger?

This is an important fairness question.

Original Pulse-PPG:

28.5\\text{ million parameters}

PaPaGei-S:

5.7\\text{ million parameters}

Could Pulse-PPG win simply because it is larger and receives longer input sequences?

The authors investigate this by creating Light Pulse-PPG.

| Model              | Parameters | Input duration |
| ------------------ | ---------- | -------------- |
| Original Pulse-PPG | 28.5M      | 4 minutes      |
| Light Pulse-PPG    | 4.73M      | 10 seconds     |
| PaPaGei-S          | 5.7M       | 10 seconds     |

This is a much fairer comparison of model scale and input context.

The authors report that Light Pulse-PPG outperforms PaPaGei across all the average performance metrics in their comparison.

Important finding

This strengthens the argument that the field pre-training strategy contributes meaningful value beyond simply using a larger network.

However, it does not completely isolate the effect of the pre-training objective because the two models still use different learning methods.

arXiv

### 6.2 Experiment 6: Input-window ablation

The authors compare different input-window durations and normalization configurations.

Here are some average results.

| Configuration         | Classification F1 | Classification AUROC | Regression MAE |
| --------------------- | ----------------- | -------------------- | -------------- |
| 4 min, normalized     | 0.5870            | 0.7481               | 8.8593         |
| 1 min, normalized     | 0.5851            | 0.7441               | 8.9284         |
| 2 min, normalized     | 0.5800            | 0.7342               | 9.1154         |
| 1 min, not normalized | 0.5620            | 0.7136               | 9.0028         |
| 2 min, not normalized | 0.5671            | 0.7365               | 9.3761         |

The authors conclude:

* Normalization consistently improves performance.

* Four-minute input windows produce the best overall average results.

Notice that the differences between four-minute and one-minute windows are relatively small in some metrics.

We should not claim that four minutes is dramatically better for every task.

### Research interpretation

This suggests a potential opportunity for multi-scale pre-training.

Instead of choosing a single duration, we could train a model using multiple temporal contexts:

X^{(5s)},\\quad X^{(30s)},\\quad X^{(240s)}

The model could learn:

* Short-term pulse morphology.

* Medium-term physiological variation.

* Long-term contextual dynamics.

This could potentially improve both real-time inference and long-context physiological modeling.

### Part 7 — What do the results actually prove?

Let's now critically assess the evidence.

I want you to distinguish between three levels of scientific claims.

Strongly supported by the experiments

Claim 1: Field-trained Pulse-PPG learns useful representations.

Evidence: Its frozen embeddings achieve competitive performance across multiple wearable and clinical downstream tasks.

Supported by controlled comparisons

Claim 2: Field pre-training can improve generalization over clinical pre-training.

Evidence: The authors retrain Pulse-PPG and PaPaGei with different pre-training datasets and observe benefits on many downstream tasks.

Not fully established

Claim 3: Motif-based relative contrastive learning is the primary reason for the improvements.

Evidence: The overall model performs well, but fully isolating the learning objective from data characteristics requires more controlled ablations.

### 7.1 Five limitations in the experimental evidence

1\. Limited independent participants

The pre-training dataset contains 120 participants. A very large number of windows does not eliminate uncertainty about population generalization.

2\. Limited field stress evaluation

The authors explicitly acknowledge that the MOODS field stress labels rely on a commercial pre-trained model used to obtain self-reported stress ratings. Additional independent field datasets would strengthen this result.

3\. Demographic information

Race and ethnicity were not collected, and skin-tone-related differences in optical PPG measurement were not explicitly investigated.

4\. Missing modalities

No accelerometer is used in the foundation-model pre-training, even though motion is an important source of PPG artifacts.

5\. Deployment constraints

The authors do not demonstrate a complete battery-powered, low-latency wearable implementation.

arXiv +1

### 7.2 An important clinical interpretation

The PPG-BP experiment should not be interpreted as proving that Pulse-PPG can independently diagnose hypertension or reliably replace a validated blood-pressure monitor.

It shows that the representation can support a downstream prediction task on that dataset.

Clinical validity requires additional evidence, including independent prospective evaluation, calibration, measurement-error analysis, and appropriate comparison against validated reference measurements.

This distinction is essential when developing physiological foundation models.

### Part 8 — My research assessment

Let's rank possible extensions based on how directly they address the paper's findings.

| Research direction          | Motivation                      | Potential |
| --------------------------- | ------------------------------- | --------- |
| Sleep-aware pre-training    | Weakness on sleep disturbance   | High      |
| PPG + accelerometer         | Motion-related confounding      | Very high |
| Multi-scale pre-training    | Single four-minute context      | High      |
| Temporal-order-aware motifs | Local motif matching            | High      |
| Demographic robustness      | Limited demographic evaluation  | Very high |
| Efficient edge deployment   | No demonstrated on-device model | High      |

My strongest recommendation is to investigate motion-aware, temporally structured representation learning.

Here's why:

* It directly builds on the motif-distance mechanism.

* It addresses a known challenge in field PPG.

* It introduces a testable learning objective.

* It enables meaningful ablation studies.

* It can be evaluated on cross-subject and cross-device generalization.

A potentially interesting hypothesis would be:

H_1:
\\text{Motion-aware temporal representations}
>
\\text{PPG-only motif representations}

But the evaluation must demonstrate that improvements come from physiological robustness, rather than simply learning activity labels from accelerometer data.

### Part 9 — Advanced research assessment

Try answering these as if you were defending the paper in a research seminar.

Lesson 6 research assessment

0/5 answered

1. Why is the 10/11 result against PaPaGei not sufficient to establish that Pulse-PPG's learning objective is superior?

The models use different datasets and learning objectives

PaPaGei has no encoder

Both models use exactly the same pre-training data

The evaluation contains no downstream tasks

2. Which model has the best average regression MAE in Experiment 2?

Pulse-PPG

PaPaGei

Chronos

MOMENT

3. Why does PaPaGei perform better on sleep disturbance?

It has more parameters than every model

Its pre-training included sleep-study data

It uses accelerometer signals

Pulse-PPG was trained using sleep labels

4. What does Experiment 3 establish most directly?

Every noisy signal is better than every clean signal

Field pre-training can improve transfer compared with clinical pre-training

The motif network is statistically optimal

The largest model always wins

5. What is the most important weakness in the field stress evaluation?

No PPG signals were collected

The labels rely on a commercial pretrained model and self-reported stress ratings

The task has no validation set

The model was not fine-tuned

Submit answers

### What comes next — Lesson 7

Next lesson

### Discussion, Limitations, and Identifying a Publishable Research Gap

![AI in Doctoral Research: University of Phoenix Study — The AI Chronicle](https://images.openai.com/static-rsc-4/0gLX-DFn7dQ5Tlfs-ru3HGvfMTY4dfR-0cZc2DVvXxL98pqLdZdiaD8-vQ6Qr_Q-I2csnoEgg5HjpL84y6edqeDYSu-E-G2I8ga-nSdbrJldxgmYxvUqPMNzTiAO3qfT0hyKdGuITVcc1b0m0JFHHqmJz-pSMaVv2sxh8foq805-NCGiDBksHn-kgI-ER9hP?purpose=fullsize)

We'll investigate:

* The authors' interpretation of their results.

* What the paper genuinely contributes to PPG foundation modeling.

* Which conclusions are supported by experiments and which remain hypotheses.

* The five most important unresolved scientific questions.

* How to formulate a novel research hypothesis.

* How to design baseline comparisons and ablation studies.

* How to turn a research extension into a potential publication.

Final goal: Develop a technically defensible research proposal inspired by Pulse-PPG.

### One question to think about before Lesson 7

Suppose you have enough GPU resources to conduct only one major experiment.

Which would you investigate first?

Integrate accelerometer information to distinguish motion artifacts from physiology.

Improve motif matching with temporal-order constraints.

Introduce multi-scale temporal representation learning.

Add sleep PPG to improve physiological coverage.

Investigate demographic and skin-tone-related generalization.

Use this for Lesson 7

Research principle: Don't aim to make Pulse-PPG more complicated. Aim to discover something the original model cannot explain or handle, and then design an experiment that convincingly demonstrates your solution.

Original paper: [Pulse-PPG — Section 6, Experimental Results](https://arxiv.org/html/2502.01108v2?utm_source=chatgpt.com).
