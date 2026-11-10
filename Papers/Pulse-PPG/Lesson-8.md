### Lesson 8 — From Paper to Code: Reproducing Pulse-PPG and Building Your Extension

We’ve now covered the paper’s motivation, related work, methodology, mathematics, training setup, results, and limitations. The final step is to turn that understanding into a reproducible research pipeline.

A key distinction before we start:

* Use the pretrained model: load its weights, extract embeddings, and evaluate downstream tasks.

* Reproduce the paper: recreate its preprocessing, motif-distance training, foundation-model pretraining, and evaluations.

* Extend the method: change one scientific component, then test whether that change produces a measurable improvement.

These are three different levels of effort. I recommend starting with pretrained inference and a faithful downstream baseline, then attempting full pretraining only if the data and compute are available.

### 1\. What the official repository actually provides

The official [Pulse-PPG GitHub repository](https://github.com/maxxu05/pulseppg?utm_source=chatgpt.com) is more useful than a paper-only description because it exposes the experiment structure:

* `run_exp.py` — main experiment launcher.

* `pulseppg/models/RelCon/` — relative contrastive training.

* `pulseppg/models/MotifDist/` — motif-distance model.

* `pulseppg/nets/` — network backbones.

* `pulseppg/data/process/` — data processing.

* `pulseppg/eval/` — evaluation pipeline.

* `pulseppg/experiments/configs/` — experiment configurations.

    GitHub

The README documents pretrained weights hosted on Zenodo, a Conda environment, public evaluation-data preprocessing scripts, and commands for evaluation and retraining. Importantly, it says the current custom-dataset evaluation configuration is limited to linear probing; fine-tuning support is described as planned. GitHub

That gives us a concrete starting point rather than having to reconstruct the codebase from equations alone.

### 2\. A staged reproduction workflow

### Stage A — Establish a reproducible environment

The repository's documented setup is:

```bash
git clone https://github.com/maxxu05/pulseppg.git
cd pulseppg

conda env create -f env.yml
conda activate pulseppg
pip install -e .
```

The README also documents a script for downloading the pretrained weights. Check the repository's current file list before running it: the README refers to `download_pulseppg.sh`, while the top-level file listing currently displays `download_model.sh`. Don't assume those names are interchangeable. GitHub

Record the exact code version and environment:

```bash
git rev-parse HEAD
conda env export > environment.yml
python --version
```

Also record the GPU model, CUDA version, random seeds, and the exact checkpoint used.

### Stage B — Run the provided evaluation first

The documented evaluation command is:

```bash
python run_exp.py --config pulseppg --retrain_eval
```

The README says the public evaluation datasets can be prepared using scripts for PPG-BP, PPG-DaLiA, SDB, and WESAD. GitHub

Your first milestone is not to improve the reported score. It is to confirm that the code runs and to understand what the pipeline actually measures.

For every run, capture:

* Dataset and task.

* Subject-level split.

* Preprocessing and normalization.

* Frozen or trainable encoder.

* Checkpoint identifier.

* Evaluation metric.

* Random seed.

Do not compare your result to the paper until you have checked that the split, preprocessing, label construction, and metric definitions match. A seemingly small difference in subject splitting can make a representation-learning comparison misleading.

### Stage C — Evaluate on your own dataset

The README describes adding a dataset under `pulseppg/data/datasets` and defining an `Eval_Config` in `experiments/out/PulsePPG_expconfigs.py`. It also specifies the expected pretraining data hierarchy as:

```text
train/
  subject_id/
    data_input_0.npy
    data_input_1.npy
    ...
```

The `DUMMY.py` processing example is identified as the reference for the expected hierarchy. GitHub

Before integrating your data, verify the actual loader's assumptions: array shape, dtype, sampling rate, channel convention, missing-value handling, and whether normalization is applied per window or per subject. The directory structure alone does not establish those details.

### 3\. Reproducing pretraining from scratch

The repository documents two separate training commands:

```bash
python run_exp.py --config motifdist --retrain
python run_exp.py --config pulseppg --retrain
```

The intended order matters:

* Train the motif-distance model.

* Use the learned distance in the Pulse-PPG relative contrastive training stage.

The README says you can use different input lengths for pretraining because the model uses temporal pooling. It gives 30 seconds as an example, compared with the paper's four-minute inputs. GitHub

But there's an important scientific distinction:

Being able to train on a different window length does not mean the resulting model is equivalent.

Changing window length changes the temporal context available to the encoder, the number and distribution of motifs, and potentially the representation's invariances. Treat window duration as an experimental variable, not just a convenient configuration setting.

Also, don't assume that access to the source code and pretrained weights gives you access to the original MOODS raw training data. The README documents public evaluation datasets and custom pretraining data, but you should verify data access and usage permissions separately.

### 4\. How I would design your first extension

I would recommend starting with the temporal-order-aware motif idea from Lesson 7. It is a relatively contained modification: it changes the learning objective while leaving most of the Pulse-PPG architecture intact.

The hypothesis:

> Relative contrastive learning based on local motif similarity may identify matching local patterns without adequately preserving their global temporal order. Explicitly penalizing order-inconsistent alignments may improve representations of physiological dynamics.

### Proposed objective

Let represent the attention or alignment weight between position in one signal and position in another.

A possible order-violation penalty is:

\\mathcal L_{\\mathrm{order}}
=
\\sum_{i<k}\\sum_{j>l}P_{ij}P_{kl}

This penalizes alignments where the order of matched positions is reversed.

Then:

\\mathcal L_{\\mathrm{total}}
=
\\mathcal L_{\\mathrm{RelCon}}
+
\\lambda\\mathcal L_{\\mathrm{order}}

This is a proposed research modification, not an equation from the original paper.

There are implementation choices to resolve before coding:

* Should be normalized attention, a soft alignment matrix, or a transport plan?

* Should the penalty operate over all positions or only selected motifs?

* Should it be applied to both directions of the motif distance?

* How should it handle genuine physiological variation, such as heart-rate changes or local timing differences?

One concern: excessive order preservation could penalize legitimate temporal warping. That makes the weight and the alignment formulation central research variables.

### 5\. Experimental design

I would use this initial experiment matrix:

| Experiment | Encoder/objective                    | Purpose                                   |
| ---------- | ------------------------------------ | ----------------------------------------- |
| E0         | Original Pulse-PPG                   | Baseline                                  |
| E1         | Pulse-PPG + order penalty            | Main proposed method                      |
| E2         | E1 with                              | Implementation control                    |
| E3         | E1 with small                        | Weak order constraint                     |
| E4         | E1 with medium                       | Moderate constraint                       |
| E5         | E1 with large                        | Strong constraint                         |
| E6         | Random or shuffled alignment control | Test whether the alignment signal matters |

Evaluate at three levels:

Representation quality

* Linear-probe performance.

* Embedding consistency across augmentations.

* Within-subject versus between-subject similarity.

Generalization

* Subject-independent evaluation.

* Cross-dataset transfer.

* Cross-device evaluation, if metadata permits.

Robustness

* Motion-corrupted signals.

* Amplitude changes.

* Missing or low-quality signal segments.

* Different window lengths.

Use the same data splits and training budget for the baseline and proposed method. Repeat the main experiments with multiple random seeds and report mean and standard deviation.

One especially important control: test whether the proposed method improves physiological information rather than merely learning subject identity or recording conditions.

### 6\. What would make this a convincing research contribution?

A strong extension needs more than a higher F1 score on one dataset.

I'd want the eventual paper to establish:

* A clear failure mode: demonstrate that local motif matching can produce order-inconsistent alignments.

* A principled solution: explain why the new objective addresses that failure mode.

* A controlled comparison: compare against original Pulse-PPG under the same training conditions.

* Ablation evidence: show how performance changes with the order penalty and its design.

* Generalization evidence: demonstrate improvements on held-out subjects and preferably another dataset.

* A cost analysis: quantify additional training time, memory, and inference overhead.

Your first practical deliverable should be a working baseline with an experiment log—not a modified loss function. Once you can reproduce the baseline, you have a trustworthy reference against which to measure your contribution.

### 7\. Your next research step

I suggest we now move from paper-reading mode into implementation mode. The most useful next step is to inspect the repository's actual model and training code, identify the exact point where the proposed order penalty belongs, and design the modification without disturbing the original baseline.

One question: What compute environment will you use?

Compute environment

Local NVIDIA GPU

Google Colab

University or cloud GPU server

CPU only

Not decided yet

GPU model, if known (optional)

First implementation goal

Reproduce pretrained evaluation

Reproduce full pretraining

Implement temporal-order extension

Continue to implementation

That will determine whether we start with checkpoint loading, full training, or the proposed research modification.
