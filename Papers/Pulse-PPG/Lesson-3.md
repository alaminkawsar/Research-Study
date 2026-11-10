### Lesson 3 — Pulse-PPG Methodology: Reconstructing the Actual Algorithm

Now we're entering the technical heart of the paper.

Our objective is not simply to understand what the authors did. We want to understand why each mathematical operation exists, what assumptions it introduces, and how we could improve it in a follow-up paper.

One correction to keep our reading precise: the paper's motif-matching function is implemented using a learnable cross-attention mechanism and a reconstruction-style distance. It is not simply conventional nearest-neighbor matching.

We'll reconstruct that mechanism directly from the equations.

### 1\. First, understand the complete pipeline

Pulse-PPG has two important learning stages:

* Train a learnable motif-based distance function.

* Use that distance function to train the foundation model with relative contrastive learning.

This separation is essential.

Stage 1 — Learn the distance function

Raw PPG sequence pairs

Anchor and candidate

Dilated convolution networks

Learn Q, K and V representations

Cross-attention and reconstruction

Calculate motif-based distance

Learned distance function

Stage 2 — Train the foundation model

PPG sequences and learned relative distances

Relative contrastive learning

Pulse-PPG foundation model

The important insight is that the distance function provides a notion of similarity that the foundation model subsequently learns to reproduce.

Source: Sections 3.2 and 4.1 of the paper. arXiv

### 2\. Why do we need a special distance function?

Let's start with a familiar mathematical concept.

Suppose we have two PPG sequences:

X_a,X_c\\in\\mathbb{R}^{T}

where:

* is the anchor.

* is the candidate.

* is the sequence length.

A simple approach is Euclidean distance:

d_E(X_a,X_c)
=
\\sum_{t=1}^{T}
(X_a(t)-X_c(t))^2

This assumes that corresponding positions should have similar values.

But consider the following example:

* Sequence A contains a pulse at time 10.

* Sequence B contains a similar pulse at time 15.

Even if their morphology is almost identical, pointwise distance can be large because the pulses are misaligned.

The authors want something different.

They want to compare local motifs without requiring exact temporal alignment.

### 2.1 The ideal motif-matching formulation

The paper initially introduces the following conceptual formulation:

d(X_a,X_c)
\\approx
\\sum_{i=0}^{T}
\\underset{j\\in\[0,\\ldots,T\]}{\\arg\\min}
\\left\\{
d_m
\\left(
M(X_a\[i\]),M(X_c\[j\])
\\right)
\\right\\}

Here:

* represents a local motif around position .

* measures the distance between two motifs.

* For each anchor motif, find its best matching candidate motif.

There is a small mathematical subtlety: the displayed equation uses `argmin`, which formally returns an index rather than a distance. The intended operation is the minimum matching distance, or the reconstruction error produced by its learnable approximation.

This distinction will matter when we implement the method.

Intuition: The model should learn which local patterns resemble one another, even if they occur at different positions.

### 3\. Equation (2): The learnable motif-based distance

This is the central mathematical construction.

The authors define:

\\boxed{
d(X_a,X_c)
=
\\sum_{x_a\\in_s X_a}
\\left\\|
\\sum_{x_c\\in_s X_c}
\\alpha(x_a,x_c)f_v(x_c)
-
x_a
\\right\\|^2
}

where the attention weights are:

\\alpha(x_a,x_c)
=
\\operatorname{softmax}_{x_c}
\\left\[
\\operatorname{sim}
\\left(f_q(x_a),f_k(x_c)\\right)
\\right\]

This is a simplified mathematical rendering of Equation (2), with the paper's omitted projection and normalization details left out.

Let's derive it piece by piece.

### 3.1 Query, key, and value representations

The authors use three learnable functions:

Q=f_q(X)K=f_k(X)V=f_v(X)

Each is implemented using a dilated convolution network:

f_{\\{q,k,v\\}}(X)
=
\\operatorname{DilatedConvNet}_{\\{q,k,v\\}}(X)

Think of these as three separate feature extractors.

| Component | Role                                               |
| --------- | -------------------------------------------------- |
| Query (Q) | Describes the motif we want to reconstruct         |
| Key (K)   | Describes candidate motifs for matching            |
| Value (V) | Contains information used to reconstruct the motif |

Why three networks?

Because similarity and reconstruction are different operations.

A key can be useful for matching even if its corresponding value representation is optimized for reconstruction.

This is the same fundamental distinction used in Transformer attention.

### 3.2 Calculate the attention weights

For an anchor motif and candidate motif :

s_{ac}=f_q(x_a)^\\top f_k(x_c)

Then:

\\alpha_{ac}
=
\\frac{\\exp(s_{ac})}
{\\sum_j\\exp(s_{aj})}

Notice that:

\\sum_c \\alpha_{ac}=1

For every anchor motif, the model creates a probability distribution over candidate motifs.

The most relevant candidate motifs receive larger attention weights.

### 3.3 Reconstruct the anchor motif

The candidate values are combined:

\\hat{x}_a
=
\\sum_c \\alpha_{ac}f_v(x_c)

Here, is the reconstructed anchor motif.

Finally, the reconstruction error is:

e_a=\\|\\hat{x}_a-x_a\\|^2

Summing over the anchor motifs gives the distance.

The key intuition:

If candidate motifs can reconstruct the anchor motifs accurately, the two sequences have a small motif-based distance.

If reconstruction is poor, the distance is larger.

One anchor motif, three candidate motifs

Candidate A

### 0.70

Attention

Candidate B

### 0.20

Attention

Candidate C

### 0.10

Attention

Illustrative attention weights, not values reported by the paper.

\\hat{x}_a=0.7v_A+0.2v_B+0.1v_C

The model learns a weighted reconstruction rather than selecting exactly one nearest motif.

### 3.4 Why call this kernel regression?

The authors interpret this attention-weighted reconstruction as a form of kernel regression.

In kernel regression, observations that are more similar to a query contribute more strongly to its prediction.

Here:

* Query = anchor motif.

* Reference observations = candidate motifs.

* Kernel weights = attention weights.

* Prediction = reconstructed motif.

The difference is that the kernel is learned through neural networks.

This is a powerful idea because the model learns the notion of similarity itself.

### 4\. Why use dilated convolutions?

Now let's examine the architecture of the motif-distance network.

A standard convolution has limited receptive field.

For example, suppose we use kernel size:

k=3

With dilation:

d=1

The convolution accesses adjacent positions.

But if we increase dilation to , the convolution accesses positions with gaps:

\[t-4,t,t+4\]

![Improved Handwritten Digit Recognition Using Convolutional Neural Networks (CNN)](https://images.openai.com/static-rsc-4/wyx-_O9PQflmie4Dnb0NCqj-_CBsThKm4ylNtfvJ72CuMNk8HCRhoEbBr8tZpPOLSnBY6DsoSFNvQrdlIk6SPIukHoD2iLGfCuvvBzzi4zb7Z-OI3LdDsnxZ3lds2gbg4MtpZaJmmkaYGhqZE_WmtqeOkBKgQLu4A12Z9BQZav8-cDvJzSZO2sJVjICw32sb?purpose=fullsize)

The effective kernel size is:

k_{\\text{eff}}=1+(k-1)d

For example, with :

| Dilation | Effective kernel size |
| -------- | --------------------- |
| 1        | 3                     |
| 2        | 5                     |
| 4        | 9                     |
| 8        | 17                    |

This lets the network capture broader temporal context without requiring enormous convolution kernels.

Why is this useful for PPG?

A local waveform motif may need context beyond its immediate neighboring samples to distinguish it from an artifact or another waveform structure.

The authors use separate dilated convolution networks for Q, K, and V.

They also subsample the sequences with stride when calculating reconstruction distance.

This reduces the attention computation from approximately:

O(T^2)

to:

\\boxed{O((T/s)^2)}

For their input length of 12,000 time points:

\\frac{12,000}{10}=1,200

The attention matrix therefore operates on approximately 1,200 positions per sequence rather than 12,000.

The reduction in attention-matrix size is approximately:

\\frac{12,000^2}{1,200^2}=100100× smaller attention matrix

This is an important engineering decision: retain the ability to learn motifs from the full signal, while making pairwise reconstruction computationally feasible.

arXiv

### 5\. How is the motif-distance function trained without labels?

This is a particularly elegant part of the methodology.

At the beginning, the authors do not know whether two randomly selected PPG sequences belong to similar physiological states.

Therefore, they cannot directly supervise motif similarity between arbitrary sequences.

Instead, they construct a reconstruction task.

### 5.1 Create a masked query

Start with one PPG sequence:

X\\in\\mathbb{R}^{T\\times D}

Create two copies:

X_q=XX_k=X

Then apply a contiguous missingness mask to the query:

\\bar X_q=M(X_q)

The mask hides a contiguous segment of 2 seconds.

At a sampling rate of 50 Hz:

2\\times50=100

So 100 consecutive samples are hidden.

Masked reconstruction task

Conceptual illustration

●

●

●

●

●

●

●

●

?

?

?

?

●

●

●

●

●

●

●

●

Visible query

Masked 2-second region

Key sequence: original, unmasked PPG

Search for motifs that reconstruct the missing region

Reconstructed missing motif

The cross-attention mechanism learns to retrieve information from the key sequence that can reconstruct the masked query region.

### 5.2 Minimize reconstruction error

Conceptually, the training objective is:

\\mathcal L_{\\text{recon}}
=
\\sum_{t\\in\\mathcal M}
\\left\\|
\\hat X_q(t)-X(t)
\\right\\|^2

where is the masked region.

This is an explanatory expression of the masked reconstruction objective, not a claim that the paper specifies every implementation detail in precisely this notation.

The network learns which candidate motifs are useful for reconstruction.

After training, the learned distance function is used as a fixed similarity estimator during foundation-model pre-training.

Research interpretation: The model acquires a learned similarity function without needing physiological class labels.

This is an interesting form of self-supervision.

However, there is an assumption worth investigating:

> Does the ability to reconstruct a masked local waveform necessarily imply that the model has learned physiologically meaningful similarity?

Not always. A model could learn shortcuts based on local autocorrelation or repeated noise patterns.

That is one potential research gap.

### 6\. Relative contrastive learning — the second major stage

Now that we have a learned distance function, we can compare different PPG sequences.

Suppose we have:

X_a = \\text{anchor}

and a candidate set:

\\mathcal S_{\\text{cand}}
=
\\{X_1,X_2,\\ldots,X_N\\}

The learned motif-distance function calculates:

d(X_a,X_i)

for every candidate.

We can then compare the distances.

### 6.1 Construct the negative set

The paper defines:

\\boxed{
f_{\\text{neg}}(X_a,X_i,\\mathcal S)
=
\\left\\{
X\\in\\mathcal S:
d(X_a,X)>d(X_a,X_i)
\\right\\}
}

This is a crucial equation.

For every candidate :

* Treat as the positive.

* Select candidates farther from the anchor as negatives.

* Exclude candidates that are closer than the selected positive from its negative set.

Let's work through a numerical example.

Suppose the learned distances are:

| Candidate | Motif distance from anchor |
| --------- | -------------------------- |
| A         | 0.10                       |
| B         | 0.25                       |
| C         | 0.45                       |
| D         | 0.80                       |
| E         | 1.20                       |

If candidate C is selected as the positive:

d(X_a,C)=0.45

Then:

\\mathcal S_{\\text{neg}}=\\{D,E\\}

A and B are excluded because they are closer to the anchor than C.

Relative negative selection

Closer

A (0.10), B (0.25)

Selected positive

C (0.45)

Negatives

D (0.80), E (1.20)

0.10<0.25<0.45<0.80<1.20

### 6.2 Apply NT-Xent

For a given positive candidate, the paper uses:

\\ell(X_a,X_i,\\mathcal S_{\\text{neg}})
=
-\\log
\\frac{
\\exp(\\operatorname{sim}(z_a,z_i)/\\tau)
}{
\\exp(\\operatorname{sim}(z_a,z_i)/\\tau)
+
\\sum_{X_j\\in\\mathcal S_{\\text{neg}}}
\\exp(\\operatorname{sim}(z_a,z_j)/\\tau)
}

Here, represents the foundation-model embedding.

The important detail is that the positive is defined using the learned motif-distance ranking, rather than simply generating two augmented versions of the same sample.

### 6.3 Sum over all candidates

The final relative contrastive objective is:

\\boxed{
\\mathcal L_{\\text{RelCon}}
=
\\sum_{X_i\\in\\mathcal S_{\\text{cand}}}
\\ell
\\left(
X_a,
X_i,
f_{\\text{neg}}(X_a,X_i,\\mathcal S_{\\text{cand}})
\\right)
}

This is the paper's Equation (5).

The model is therefore trained against multiple relative similarity relationships, not just one positive and a fixed collection of negatives.

arXiv

### 7\. A deeper research critique: What could go wrong?

Now let's move beyond understanding the equations.

I want you to recognize three limitations that could motivate a publishable extension.

### Limitation A — Local motif matching ignores global ordering

Consider two sequences:

X_1=\[A,B,C,D\]X_2=\[A,C,B,D\]

Both contain exactly the same motifs.

A matching mechanism that only considers the best local matches may assign them relatively similar distances, despite their different temporal ordering.

This raises an important question:

Does the ordering of cardiac waveform patterns contain information that the current distance function overlooks?

Potential extension:

\\mathcal L_{\\text{new}}
=
\\mathcal L_{\\text{RelCon}}
+
\\lambda\\mathcal L_{\\text{temporal}}

Where the additional term encourages preservation of temporal ordering.

### Limitation B — Asymmetric distance

The motif distance is generally asymmetric:

d(X_a,X_b)\\neq d(X_b,X_a)

Why?

Because A reconstructs itself using motifs from B, whereas B reconstructs itself using motifs from A.

These are different reconstruction problems.

This means the learned distance is not necessarily a mathematical metric.

In particular, it may not satisfy:

d(A,B)=d(B,A)

or the triangle inequality:

d(A,C)\\leq d(A,B)+d(B,C)

Potential extension: investigate a symmetrized distance:

d_{\\text{sym}}(A,B)
=
\\frac{d(A,B)+d(B,A)}{2}

But don't assume symmetrization is automatically better. It could remove useful directional information.

### Limitation C — Noise may become a shortcut

Suppose a participant usually experiences motion artifacts while exercising.

The model might learn to associate those artifacts with exercise.

But what happens when the same participant wears a different watch or performs the same activity under different sensor-contact conditions?

The learned representation may fail.

Potential extension: explicitly separate physiological morphology from acquisition artifacts, then test generalization across devices and activities.

### 8\. What we have reconstructed so far

Pulse-PPG's mathematical workflow

* Raw PPG sequences

    Long 4-minute windows, sampled at 50 Hz.

* Dilated convolution feature extraction

    Construct Q, K and V representations.

* Cross-attention

    Match candidate motifs to anchor motifs.

* Reconstruction-based distance

    Measure how well candidate motifs reconstruct anchor motifs.

* Relative candidate selection

    Construct negative sets based on learned distance rankings.

* Relative contrastive learning

    Train the foundation encoder to capture these relationships.

* Pre-trained representations

    Reuse the encoder for downstream physiological tasks.

### 9\. Research-level knowledge check

These questions are deliberately more difficult than the previous lesson.

Research comprehension test

0/4

1. Why does Pulse-PPG use cross-attention in its motif-distance function?

To classify heart-rate zones

To reconstruct each anchor motif using weighted candidate motifs

To eliminate the need for convolution

To force all embeddings to be identical

2. Why is the distance function trained using a masked region from the same sequence?

To obtain manually annotated labels

To learn reconstruction-based motif matching without labels

To generate negative participants

To calculate heart rate directly

3. For a positive candidate at distance 0.45, which candidates are negatives?

All candidates

Only candidates with distance below 0.45

Candidates with distance greater than 0.45

Only candidates at distance exactly 0.45

4. What is a fundamental limitation of the motif-distance function?

It cannot use attention

It is guaranteed to satisfy the triangle inequality

It may be asymmetric and may not preserve global motif order

It requires physiological labels

Evaluate my understanding

### 10\. What we'll study in Lesson 4

Next: Mathematical deep dive

### Deriving Pulse-PPG from First Principles

We'll investigate:

* The exact tensor shapes throughout the distance network.

* Cross-attention equations and masking.

* The reconstruction objective and its gradients.

* Relative contrastive loss, including gradient behavior.

* Computational complexity and memory consumption.

* How to design a temporal-order-aware alternative.

We'll also start translating the mathematics into PyTorch pseudocode.

My research advice: Don't rush into proposing a new architecture yet. First understand whether the current objective learns a good similarity structure. A strong extension should improve the learning objective and demonstrate why the improvement matters—not merely add another neural-network block.

For reference, keep the original methodology open: [Pulse-PPG, Sections 3.2–4.1](https://arxiv.org/html/2502.01108v2?utm_source=chatgpt.com).
