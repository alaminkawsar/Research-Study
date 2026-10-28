Your research idea is scientifically interesting, and the central concept is worth investigating: can we isolate the component of a PPG signal associated with glucose-related physiological changes by subtracting a baseline signal recorded under similar conditions?

The strongest part of your idea is that you are not trying to predict glucose directly from raw PPG alone. You want to first account for other factors, such as activity, and then use the remaining signal information to estimate glucose.

However, there is one important distinction: subtracting two PPG feature vectors does not automatically isolate the effect of glucose. Your method can work as a research hypothesis, but you will need to design the experiment and models carefully to test whether the difference contains glucose-related information rather than noise or other physiological changes.

### 1\. Your proposed mathematical model

Let's formalize your idea.

### Model A — Activity baseline

A = f_{\\theta}(X_{\\text{PPG}},\\,a)

Represent PPG features during activity , without a recent glucose challenge.

### Model B — Activity + glucose intake

B = g_{\\phi}(X_{\\text{PPG}},\\,a,\\,c)

Represent PPG features during the same activity , after glucose intake .

### Your proposed glucose-related feature

\\Delta = B-A

A difference vector that may contain information about glucose-related changes, alongside residual confounding and noise.

Here, denotes activity, and denotes glucose intake or the post-intake condition.

Your final step would be to learn a mapping from this difference vector to a reference glucose measurement:

\\widehat{G}=h_{\\psi}(\\Delta)

where is the glucose concentration measured using a glucometer.

That is a coherent research pipeline. The key question is whether the difference vector actually isolates glucose-related information.

### 2\. The most important scientific problem: how do you isolate glucose?

Imagine that you record PPG while a participant is standing still before and after drinking a glucose solution.

Even if the activity remains standing, PPG can change because of:

* Heart rate and blood pressure changes.

* Peripheral blood flow and skin temperature.

* Respiration and autonomic nervous system responses.

* Sensor pressure, placement, and contact quality.

* Time-dependent changes and measurement noise.

* The physiological response to eating or drinking that is not specific to glucose concentration.

Therefore, the difference is more accurately described as:

\\Delta_{\\text{observed}}
=
\\Delta_{\\text{glucose-related}}
+
\\Delta_{\\text{other physiology}}
+
\\Delta_{\\text{noise}}

Your objective is to determine how much glucose-related information is present in that difference.

Also, glucose intake and blood glucose concentration are not the same thing. The amount consumed does not uniquely determine the measured glucose level, and PPG may respond to physiological changes associated with glucose regulation rather than glucose molecules directly.

### 3\. How I would improve your proposed architecture

I would modify your approach slightly to make it more scientifically defensible.

### Step 1 — Collect PPG and contextual data

Record PPG windows alongside activity, heart rate if available, sensor quality, timestamps, and reference glucose measurements.

### Step 2 — Learn the expected baseline

Train a baseline model to predict PPG features expected under the current activity and physiological conditions, using data collected without a recent glucose challenge.

### Step 3 — Calculate the residual

Compare the observed post-intake PPG representation with the expected baseline representation.

r_t=z_t-\\widehat{z}_{0,t}

Here, is the observed feature vector, and is the predicted feature vector under the baseline condition.

### Step 4 — Estimate glucose

Learn a regression model using the residual, relevant contextual variables, and synchronized glucometer readings.

\\widehat{G}_t=h_{\\psi}(r_t,\\,a_t,\\,q_t)

Here, represents other measured covariates that may help explain the PPG signal.

This residual-based approach is a refinement of your original equation.

One crucial recommendation: use the same feature extractor for the baseline and post-intake PPG, or otherwise ensure the two feature spaces are explicitly aligned. If you train two independent neural networks to generate and , their embeddings might differ simply because the networks learned different representations.

Also, activity alone is insufficient to predict a unique baseline PPG feature vector. Your baseline model will likely need participant-specific information and relevant physiological covariates.

### 4\. Should you reduce the difference vector to a single value?

Not at the beginning.

Suppose the difference vector contains 64 features:

\\Delta\\in\\mathbb{R}^{64}

You could reduce it to one value using a learned projection:

s=w^\\top\\Delta

Then estimate glucose using:

\\widehat{G}=b_0+b_1s

This is a reasonable experiment, but reducing the vector to one scalar too early may discard useful information.

I recommend comparing three approaches:

| Approach        | Input to glucose estimator | Purpose                                 |
| --------------- | -------------------------- | --------------------------------------- |
| Baseline        | Original PPG features      | Establish a benchmark                   |
| Scalar residual | One learned value from     | Test your original hypothesis           |
| Vector residual | Full difference vector     | Preserve potentially useful information |

You can then test whether the residual representation improves prediction over raw PPG features and simpler baselines.

The regression relationship should be learned from paired observations, not assumed to be linear from the outset. A single scalar may be useful if the data support it, but a multivariable model might perform better.

### 5\. Which models should you investigate?

You mentioned two models: one to generate the baseline PPG features and another to generate the post-intake features. Here is how I would approach model selection.

![Oxymètre de pouls (Jean-Francois Mainguet)](https://images.openai.com/static-rsc-4/RVNcG81S3Urk_vFyr1J4fOSRZU2lHkK0QZB9BimPy1rkcL7S3DxzJg7pKe372gTcAoPK3iSd2-VPN-gxgyXswuSIw0rcn8kuC5xQBIb1pKfHNwb2lmdB0NGS_ac3Zu9AXSctKBs9MPeDPunagP-uwcO2JjeHTcpSUMdIhmmgV-3u1o3p5UXh8-lMUSbMfbEQ?purpose=fullsize)

A. Baseline feature model

Start with a model that predicts expected PPG features under a baseline condition.

* Linear regression or a generalized additive model as interpretable baselines.

* Random forest or gradient boosting for nonlinear relationships.

* Temporal CNN or LSTM if you need to learn from sequential PPG windows.

Its job is to estimate the baseline representation, not glucose.

![IEEE Xplore, delivering full text access to the world's highest quality technical literature in engineering and technology. | IEEE Xplore](https://images.openai.com/static-rsc-4/OaMTFSSq6WT8h_4NN-LhiUDD_0TUBi9NPV4_89GlGdG5MiyRDJu4ZJLEVTndQDn51MH_vGViVnhm-4m7Loe2hSUso12H9cG8afNo5ARlYuW2qOwuzr8IZ44ec-CFEH4kgrLBWxu2SWe_IGsGTmo5SxV8u2H9ZbPgBRB4o-0tESrxBcPOPrKi3GD4-bdKM4Qt?purpose=fullsize)

B. PPG feature extractor

Compare hand-engineered features with learned representations.

* Pulse amplitude, pulse width, pulse area, and waveform morphology.

* Frequency-domain features and beat-to-beat variability.

* A 1D CNN or another time-series encoder for learned features.

Apply the same extractor to baseline and post-intake recordings.

![Enhanced glucose forecasting using recurrent neural network and advanced feature engineering | Scientific Reports](https://images.openai.com/static-rsc-4/ClvFLFxshHY3pCHCVKZMD7IS5qqSvXzIG_Liyi-zIOsrsJaUDjNmcYuRwzOia8w9Vtb59ocTrZ5qYIL6u-uNNKtfZ33OsTuKWjdr_O9MlU9iug6o0J2WoxSg_7WtK6IElCyHO2XfdhBq5eAmvRYC2QH7sYaA6Nd9fsvlfKEorvDNonYMQbcOFE5wEhixXF9Q?purpose=fullsize)

C. Glucose estimation model

Compare linear regression, ridge regression, partial least squares (PLS), and gradient boosting. Start with simpler models because they make it easier to establish whether your proposed residual carries useful information.

These are candidate models to evaluate, not models whose accuracy can be guaranteed in advance.

### 6\. How should you design the experiment?

The experimental design will probably matter more than choosing an advanced neural network.

I would begin with a controlled, repeated-measures study.

* Baseline session: Record PPG during a defined activity before the glucose challenge.

* Glucose challenge: Record the intake time and amount, under an appropriate research protocol.

* Repeated measurements: Record PPG continuously or in defined windows, with synchronized reference glucose measurements at multiple time points.

* Control sessions: Collect comparable recordings without the glucose challenge to characterize ordinary temporal variation.

* Repeat across participants: Capture differences between individuals rather than relying on one person's response.

For the first experiment, choose one activity, such as sitting or standing still. Once you understand the results, extend the study to walking, sleep, or exercise. Sleep and exercise introduce additional challenges and should not be treated as interchangeable with a stationary baseline.

Use a research protocol with appropriate ethical oversight and clinical supervision, particularly if participants have diabetes or are exposed to a glucose challenge.

### How to evaluate your results

Use participant-level separation between training, validation, and testing data. Ideally, test on participants not seen during training, and also evaluate performance on later sessions.

Measure:

* MAE and RMSE for glucose prediction errors.

* Bias and agreement across the glucose range.

* Performance across participants and activity conditions.

* Whether residual-based features outperform raw PPG and simple contextual baselines.

* Whether performance holds up on an independent dataset.

Be particularly careful about data leakage: random splitting of overlapping PPG windows from the same person can produce overly optimistic results.

### 7\. The most important research question

I would formulate your core hypothesis as follows:

> Does subtracting an activity- and context-conditioned baseline PPG representation from the observed post-glucose-challenge representation improve blood glucose estimation compared with directly estimating glucose from PPG?

This hypothesis is testable even if the residual does not isolate glucose perfectly.

Your study should include an ablation experiment comparing:

* Model 1: PPG features alone.

* Model 2: PPG features plus activity and physiological covariates.

* Model 3: Baseline-corrected PPG residuals.

* Model 4: Baseline-corrected residuals plus contextual covariates.

If Model 3 or Model 4 consistently outperforms the other models on unseen participants, that would support the value of your approach. It would not, by itself, prove that the residual is glucose-specific.

### 8\. One question before we develop the architecture

There is an important design choice that will affect how your baseline model should work.

When you say the model should generate PPG with just activity, which situation do you have in mind?

1\. How will you obtain the baseline PPG?

The same participant's PPG before glucose intake

A model predicts baseline PPG from activity and other features

A reference recording from a different session or day

2\. Where will the PPG sensor be worn?

Wrist

Finger

Ear

Another location

3\. What glucose value do you want to predict?

Absolute blood glucose concentration at the current time

Change in glucose concentration relative to baseline

Both absolute concentration and change from baseline

Develop my research architecture

Your answers will help determine whether a paired-subtraction model, a conditional baseline model, or a combination of both is the most appropriate starting point.

---

### Proposed research architecture: personalized baseline-corrected wrist PPG for glucose estimation

I recommend structuring your research around a personalized, context-conditioned residual learning framework. The participant's own pre-intake recordings provide the baseline, and the model learns how the observed PPG differs from what would ordinarily be expected under comparable conditions.

This is a reasonable hypothesis to investigate. Wrist PPG is sensitive to motion and physiological variation, and published reviews identify these as important challenges for glucose-estimation research. PMC +1

### 1\. Overall system architecture

Data acquisition

Wrist PPG + accelerometer + timestamps + activity + reference glucose

Preprocessing and quality control

Signal filtering, windowing, artifact flags, synchronization

### Baseline branch

Personal pre-intake data

Baseline predictor

Expected PPG features

### Observation branch

Current wrist PPG

Shared encoder

Observed PPG features

Residual representation

r_t=z_t-\\widehat z_{0,t}

Residual + baseline state + contextual features

Output 1

Absolute glucose estimate

Output 2

Change from baseline

One important refinement: your original is most straightforward when both vectors represent comparable observations. Because you want to predict glucose at a future time, I would use the difference between the current observed features and a predicted counterfactual baseline: what the features would be expected to look like at that time without the glucose challenge.

That predicted baseline is a model estimate, not a directly observed truth.

### 2\. Mathematical formulation

Let:

* : participant.

* : measurement time.

* : raw wrist PPG window.

* : activity and posture.

* : other available covariates, such as heart rate, skin temperature, and sensor-quality indicators.

* : reference glucose measurement.

Use a shared feature encoder:

z_{i,t}=f_\\theta(x_{i,t})

Train a baseline model using pre-intake data:

\\widehat z_{0,i,t}
=g_\\phi(a_{i,t},c_{i,t},b_i,\\tau_t)

Here summarizes the participant's baseline characteristics, and represents elapsed time or other relevant temporal information. Only information available at prediction time should be used.

Calculate the residual:

r_{i,t}=z_{i,t}-\\widehat z_{0,i,t}

Then predict both targets:

\\widehat G_{i,t}=h_\\psi(r_{i,t},z_{0,i},c_{i,t})\\widehat{\\Delta G}_{i,t}
=k_\\omega(r_{i,t},G_{i,0})

where is a summary of the participant's initial baseline, and is the reference glucose value at baseline.

Define the reference change as:

\\Delta G_{i,t}=G_{i,t}-G_{i,0}

The absolute-glucose head and change-from-baseline head should be trained and evaluated separately, even if they share a representation.

If you use the same baseline reference in both outputs, you can check their consistency:

\\widehat G_{i,t}\\approx G_{i,0}+\\widehat{\\Delta G}_{i,t}

Do not force this equality unless your model design explicitly enforces it and your reference measurements support that constraint.

### 3\. Experimental methodology

### Phase 1 — Pilot study and signal characterization

Start with a small pilot to determine whether your wrist PPG recordings are stable enough for this approach. The purpose is to validate the measurement protocol, not to claim glucose-prediction accuracy.

Record the following data:

| Variable              | Recommended recording                                        |
| --------------------- | ------------------------------------------------------------ |
| Wrist PPG             | Raw waveform, preferably with all available optical channels |
| Motion                | Synchronized accelerometer; gyroscope if available           |
| Activity              | Posture, walking, exercise and rest labels                   |
| Physiological context | Heart rate, skin temperature if available                    |
| Reference glucose     | Time-stamped glucometer measurements                         |
| Experimental context  | Intake time, amount, meal details and session ID             |
| Sensor conditions     | Device, wrist, fit, contact quality and signal-quality flags |

Use the same device and wrist throughout the initial study. Document sensor tightness, placement, ambient temperature, and time spent resting before measurements. Poor-quality PPG windows should be flagged rather than automatically interpreted as physiological changes.

### Phase 2 — Repeated baseline and challenge sessions

I would use a repeated-measures protocol with a baseline condition and a glucose-challenge condition, plus a matched control condition when feasible.

### Illustrative session timeline

* Stabilization

    Participant rests in a standardized posture; verify PPG quality and record initial contextual measurements.

* Baseline window

    Record PPG and reference glucose before the challenge. Repeat baseline sessions on different days to measure normal variability.

* Intervention or control

    Use a standardized, ethically approved protocol. Record the exact time and intervention details.

* Post-intervention monitoring

    Collect continuous PPG and synchronized reference glucose readings at protocol-defined intervals, while recording activity and relevant covariates.

* Repeat and compare

    Repeat sessions where appropriate to distinguish reproducible responses from ordinary within-person variation.

The control session matters because your model could otherwise learn the passage of time, hydration changes, or ordinary post-meal physiology rather than glucose-related changes.

Use an ethics-approved protocol and appropriate clinical supervision. Do not ask participants to alter prescribed medication or deliberately induce unsafe glucose levels.

### Phase 3 — Construct the dataset correctly

Each training example should contain a current PPG window, the baseline data available before that window, and a reference glucose measurement collected at the relevant time.

A conceptual dataset row might look like this:

| Field                     | Example  |
| ------------------------- | -------- |
| Participant ID            | P017     |
| Session ID                | S02      |
| Time since intervention   | 30 min   |
| Activity                  | Standing |
| PPG feature vector        |          |
| Predicted baseline vector |          |
| Residual vector           |          |
| Reference glucose         |          |
| Baseline glucose          |          |
| Change in glucose         |          |

The values above illustrate the schema; they are not experimental observations.

Prevent leakage: baseline recordings must not include information from future post-intake windows. Fit normalization parameters and feature selection only on training data. If you train a learned encoder, train or freeze it within the appropriate training folds before generating residual features for validation and test sets.

### 4\. Model development: what to train first

Do not begin with two independent deep-learning models that generate and . Start with interpretable models and progressively add complexity.

| Experiment | Baseline approach                           | Glucose estimator                                     |
| ---------- | ------------------------------------------- | ----------------------------------------------------- |
| E0         | No baseline correction                      | Ridge regression on raw PPG features                  |
| E1         | Personal pre-intake feature mean            | Ridge regression on residuals                         |
| E2         | Activity- and context-conditioned predictor | Ridge regression on residuals                         |
| E3         | Learned shared PPG encoder                  | PLS or gradient boosting on residuals                 |
| E4         | Learned conditional baseline                | Neural regression with residual and contextual inputs |

For E1, the baseline residual is simply:

r_{i,t}=z_{i,t}-\\bar z_{i,\\mathrm{baseline}}

For E2, use a baseline predictor:

\\widehat z_{0,i,t}=g_\\phi(a_{i,t},c_{i,t},b_i,\\tau_t)

The second approach is more flexible because it can account for changes in activity and measured physiological conditions. However, it is only trustworthy when the baseline training data adequately represent those conditions.

My recommendation: implement E0, E1 and E2 before attempting E3 or E4. This gives you an early answer to the central research question: does personalized baseline correction actually help?

### 5\. How to train the baseline model without leakage

There is a subtle problem with your proposal.

You want to learn what PPG looks like without a glucose challenge. But your baseline model could accidentally learn characteristics of the training participants rather than a general relationship between activity and PPG.

Use this training procedure:

* Collect multiple pre-intake recordings for each participant, covering the conditions you intend to model.

* Extract PPG features using the same preprocessing pipeline for all recordings.

* Train the baseline predictor using only pre-intake observations.

* Validate it on held-out baseline sessions, including sessions from participants not used in training.

* Generate expected baseline features for post-intake observations using only information available at prediction time.

* Calculate residuals and train the glucose estimator on the resulting training data.

* Freeze the pipeline and evaluate it on completely held-out participants.

A participant's own baseline can be used for personalization at test time, but the model must not access their future glucose measurements or post-intake PPG when constructing that baseline.

You should evaluate baseline reconstruction separately from glucose estimation. A baseline model that reconstructs PPG accurately is not necessarily a good glucose estimator; it could remove useful physiological information along with nuisance variation.

### 6\. Experimental controls and confounders

Your goal is to reduce the effects of other factors, not to assume they can all be eliminated.

| Potential confounder                 | How to address it                                                                      |
| ------------------------------------ | -------------------------------------------------------------------------------------- |
| Activity and motion                  | Accelerometer-based activity labels, quality flags, matched conditions                 |
| Heart rate and autonomic changes     | Measure heart rate and test whether residuals retain predictive value after adjustment |
| Temperature and peripheral perfusion | Standardize the environment and measure skin temperature when possible                 |
| Sensor fit and contact pressure      | Standardize placement and strap fit; log repositioning                                 |
| Participant-specific physiology      | Personal baseline calibration and held-out participant evaluation                      |
| Meals and time of day                | Standardize the protocol and include appropriate control sessions                      |
| Reference measurement error          | Use a validated glucometer, consistent sampling procedures and precise timestamps      |

Wrist PPG can be affected by baseline drift, respiration, thermoregulation and autonomic activity, which supports your motivation for correction but also shows why a single activity label will not capture every relevant effect. PMC +1

A particularly important control is to compare your glucose challenge against a matched session without that challenge. If residuals change similarly in both sessions, your model may be detecting time-dependent physiological variation rather than a glucose-associated response.

### 7\. Training objectives and evaluation

Train two prediction heads with separate targets.

For absolute glucose estimation:

\\mathcal L_{\\mathrm{abs}}
=\\frac{1}{N}\\sum_{i,t}
(\\widehat G_{i,t}-G_{i,t})^2

For change estimation:

\\mathcal L_{\\mathrm{change}}
=\\frac{1}{N}\\sum_{i,t}
\\left(\\widehat{\\Delta G}_{i,t}
-(G_{i,t}-G_{i,0})\\right)^2

You can combine these losses later, after checking the performance of each head separately. If you combine them, normalize the losses appropriately so their numerical scales do not cause one objective to dominate.

### Evaluation metrics

| Metric                                                | What it tells you                                                          |
| ----------------------------------------------------- | -------------------------------------------------------------------------- |
| MAE                                                   | Average magnitude of glucose estimation error                              |
| RMSE                                                  | Error with greater penalty for large mistakes                              |
| Bias                                                  | Whether predictions systematically overestimate or underestimate glucose   |
| Bland–Altman analysis                                 | Agreement and limits of agreement between predictions and reference values |
| Change MAE                                            | Accuracy of predicted glucose changes                                      |
| Within-participant vs. unseen-participant performance | Whether the method generalizes beyond personalized calibration             |

Report errors in mg/dL or mmol/L, and specify the reference method and glucose range.

A glucometer is a practical reference for a research study, but its readings also have measurement error. For rigorous clinical validation, consider whether laboratory reference measurements are feasible and appropriate. Published evaluations have shown that promising-looking noninvasive glucose-monitoring approaches do not necessarily achieve adequate measurement accuracy. PubMed +1

Do not use correlation alone as your main performance measure. A model can have a high correlation with reference glucose and still have substantial systematic errors.

### 8\. The most important ablation experiment

I would make this the centerpiece of your first paper.

### Research experiment: Does residual learning help?

Compare all methods using the same held-out participants and reference glucose observations.

Model A — Raw PPG

Baseline

Does PPG alone predict glucose?

Model B — PPG + context

Does activity and physiological context improve prediction?

Model C — Personal baseline residual

Does subtracting the participant's baseline improve prediction?

Model D — Predicted baseline residual

Does your activity- and context-conditioned approach improve on a simple baseline?

Model E — Residual + context

Does retaining contextual variables alongside the residual produce the best result?

Predefine your primary metric and statistical comparison. Use participant-level bootstrap confidence intervals or another appropriate repeated-measures method to quantify uncertainty. The sample size should be determined by a power or precision analysis based on pilot variability, rather than an arbitrary number of participants.

If the residual models do not outperform the simpler models, that is still a useful research finding. It would suggest that your baseline subtraction does not add enough glucose-related information under the conditions tested.

### 9\. Recommended research roadmap

* Stage 1 — Feasibility. Establish wrist PPG quality, reliable synchronization, and a controlled data collection protocol.

* Stage 2 — Baseline modeling. Compare personal feature means, linear models and nonlinear conditional models.

* Stage 3 — Residual validation. Test whether residuals respond differently during glucose-challenge and control sessions.

* Stage 4 — Glucose regression. Compare raw PPG, contextual features and residual-based estimators for absolute glucose and glucose change.

* Stage 5 — Generalization. Evaluate on unseen participants and later sessions, followed by an independent validation study.

One final safety and scientific point: this is a research concept, not an established noninvasive glucose measurement method. The FDA warns against relying on smartwatches or smart rings that independently claim to measure glucose without piercing the skin, and clinical guidance does not currently recommend noninvasive glucose measurement as a replacement for established blood glucose monitoring. FDA +1

### My final recommendation

Keep your original idea, but refine its central claim:

Instead of assuming that equals the glucose feature, test whether a personalized, activity-conditioned PPG residual contains information that improves glucose estimation.

That is a more defensible scientific hypothesis and a strong foundation for an experimental research project.
