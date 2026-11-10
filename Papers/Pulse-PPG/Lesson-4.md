### Lesson 4 — Mathematical Deep Dive: Deriving Pulse-PPG from First Principles

Today we'll move from understanding the methodology to being able to derive and implement it.

I want you to be able to answer three questions mathematically:

* How does Pulse-PPG calculate similarity between two noisy PPG sequences?

* How does that similarity guide the foundation model's embedding space?

* What happens to the gradients, computational complexity, and learned representations?

We'll follow the actual equations in Sections 3.2 and 4.1–4.3 of the paper.

Our notation

| Symbol | Meaning                    |
| ------ | -------------------------- |
|        | Batch size                 |
|        | Number of time points      |
|        | Feature dimension          |
|        | Subsampling stride         |
|        | Anchor sequence            |
|        | Candidate sequence         |
|        | Query, key, value          |
|        | Foundation-model embedding |

The actual input is a four-minute PPG segment:

T=240\\times50=12,000

The motif-distance network uses feature dimension 64 and stride 10.

The foundation model produces a 512-dimensional embedding.

These are two separate networks with different purposes.

arXiv

### Part 1 — Tensor shapes: Understand the data flow

Let's start with the most fundamental implementation detail.

A batch of PPG sequences can be represented as:

X\\in\\mathbb R^{B\\times T\\times 1}

For example:

X\\in\\mathbb R^{16\\times12000\\times1}

This means:

* 16 sequences.

* 12,000 time points per sequence.

* One input channel.

The distance network transforms the signal into three feature representations.

Q=f_q(X)K=f_k(X)V=f_v(X)

Their conceptual shapes are:

Q,K,V\\in\\mathbb R^{B\\times T\\times64}

The actual implementation uses convolutional layouts, typically:

\[B,64,T\]

After subsampling:

Q_s,K_s,V_s
\\in
\\mathbb R^{B\\times1200\\times64}

Tensor-shape walkthrough

\[B, 1, 12000\]

Dilated convolution networks

Q

\[B, 64, 12000\]

K

\[B, 64, 12000\]

V

\[B, 64, 12000\]

Subsampling, stride 10

\[B, 64, 1200\]

Cross-attention

\[B, 1200, 1200\] attention matrix

Important distinction: The full-resolution convolutional representations capture temporal context before the subsampled positions are used for the expensive reconstruction comparison.

This is why subsampling does not simply mean throwing away 90% of the original waveform before feature extraction.

### Part 2 — Derive cross-attention mathematically

Now let's derive the attention mechanism.

Suppose we have one anchor sequence and one candidate sequence.

After feature extraction and subsampling:

Q_a\\in\\mathbb R^{L\\times D}K_c,V_c\\in\\mathbb R^{L\\times D}

where:

L=T/s=1200,\\qquad D=64

### Step 1: Calculate similarity scores

S=Q_aK_c^\\top

Therefore:

S\\in\\mathbb R^{1200\\times1200}

Each entry:

S_{ij}=q_i^\\top k_j

measures the compatibility between anchor position and candidate position .

### Step 2: Apply softmax

A_{ij}
=
\\frac{\\exp(S_{ij})}
{\\sum_{r=1}^{L}\\exp(S_{ir})}

Now every row sums to one:

\\sum_{j=1}^{L}A_{ij}=1

This means each anchor position has its own distribution over candidate positions.

### Step 3: Reconstruct

\\hat X_a=AV_c

Shapes:

\[L,L\]\\times\[L,D\]=\[L,D\]

Each reconstructed anchor feature is a weighted combination of candidate value features.

### Step 4: Calculate reconstruction distance

\\boxed{
d(X_a,X_c)
=
\\sum_{i=1}^{L}
\\sum_{r=1}^{D}
(\\hat X_{a,i,r}-X_{a,i,r})^2
}

The reference in the reconstruction error is the anchor representation at the corresponding subsampled positions.

Cross-attention operation

Anchor queries

1200 × 64

Candidate keys

1200 × 64

Similarity matrix

### 1200 × 1200

Softmax attention × candidate values

Reconstructed anchor

1200 × 64

Scalar reconstruction distance

One detail: the paper omits projection and normalization details in its mathematical presentation. The equations above explain its core attention computation, rather than claiming to reproduce every internal layer of the released implementation.

### Part 3 — Understand the gradient of the reconstruction objective

This is where your mathematical background becomes particularly useful.

We want to understand how the model learns better motif matching.

For one anchor position, define:

\\hat x=\\sum_j\\alpha_jv_j

and:

e=\\|\\hat x-x\\|^2

Let:

\\alpha_j=\\operatorname{softmax}(s)_j

where .

### Step 1: Differentiate the error with respect to reconstruction

\\frac{\\partial e}{\\partial\\hat x}
=
2(\\hat x-x)

Interpretation:

If reconstruction is inaccurate, the gradient increases in magnitude.

### Step 2: Differentiate with respect to attention weights

Because:

\\hat x=\\sum_j\\alpha_jv_j

we obtain:

\\frac{\\partial e}{\\partial\\alpha_j}
=
2(\\hat x-x)^\\top v_j

This tells us how changing the weight of a candidate value affects reconstruction error.

### Step 3: Differentiate through softmax

The softmax Jacobian is:

\\frac{\\partial\\alpha_j}{\\partial s_l}
=
\\alpha_j(\\delta_{jl}-\\alpha_l)

Combining the derivatives gives:

\\boxed{
\\frac{\\partial e}{\\partial s_l}
=
2\\alpha_l(\\hat x-x)^\\top(v_l-\\hat x)
}

This equation is extremely useful.

It tells us that attention scores are updated according to the relationship between:

* Reconstruction error.

* Candidate value representation.

* Current reconstructed representation.

* Current attention probability.

The model is not merely learning to maximize similarity between Q and K.

It is learning attention weights that improve reconstruction.

### Research interpretation

This is a key difference from ordinary similarity-based attention.

The attention mechanism is optimized indirectly by the reconstruction objective.

That creates a potentially useful representation of local waveform structure, but it also introduces a possible weakness:

The model may discover reconstructive shortcuts that are not necessarily physiologically meaningful.

For example, highly repetitive noise patterns could help reconstruct masked regions.

This motivates additional objectives that test whether learned motifs correspond to genuine physiological structure.

### Part 4 — Computational complexity

Let's calculate why stride 10 matters.

Without subsampling:

L=12,000

The attention matrix contains:

12,000^2=144,000,000

entries.

With stride 10:

L=1,200

The attention matrix contains:

1,200^2=1,440,000

entries.

The ratio is:

\\frac{144,000,000}{1,440,000}=100

So the attention matrix is 100 times smaller.

This reduction applies to the quadratic attention calculation, not necessarily to the entire network's runtime or memory footprint.

Research opportunity: Could we use sparse attention or hierarchical motif matching to reduce the cost further without sacrificing the quality of the distance estimates?

That is a viable systems-oriented extension.

### Part 5 — Derive Relative Contrastive Learning

Now we move from the distance network to the foundation encoder.

This is the second major optimization problem.

Let the foundation encoder be:

z=f_\\theta(X)

where:

z\\in\\mathbb R^{512}

The encoder is a 1D ResNet-26 with 28.5 million trainable parameters.

The motif-distance network is already trained and is used as a static distance estimator during this stage.

### 5.1 Construct the candidate set

For an anchor sequence , the paper samples candidates from two sources:

Within-subject candidates

Same person, different time windows.

These help model how one individual's PPG changes throughout the day.

Between-subject candidates

Different people from the batch.

These help model physiological similarities and differences across individuals.

This distinction is scientifically important.

The model should not simply learn that all signals from one person are identical.

It should learn both:

* Intra-individual variability.

* Inter-individual relationships.

### 5.2 Construct relative rankings

Suppose the learned distance network produces:

d_a=\[0.10,0.25,0.45,0.80,1.20\]

For each candidate , define its negative set:

\\mathcal N_i=
\\{j:d_{aj}>d_{ai}\\}

Now calculate the contrastive loss for each candidate:

\\ell_i=
-\\log
\\frac{
\\exp(\\operatorname{sim}(z_a,z_i)/\\tau)
}{
\\exp(\\operatorname{sim}(z_a,z_i)/\\tau)
+
\\sum_{j\\in\\mathcal N_i}
\\exp(\\operatorname{sim}(z_a,z_j)/\\tau)
}

The total loss is:

\\mathcal L_{\\text{RelCon}}
=
\\sum_i\\ell_i

### 5.3 Why is this different from ordinary contrastive learning?

Imagine ordinary contrastive learning has one positive and three negatives.

It knows only that:

z_a\\sim z_p

and:

z_a\\not\\sim z_{n_1},z_{n_2},z_{n_3}

Relative contrastive learning constructs multiple comparisons.

It can encode a ranking structure:

d(A,B)<d(A,C)<d(A,D)

Rather than declaring C and D equally negative relative to A, it uses the different candidate-specific negative sets.

This is particularly useful when the dataset contains continuous physiological variation rather than clean categorical classes.

### 5.4 A subtle point about gradients

The motif-distance function is static during foundation-model training.

Therefore:

\\frac{\\partial \\mathcal L_{\\text{RelCon}}}
{\\partial \\theta_d}=0

where represents the distance-network parameters.

But:

\\frac{\\partial \\mathcal L_{\\text{RelCon}}}
{\\partial \\theta_f}\\neq0

where represents the foundation encoder parameters.

The contrastive loss updates the foundation encoder, not the motif-distance model.

This separation is important for reproducing the training procedure correctly.

### Part 6 — Reconstruct the actual model architecture

The two networks have substantially different sizes and purposes.

A. Motif-distance network

127K parameters

* Five dilated convolution blocks.

* Initial dilation of 1, doubling after each layer.

* Kernel size 15.

* Feature dimension 64.

* Stride 10.

* Partial convolution for handling missing input.

* Instance normalization and residual connections.

* MSE reconstruction distance.

    B. Pulse-PPG foundation encoder

    28.5M parameters

* 1D ResNet-26.

* Initial filters: 128.

* Kernel size: 11.

* Initial stride: 2.

* 12 residual blocks.

* Instance normalization.

* Global temporal max pooling.

* 512-dimensional output embedding.

Notice something interesting:

The smaller model defines the similarity structure.

The much larger model learns to represent that structure efficiently.

This is a form of teacher-like supervision, although it is not conventional teacher-student distillation: the teacher here is a learned pairwise distance function rather than a classification network.

arXiv

### Part 7 — PyTorch implementation blueprint

Let's translate the mathematics into code.

This is educational pseudocode, not a reproduction-ready implementation of the authors' repository.

### 7.1 Cross-attention reconstruction

```python

import torch
import torch.nn.functional as F

def motif_distance(query, candidate, q_net, k_net, v_net,
                   stride=10):
    """
    query:     [B, 1, T]
    candidate: [B, 1, T]
    """

    # Feature extraction at full temporal resolution
    Q = q_net(query)       # [B, D, T]
    K = k_net(candidate)   # [B, D, T]
    V = v_net(candidate)   # [B, D, T]

    # Subsample feature positions
    Q = Q[..., ::stride]
    K = K[..., ::stride]
    V = V[..., ::stride]

    # Attention: [B, L, L]
    scores = torch.bmm(
        Q.transpose(1, 2),
        K
    )

    attention = F.softmax(scores, dim=-1)

    # Weighted reconstruction: [B, D, L]
    reconstructed = torch.bmm(
        V,
        attention.transpose(1, 2)
    )

    # Compare against anchor features
    target = Q

    # Per-example squared reconstruction error
    distance = (
        reconstructed - target
    ).pow(2).sum(dim=(1, 2))

    return distance
```

One important implementation note: the paper's distance network includes projection and normalization layers, and its actual architecture must be followed when reproducing the published results. The code above illustrates the mathematical flow.

### 7.2 Relative contrastive loss

```python

import torch
import torch.nn.functional as F

def relative_contrastive_loss(
    anchor_embedding,
    candidate_embeddings,
    distances,
    temperature=0.1
):
    """
    anchor_embedding:     [D]
    candidate_embeddings: [N, D]
    distances:            [N]

    Smaller distance = more similar.
    """

    # Similarity in embedding space
    z_a = F.normalize(anchor_embedding, dim=-1)
    z_c = F.normalize(candidate_embeddings, dim=-1)

    similarities = z_c @ z_a / temperature

    losses = []

    for i in range(len(distances)):

        # Candidates farther away than positive i
        negative_mask = distances > distances[i]

        # Positive plus all selected negatives
        selected_logits = torch.cat([
            similarities[i:i+1],
            similarities[negative_mask]
        ])

        target = torch.zeros(
            1, dtype=torch.long,
            device=selected_logits.device
        )

        losses.append(
            F.cross_entropy(
                selected_logits.unsqueeze(0),
                target
            )
        )

    return torch.stack(losses).sum()
```

The implementation above demonstrates the candidate-wise objective. A full implementation must also handle candidate-set construction, batching, ties, empty negative sets, and the exact similarity and normalization conventions of the reference implementation.

### Part 8 — What can we improve scientifically?

Now comes the part most relevant to your research goal.

Let's formulate an extension rather than simply changing the backbone.

Potential research contribution

Temporal-Order-Aware Relative Contrastive Learning for PPG

The core issue:

The existing motif distance can identify similar local patterns without explicitly requiring that their global temporal order be preserved.

Suppose:

X_a=\[A,B,C,D\]X_c=\[A,C,B,D\]

A local matching system might find good matches for every motif, even though the sequence order differs.

We could introduce an order-consistency objective.

### Proposed formulation

Let:

H_a,H_c

represent learned temporal motif embeddings.

Define pairwise similarity:

S_{ij}
=
\\operatorname{sim}(H_{a,i},H_{c,j})

We could construct a soft alignment matrix:

P=\\operatorname{softmax}(S)

Then introduce an order-consistency penalty:

\\mathcal L_{\\text{order}}
=
\\sum_{i,j,k,l}
P_{ij}P_{kl}
\\max(0,-(i-k)(j-l))

This penalizes pairs of alignments that reverse temporal order.

Finally:

\\boxed{
\\mathcal L_{\\text{proposed}}
=
\\mathcal L_{\\text{RelCon}}
+
\\lambda\\mathcal L_{\\text{order}}
}

This is a proposed research objective, not part of the original Pulse-PPG method.

Why might it help?

It could preserve both:

* Local waveform morphology.

* Global temporal structure.

But it introduces a trade-off: some legitimate PPG patterns shift in time because heart rate changes. A rigid order constraint could hurt robustness if designed poorly.

We would need experiments to determine whether a soft order constraint actually improves generalization.

### Part 9 — Research-level critical questions

Before we proceed, I want you to think about five deeper issues.

| Research question                                             | What you should investigate                       |
| ------------------------------------------------------------- | ------------------------------------------------- |
| Does reconstruction imply physiological similarity?           | Shortcut learning and representation validity     |
| Is the distance function symmetric?                           | Directional reconstruction and metric learning    |
| Can local matching preserve temporal order?                   | Sequence alignment and structural constraints     |
| Does subsampling lose important motifs?                       | Resolution and computational trade-offs           |
| Does RelCon learn semantic structure or participant identity? | Subject leakage and unseen-subject generalization |

One particularly important issue is the distinction between physiological similarity and participant similarity.

If two segments from the same individual are similar, is that because they share physiology, sensor characteristics, or simply the same person's acquisition conditions?

That distinction deserves a dedicated ablation study.

### Part 10 — Test your mathematical understanding

Advanced mathematical assessment

0/5 answered

1. What is the shape of the attention matrix after stride-10 subsampling?

1200 × 64

1200 × 1200

64 × 64

12000 × 12000

2. What does the motif reconstruction objective optimize?

Classification accuracy

Attention weights that improve anchor reconstruction

Participant identification

Heart-rate prediction

3. During foundation-model training, what happens to the motif-distance network?

It is jointly updated with ResNet

It is frozen and used to calculate relative distances

It is replaced by a classifier

Its weights are randomly initialized for every batch

4. What is the primary purpose of the relative negative-set construction?

Treat every candidate as equally negative

Select candidates farther from the anchor than the chosen positive

Select only same-subject examples

Remove all hard negatives

5. What is a potential weakness of adding a temporal-order constraint?

It always increases the number of subjects

It can penalize legitimate temporal shifts caused by physiological variability

It removes the need for training data

It guarantees perfect generalization

Submit answers

### Lesson 4 — What you should now be able to explain

You should be able to derive the following pipeline without looking at the paper:

### Complete mathematical picture

X_a,X_c\\in\\mathbb R^{T\\times1}Q=f_q(X_a),\\quad K,V=f_{k/v}(X_c)A=\\operatorname{softmax}(QK^\\top)\\hat X_a=AVd(X_a,X_c)=\\|\\hat X_a-X_a\\|_2^2

z_i=f_\\theta(X_i)\\mathcal N_i=\\{j:d_{aj}>d_{ai}\\}\\mathcal L_{\\mathrm{RelCon}}=\\sum_i\\ell(z_a,z_i,\\mathcal N_i)

Conceptual mathematical summary; the paper's implementation includes additional feature projections, normalization and subsampling details.

### Next: Lesson 5 — Training, Datasets, and Reproducibility

Next lesson

### How Pulse-PPG Was Actually Trained

![NVIDIA L40S Cloud GPUs for Generative AI & RAG Workloads | Inhosted.ai](https://images.openai.com/static-rsc-4/SM6YrZyZ_jaEQOtOTZOF0xflsItqHI73YZ9NbSPiaaXEOCgrTsaqWQ1i324LN2cweeN6NmU_Sj_Mq_XcrF26WKbkkPTjzJaQyGcSDf3SqU-f0L8evDgmvPy7G-3xs1zHlRF6I9eM9fheJLr4JIeCsfdbBjxZruoXvmhtTpXbzwDbfGzTK6EwJSAgSPKcgnBg?purpose=fullsize)

We'll investigate the experimental implementation:

* MOODS dataset: 120 participants and approximately 55,000 hours of raw PPG.

* Subject-wise train/validation/test splitting.

* Person-specific normalization.

* Four-minute input-window selection.

* Hyperparameter selection and ablation studies.

* The six-epoch pre-training process.

* Reproducing the model using the official PyTorch repository.

* Identifying weaknesses in the experimental design.

We'll also examine whether the reported improvements can be attributed to the training objective, the data distribution, or both.

A research challenge to keep in mind: If you had unlimited GPU resources, would you improve the motif-distance function, the relative contrastive objective, or the dataset first?

There isn't an obvious answer. A good research paper needs experiments that separate these factors.

Original paper: [Pulse-PPG — full paper](https://arxiv.org/html/2502.01108v2?utm_source=chatgpt.com) · [Official implementation](https://github.com/maxxu05/pulseppg?utm_source=chatgpt.com).
