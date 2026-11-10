### Lesson 5 — Training Pulse-PPG: Dataset, Experimental Design, and Reproducibility

Now we're moving from mathematical theory to experimental science.

This lesson is particularly important for your research goal because a model's performance depends on more than its architecture or loss function.

We need to understand:

* Where the training data came from.

* How the authors prepared the data.

* How they prevented participant leakage.

* How they selected hyperparameters.

* How they trained the two networks.

* How they evaluated the foundation model.

* Whether the experiments support the paper's claims.

* How to reproduce and extend the experiments.

A correction to our earlier lessons: The paper's final reported foundation-model training ran for 6 epochs, although its hyperparameter-search configuration specified 20 epochs. The distance network was trained for 20 epochs. We will distinguish the search configuration from the final training run throughout this lesson.

Our primary references are Sections 4 and 5 of the original paper.

[Open the complete Pulse-PPG paper](https://arxiv.org/html/2502.01108v2?utm_source=chatgpt.com).

### Part 1 — Understanding the MOODS dataset

### 1.1 What is MOODS?

MOODS stands for:

Mobile Open Observation of Daily Stressors.

It is the real-world wearable dataset used to pre-train Pulse-PPG.

![Main Home - nbchealthcare](https://images.openai.com/static-rsc-4/-iPjyZePi0jYfAgRFBls_Drxu8OitWEypd5OCMhXIVvOLIMHTG-Kw3zwNOqT77UmH9GaesiBLiBIbZA4kUPN66nuVXvXd9Z7oA9MF305POZRf196Fih5XJAPkRZA46UKNBqzH3n6Oo1sFWMpG2rtv0rMvH7Zrkw85l7Wp1loU8dDtBdvItZZhXhLG6dBSyvu?purpose=fullsize)

![Qué hacer si el Apple Watch no mide bien las pulsaciones](https://images.openai.com/static-rsc-4/OonJfm9qodUZe02MpQ26wScr5B92c2o4WiyIOEXOdCTdQ3PXXeaFdFNldzRDL70CMrB1bTCv077ZV_Gh1MuA7SAfXj1s7VFLbybvTVXSV77xC31VqzpvWK_TobNaDfiF3Yiv-mkrS8DWGfImGrHruUnejEOGzM5YEFYeKfISWwEC4Hwxk9Fs-cjVAbeozcNj?purpose=fullsize)

![Young Healthy Woman Exercising Outdoors with Smartwatch, Staying Fit and Active in Nature](https://images.openai.com/static-rsc-4/22KhOAkEE8WOMbm4rsgbs9v3JNckUQ-wdaUeot-M7WJijAESRtobLJppPzj0gVDgzEE5RRDMNFkVUKz4wXZ_tgG__ia7wHtCM7l3Wo3TlhZqyJ593dO-P_ME26DvNvxEDCmM9Fy3w9CAVQUD97J7HhqDXy55Z017_2Nic8cSBQcoivkPgYN3VagM4z-YK3HL?purpose=fullsize)

The participants wore Fossil Sport smartwatches during everyday life.

The objective was to collect physiological signals in natural environments rather than only under controlled laboratory conditions.

Here are the important statistics.

### 120

Participants with PPG

From 122 enrolled participants

### 100

Days

Maximum study duration

### 822,247

PPG segments

Four-minute segments

### 55K

Hours

Approximately raw PPG recording

Additional demographic information:

| Attribute              | Participants |
| ---------------------- | ------------ |
| Men                    | 39           |
| Women                  | 77           |
| Non-binary             | 6            |
| Average age            | 38 years     |
| Age standard deviation | 13 years     |

The paper reports approximately 200 million seconds of raw PPG data.

Let's verify the magnitude:

55,000\\times3600
=
198,000,000\\text{ seconds}

This is approximately 198 million seconds, consistent with the paper's rounded figure of 200 million.

Research observation: 55,000 hours sounds enormous, but the dataset contains only 120 participants with PPG recordings.

This distinction will become important when we discuss generalization to unseen people.

arXiv

### 1.2 Why is this dataset scientifically interesting?

Traditional clinical PPG datasets are often collected under relatively controlled conditions.

MOODS captures:

* Daily physical activities.

* Changing sensor contact.

* Motion artifacts.

* Environmental variations.

* Different physiological states.

* Within-person temporal variability.

The authors hypothesize that these variations can help a foundation model learn representations that generalize to real-world applications.

However, we must distinguish two types of information:

X=X_{\\text{physiology}}+X_{\\text{artifact}}+X_{\\text{environment}}

This is a conceptual decomposition, not an exact additive physical model.

The challenge is determining which variations are useful and which are nuisance factors.

That is a central research question for your future extension.

### Part 2 — Data preprocessing

This section contains several important experimental decisions.

### 2.1 Sampling frequency

The original MOODS PPG recordings were collected at:

f_s=100\\text{ Hz}

The authors resample them to:

f_s'=50\\text{ Hz}

This means:

100\\text{ samples/second}
\\rightarrow
50\\text{ samples/second}

The Nyquist frequency after resampling becomes:

f_N=\\frac{50}{2}=25\\text{ Hz}

The original signal's content above the new Nyquist frequency must be appropriately handled during resampling to avoid aliasing.

Do not confuse resampling with simply deleting every other sample.

A proper resampling operation includes appropriate anti-alias filtering.

### 2.2 Four-minute input windows

The authors use four-minute windows.

Let's calculate their length.

T=240\\times50\\boxed{T=12,000}

Therefore, every training example has 12,000 samples.

One training example

### 12,000

PPG samples

50 samples per second × 240 seconds

0 minutes

4 minutes

The authors segment the recordings into non-overlapping four-minute windows.

Why four minutes?

The authors want to capture both:

* Micro-level changes: transient waveform morphology.

* Macro-level changes: sustained physiological responses.

For example, stress-related heart-rate and HRV dynamics can evolve over several minutes.

The paper reports that four-minute windows generally outperform the one- and two-minute alternatives in its input-window ablation study.

This does not establish that four minutes is optimal for every PPG application.

It is optimal within their investigated experimental setting.

### 2.3 No signal-specific filtering

This is one of the most important design decisions.

The authors deliberately avoid conventional signal-specific filtering.

Why?

They want the model to learn from the natural variability of field signals.

However, they do not leave the signal completely unprocessed.

They apply global person-specific z-normalization.

The normalization is conceptually:

X'_{s}(t)
=
\\frac{X_s(t)-\\mu_s}{\\sigma_s}

where:

* identifies the participant.

* is that participant's global mean.

* is that participant's global standard deviation.

This addresses differences in signal scale between participants.

Important experimental question: If person-specific normalization uses statistics computed across a participant's complete recording, what information is available when deploying the model on a genuinely unseen user in real time?

This is worth investigating carefully. For a realistic online deployment, normalization statistics may need to be estimated from calibration data or updated causally.

### Part 3 — Subject-wise data splitting

This is perhaps the most important experimental design decision in the paper.

### 3.1 The split

The authors randomly divide the 120 participants into:

| Split      | Participants |
| ---------- | ------------ |
| Training   | 84           |
| Validation | 18           |
| Test       | 18           |
| Total      | 120          |

Subject-wise partition

Train: 70%

Validation: 15%

Test: 15%

Why not randomly split the PPG windows?

Imagine participant A contributes 10,000 segments.

If you randomly split windows:

* 7,000 may go into training.

* 1,500 may go into validation.

* 1,500 may go into testing.

The model has already encountered the same participant during training.

It may learn participant-specific patterns.

Consequently, test performance can be overly optimistic when the intended deployment population consists of unseen users.

Subject-wise splitting avoids this particular leakage.

### 3.2 The subtlety: Pre-training test set versus downstream test set

The authors deliberately preserve 18 participants as a held-out test group.

This matters because MOODS is used both for foundation-model pre-training and for downstream evaluation of stress and activity.

The held-out participants are not used during pre-training, protecting the downstream test from representation-learning exposure.

This is good experimental practice.

But it also raises another question:

Are all downstream datasets evaluated under participant-independent splits?

We must inspect each evaluation protocol separately rather than assuming that the pre-training split automatically guarantees leakage-free evaluation everywhere.

arXiv

### Part 4 — How did the authors train the two networks?

Remember: Pulse-PPG has two separate training stages.

We need to understand their hyperparameters independently.

### 4.1 Stage A: Training the motif-distance network

127K parameters

The authors train the distance function using masked reconstruction.

The hyperparameter search explores:

| Hyperparameter      | Values explored                     |
| ------------------- | ----------------------------------- |
| Kernel size         | 5, 11, 15, 21, 60, 120              |
| Embedding dimension | 32, 64, 128                         |
| Learning rate       | 0.001, 0.0001                       |
| Receptive field     | Different depths and configurations |

The selected configuration:

| Parameter              | Final configuration |
| ---------------------- | ------------------- |
| Kernel size            | 15                  |
| Feature dimension      | 64                  |
| Double receptive field | 5                   |
| Epochs                 | 20                  |
| Learning rate          | 0.001               |
| Batch size             | 16                  |
| Subsampling stride     | 10                  |
| Optimizer              | Adam                |

Why did they choose these values?

Their experiments suggest:

* Small kernels and shallow receptive fields fail to capture sufficient temporal context.

* Excessively large receptive fields can over-smooth the signal.

* The selected configuration balances local motif extraction with broader temporal context.

The distance network takes approximately 10 hours to train.

### 4.2 Stage B: Training the foundation encoder

28.5M parameters

The authors use a 1D ResNet-26.

The hyperparameter search explores:

* Kernel sizes: 9, 11, 15.

* Initial filter sizes: 32, 64, 128.

* Strides: 1, 2, 5, 10, 15, 20.

* Residual blocks: 4, 8, 12, 16.

* Same-user candidate counts: 1, 5, 10, 15.

* Pooling: mean or max.

* Learning rates: 0.001 and 0.0001.

The selected configuration is:

| Parameter                      | Selected value |
| ------------------------------ | -------------- |
| Backbone                       | 1D ResNet-26   |
| Initial filters                | 128            |
| Kernel size                    | 11             |
| Initial stride                 | 2              |
| Residual blocks                | 12             |
| Final pooling                  | Max            |
| Epochs in search configuration | 20             |
| Learning rate                  | 0.0001         |
| Batch size                     | 64             |
| Optimizer                      | Adam           |
| Embedding dimension            | 512            |

The authors found that deeper models could perform slightly better on training subsets but generalize poorly to held-out field data.

This is a classic overfitting problem.

### Why did they choose max pooling?

Consider a feature map:

H\\in\\mathbb R^{T'\\times D}

Mean pooling computes:

z_d^{\\text{mean}}
=
\\frac{1}{T'}
\\sum_{t=1}^{T'}H_{t,d}

Max pooling computes:

z_d^{\\text{max}}
=
\\max_t H_{t,d}

Mean pooling summarizes average activation.

Max pooling preserves the strongest activation for each feature.

The authors report that max pooling produces more discriminative embeddings in their experiments.

Research question: Could attention pooling outperform max pooling by learning which temporal regions are important instead of always selecting the maximum?

That is a reasonable ablation experiment.

### 4.3 The actual final training run

Here is the distinction that is easy to miss.

The hyperparameter-search configuration lists 20 epochs for the foundation encoder.

But the final reported training procedure stopped after six epochs.

| Model                  | Training duration      | Epochs |
| ---------------------- | ---------------------- | ------ |
| Motif-distance network | Approximately 10 hours | 20     |
| Foundation model       | Approximately 5 days   | 6      |

The foundation model was trained on an NVIDIA L40S GPU.

The paper reports:

* 606,833 unique four-minute segments per epoch.

* Approximately 5,424 participant-days per epoch.

* Approximately 20 hours per epoch.

* Adam optimizer.

* Learning rate of 0.0001.

* Betas of (0.9, 0.999).

* No weight decay.

* Batch size of 64.

Why stop at six epochs?

The authors cite:

* Convergence of pre-training loss.

* Diminishing downstream performance improvements.

* Computational efficiency and reduced carbon footprint.

This is a good example of practical research engineering: more epochs do not automatically mean better representations.

arXiv

### Part 5 — How did they evaluate the model?

A foundation model cannot establish its value through training loss alone.

It must demonstrate that its learned representations transfer to different tasks and datasets.

The authors evaluate five downstream datasets and eleven tasks.

### 5.1 The five datasets

![Fossil FTW4021 Smartwatch User Manual](https://images.openai.com/static-rsc-4/bljIp4Jp776Y-YrmR-Q0rlvlLv_giFsoUohDBWULnp9Uz4dOMgUhZnEpm7hy-usGvsxijoaN5ll9nI_bPDzAtPu-xG-wcyJCoW7bs2oSF6um0xHIMCEw2MPERJB8YqJ17rvNSPkxjuD8YlwMt0Le0viZOlutQkL1arH04G6SAd9oT6h99HW9cVSXPIXi_f8B?purpose=fullsize)

MOODS

Wearable field

120 participants with PPG; real-world stress and activity recognition.

![Wearable Photoplethysmography Devices | Peter Charlton](https://images.openai.com/static-rsc-4/9n5J3iX43-YINPQW1mgjPjgrvIUs7hnJPQ7fbSUZHTGd3obJPoTtoIVug9ZT3yOEOEngX5yaX6PP7g0lBnqyJOUFoccDxAZ0YPlJAUwbxRL7P8fcQbpqr5LsoBqHkNEQWko71ha71Uy9OEQElTRogFnmetH7YmD6JM2_dLhXIINYROA5WhozT30QJdbg9kfh?purpose=fullsize)

PPG-DaLiA

Wearable laboratory

15 participants; instantaneous heart-rate regression and nine-class activity recognition.

![PPT - Addressing Stress and Addictive Behavior in the Natural Environment Using AutoSense PowerPoint Presentation - ID:3306204](https://images.openai.com/static-rsc-4/qPaBON52gBrE5BoEz9g-8KKoirqZ1mMGTeEfPgNsOXOpbQekS4fkLk8PbB520ctKOZsHrCo5LR0EqMol7Ckomq1QyLlNBmVl86P44XyqWm1jLYXdsRtpj8YElyU75CgHpdX8maUgDEUfIc8w369Cc3lqEH1TLbx-5xeqwZbOxy0kRmHK-tRRbg4t2sXyX4Pz?purpose=fullsize)

WESAD

Wearable laboratory

15 participants; binary and four-class stress recognition.

![Patient in hospital bed with pulse oximeter monitoring vital signs](https://images.openai.com/static-rsc-4/4UqmAFLpwSJ77IjwUVSH_dVm1aQCGA6_TAI8_f1zkGYtXraee3DYhF5QWQkrBcT-q8cUNNDOon1PC4jtigYDTKQlxwdK_-a2_pM_0iY3hjlToVRUT0ijYgCwuxFItP4mpGmzPiQeP4Non1-jH0t-Q7LQU_ymuwXr2ek3kkxx4m4u56cPsBCsGjgUnP3atD-Y?purpose=fullsize)

SDB

Clinical

146 participants; sleep disturbance classification.

![Normal heart function on pulse oximeter pleth graph bar on monitor display](https://images.openai.com/static-rsc-4/3Hq9bjVFOKKNbXwq3wm71eso3E9qn9nn4zNQZ7wXtEX4hL5Wy0kbafC1mIUaACoY1zGwrQix4fkTdvX_S1cubP27jQeZNkysyzwMHnjRCVNUtrcISJwF8r3RFXYJ1x5YWH9mzLxMabu5ODi870cERNMpCua0BU6Ko5Y0VPh2nFt-vH1lmaC6B99bEfzrOx_h?purpose=fullsize)

PPG-BP

Clinical

219 participants; systolic BP, diastolic BP, average heart rate, and hypertension.

The dataset table in the paper provides these subject counts and tasks. arXiv

### 5.2 Two evaluation strategies

This distinction is extremely important.

A. Linear probing

The foundation model is frozen.

Only a simple downstream model is trained on its embeddings.

z=f_\\theta(X)\\hat y=Wz+b

For classification, they use logistic regression.

For regression, they use regularized linear regression.

This evaluates how useful the pretrained representations are without modifying them.

B. Fine-tuning

The foundation encoder is updated using downstream labels.

\\theta^\*
=
\\arg\\min_\\theta
\\mathcal L_{\\text{task}}

This evaluates how useful the pretrained model is as an initialization for a specialized application.

| Property  | Linear probe           | Fine-tuning                 |
| --------- | ---------------------- | --------------------------- |
| Encoder   | Frozen                 | Trainable                   |
| Labels    | Downstream labels      | Downstream labels           |
| Compute   | Lower                  | Higher                      |
| Tests     | Representation quality | Adaptability                |
| Main risk | Underfitting the task  | Overfitting downstream data |

One important point: high fine-tuning performance does not necessarily mean the foundation representation is excellent. The model might learn much of the task during fine-tuning.

For evaluating representation quality, linear probing is particularly informative.

### 5.3 Evaluation metrics

For regression:

MAE=\\frac{1}{N}\\sum_i|y_i-\\hat y_i|MSE=\\frac{1}{N}\\sum_i(y_i-\\hat y_i)^2

For classification:

* Accuracy

* Precision

* Recall

* Macro F1

* AUROC

* AUPRC

Why macro F1?

Because some physiological classes may have substantially fewer examples than others.

Macro F1 gives equal importance to each class's F1 score:

F1_{\\text{macro}}
=
\\frac{1}{C}
\\sum_{c=1}^{C}F1_c

This prevents a dominant class from hiding poor performance on minority classes.

### Part 6 — Reproducibility: Can we independently reproduce this paper?

Now let's think like someone preparing a research replication.

The authors provide their model weights and code.

Official Pulse-PPG repository

Model implementation, training code, and released weights.

Open GitHub repository

For a serious reproduction, I would organize the work into these stages.

* Reproduce preprocessing

    Verify 100 Hz to 50 Hz resampling, four-minute windows, person-specific normalization, and non-overlapping segmentation.

* Reproduce motif-distance training

    Implement the five-block dilated convolution network and masked reconstruction objective.

* Verify distance behavior

    Test whether the distance function identifies reasonable motif matches on synthetic and real PPG examples.

* Reproduce candidate sampling

    Reconstruct within-subject and between-subject candidate selection.

* Train the foundation model

    Implement ResNet-26 and relative contrastive learning.

* Reproduce linear probing

    Evaluate frozen embeddings using the published downstream protocols.

* Reproduce fine-tuning

    Compare task-specific performance with the published results.

### Part 7 — Critical research evaluation

This is the most important section if you want to publish an extension.

I see seven questions worth investigating.

### 7.1 Dataset size versus participant diversity

The dataset has approximately 822,000 segments but only 120 participants with PPG.

A model can encounter hundreds of thousands of windows without encountering enough independent physiological variation.

Potential extension: Pre-train across multiple independent wearable datasets and evaluate on entirely unseen populations.

### 7.2 Subject-specific normalization and deployment

Person-specific normalization may use information from a participant's complete recording.

In real-world deployment, we might not have access to future recordings.

Potential extension: Compare:

* Global normalization.

* Calibration-based normalization.

* Causal running normalization.

* Adaptive normalization.

### 7.3 The absence of additional modalities

PPG is sensitive to motion artifacts.

But the model does not use accelerometer input during its foundation-model pre-training.

Potential extension: PPG + accelerometer contrastive learning.

This could help separate physiological changes from motion-related changes.

### 7.4 Four-minute windows may limit real-time applications

Four-minute input windows are useful for capturing longer physiological dynamics.

But applications such as instantaneous heart-rate estimation may require much shorter latency.

Potential extension: Multi-scale pre-training using 5-second, 30-second, and 240-second windows.

### 7.5 Limited demographic diversity

The dataset contains only 120 participants with PPG.

Its demographic distribution may not represent the diversity of the global wearable population.

Potential extension: Evaluate representation stability across age groups, skin characteristics, device types, and physiological conditions, with sufficient sample sizes and appropriate privacy protections.

### 7.6 Sleep generalization

The model performs worse on the sleep disturbance task than PaPaGei.

The authors explain this partly through the absence of sleep PPG in MOODS pre-training.

Potential extension: Include sleep and wake recordings in pre-training, then investigate whether the learned representation becomes more physiologically comprehensive.

### 7.7 Field robustness is not the same as noise robustness

This is a subtle but important distinction.

A model might learn to associate particular noise patterns with particular activities.

That does not necessarily mean it has learned robust physiological representations.

We should test whether its predictions remain stable when sensor noise changes independently of physiological state.

Potential extension: Controlled counterfactual artifact augmentation and cross-device testing.

These issues are closely related to the limitations identified in the paper's Discussion and Limitations sections. arXiv +1

### Part 8 — My recommended research extension

Given the technical structure of Pulse-PPG, I would investigate this:

Proposed research direction

### Multi-Scale, Motion-Aware Relative Contrastive Learning for PPG

Research problem

Pulse-PPG learns local motif similarities and relative relationships from field PPG, but does not explicitly use motion information or impose multi-scale physiological consistency.

Proposed changes

* Introduce multiple temporal resolutions.

* Add an accelerometer encoder.

* Separate physiological and motion representations.

* Retain motif-based relative contrastive learning.

* Evaluate on unseen subjects and devices.

Possible objective

\\mathcal L =
\\mathcal L_{\\text{RelCon}}
+\\lambda_1\\mathcal L_{\\text{multi}}
+\\lambda_2\\mathcal L_{\\text{cross}}
+\\lambda_3\\mathcal L_{\\text{invariance}}

Each additional term would need a carefully defined training signal and independent ablation.

Potential contribution: A more robust representation-learning framework for real-world wearable physiological signals.

I would not immediately combine all these ideas into one model. First establish which individual component produces measurable improvements.

### Part 9 — Your research assignment

I want you to answer these five questions as if you were preparing for a PhD research meeting.

Research assignment · 5 questions

1. Why is subject-wise splitting more appropriate than randomly splitting PPG windows?

2. Why did the authors avoid filtering the raw PPG signals but still apply person-specific normalization?

3. Why might a four-minute training window outperform a one-minute window for stress-related tasks?

4. What is the biggest limitation of using only 120 participants for foundation-model pre-training?

5. Which experiment would you design to establish that Pulse-PPG learns physiology rather than participant-specific noise?

Submit answers for research critique

### What comes next — Lesson 6

Next lesson

### Experimental Results: Does Pulse-PPG Actually Work?

![Nat. Biomed. Eng. | 基于深度对比学习的错义突变表型预测-腾讯云开发者社区-腾讯云](https://images.openai.com/static-rsc-4/PgHGAghynE94WnH-pNyeX7Sgna5m_eY-_qMRIeGuxrWGzi42lLOU9QTrkxntT908j77zFEp7jQ5gp5_hqbBxESuH5jHDUaiMYLgApoM93aiZxfHOfmZ7UUbfo1GErUTiqlf7-dScnHjHi4RYtaxhdZzhZyUL-mqU8s7c3RHd-Jfyi3ver32RIWSoEReZvMpp?purpose=fullsize)

We'll analyze the four major experiments:

* Pulse-PPG versus PaPaGei.

* Pulse-PPG versus Chronos, MOMENT, and supervised baselines.

* Field-to-lab generalization.

* Linear probing versus fine-tuning.

We'll also investigate:

* Why Pulse-PPG wins 10 out of 11 tasks.

* Why it loses on sleep disturbance.

* Which improvements are statistically and scientifically meaningful.

* Whether the experimental setup has potential confounders.

* Which results justify a new research direction.

Our objective: Learn to interpret the evidence, not simply accept the authors' conclusions.

One important principle to remember: A good research extension begins with a limitation demonstrated or plausibly exposed by the original experiments. It should not begin with a desire to add a more complicated architecture.

Original source: [Pulse-PPG, Sections 4–5 and Appendix](https://arxiv.org/html/2502.01108v2?utm_source=chatgpt.com).

9

9
