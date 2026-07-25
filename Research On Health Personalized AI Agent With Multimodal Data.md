# Personalized Agentic Clinical Reasoning on Edge Devices

> A research vision for developing an intelligent, personalized healthcare assistant that performs physician-like clinical reasoning using multimodal health data and Large Language Models (LLMs).

---

# Motivation

Recent advances in Large Language Models (LLMs) have demonstrated impressive medical reasoning capabilities. However, existing medical LLMs primarily operate as question-answering systems, assuming that all relevant patient information is already available.

In real clinical practice, physicians rarely make decisions from a single interaction.

Instead, physicians:

1. Listen to the patient's complaint.
2. Form an initial hypothesis.
3. Request additional examinations or laboratory tests.
4. Analyze new evidence.
5. Update their clinical hypothesis.
6. Continue until sufficient confidence is achieved.
7. Recommend diagnosis or treatment.

This project aims to reproduce this physician-like reasoning process using LLMs.

---

# Vision

Develop an intelligent healthcare framework where a medical LLM behaves like an experienced physician that interactively requests personalized health information and continuously updates its clinical reasoning based on newly available evidence.

Unlike traditional medical chatbots, the system actively determines:

- What information is missing?
- Which health data should be requested next?
- Is additional testing necessary?
- Has enough evidence been collected?
- What is the most likely diagnosis?
- How confident is the decision?

---

# Core Idea

The LLM is **NOT** responsible for analyzing raw wearable signals.

Instead,

Specialized AI models first convert raw health data into clinically meaningful features.

The LLM then reasons over those structured features exactly like a physician reasons over laboratory reports.

This mimics real clinical workflows.

---

# System Architecture

```

Patient
│
├──────── Symptoms
├──────── Medical History
├──────── Wearable Devices
├──────── Mobile Health Records
├──────── Laboratory Reports
└──────── Questionnaires
│
▼
Feature Extraction Layer
│
├── ECG Model
├── Sleep Analysis Model
├── Activity Recognition Model
├── Laboratory Parser
├── Vital Sign Analysis
└── Medical Report Understanding
│
▼
Structured Patient Representation
│
▼
General Medical LLM
(Clinical Reasoning Engine)
│
├── Request additional information
├── Request another test
├── Update hypotheses
├── Estimate diagnostic confidence
├── Explain reasoning
└── Recommend clinical action
│
▼
Final Personalized Recommendation

```

---

# Philosophy

Think of the LLM as an experienced physician.

The physician already possesses extensive medical knowledge.

The physician does **not** need to relearn medicine whenever a new patient arrives.

Instead, the physician requests additional information until sufficient evidence is collected.

The proposed system follows the same philosophy.

---

# Why Fine-tuning May Not Be Necessary

A strong medical LLM already contains extensive medical knowledge.

Instead of fine-tuning the model for every patient, we provide personalized patient evidence during inference.

Therefore, personalization occurs through:

- personalized health data
- wearable features
- laboratory reports
- patient history
- conversational interaction

rather than modifying model parameters.

Potential techniques include:

- Prompt Engineering
- Retrieval-Augmented Generation (RAG)
- Tool Calling
- Feature Injection
- Context Memory

---

# Personalized Clinical Reasoning

The primary scientific contribution is **personalized clinical reasoning**.

Traditional Medical LLM:

```

Question
↓

Answer

```

Proposed Framework:

```

Symptoms
↓

Hypothesis Generation
↓

Request Missing Information
↓

Receive New Evidence
↓

Update Clinical Reasoning
↓

Need More Evidence?
│
├── Yes → Ask another question/test
└── No
↓

Final Recommendation

```

This closely resembles real physician workflows.

---

# Multimodal Fusion

The system integrates heterogeneous health information from multiple sources.

Possible modalities include:

- Wearable Sensors
- ECG
- Heart Rate
- HRV
- Sleep Data
- Blood Pressure
- SpO₂
- Step Count
- Physical Activity
- Laboratory Reports
- Medical Images (future)
- Electronic Health Records
- Medication History
- Lifestyle Information
- Patient Conversations

Each modality is processed by its own specialized feature extraction model.

The LLM reasons over the extracted clinical evidence.

---

# Edge AI Deployment

A long-term objective is complete deployment on edge devices.

Possible platforms:

- Smartphone
- Smartwatch
- Edge AI Accelerator
- Embedded Medical Devices

Advantages:

- Privacy Preservation
- Offline Operation
- Low Latency
- Reduced Cloud Cost
- Continuous Monitoring

---

# Research Questions

RQ1

Can a general medical LLM perform physician-like reasoning using personalized multimodal health information?

---

RQ2

Can an LLM actively determine which additional information should be requested before making a clinical decision?

---

RQ3

How can heterogeneous wearable, laboratory, and mobile health information be effectively fused into clinical reasoning?

---

RQ4

Can personalized clinical reasoning be efficiently deployed on resource-constrained edge devices?

---

# Novelty

This work is **NOT** about building another medical LLM.

Instead, it focuses on:

- Personalized clinical reasoning
- Interactive evidence acquisition
- Multimodal health data integration
- Physician-inspired reasoning workflow
- Edge AI deployment

---

# Potential Contributions

Contribution 1

A physician-inspired clinical reasoning framework.

---

Contribution 2

Interactive evidence acquisition.

The LLM decides which health information is most informative.

---

Contribution 3

Multimodal personalized health fusion.

---

Contribution 4

On-device personalized healthcare assistant.

---

# Example Workflow

Patient:

"I have chest pain."

↓

LLM:

"What is your age?"

↓

Patient:

"67"

↓

LLM:

"Please upload your ECG summary."

↓

ECG Feature Model

↓

ECG Features

↓

LLM:

"I also need your troponin laboratory result."

↓

Laboratory Report

↓

LLM:

Based on current evidence:

- Acute myocardial infarction probability
- Differential diagnosis
- Explanation
- Confidence estimate
- Recommendation

This iterative reasoning process mimics physician decision making.

---

# Expected Challenges

## Clinical

- Reliable reasoning
- Hallucination reduction
- Safe recommendations
- Clinical validation

---

## AI

- Multimodal fusion
- Long-context reasoning
- Tool calling
- Memory management

---

## Edge Computing

- Small model size
- Low latency
- Limited memory
- Battery efficiency

---

# Evaluation

Possible evaluation metrics include:

Clinical

- Diagnostic Accuracy
- Precision
- Recall
- AUROC
- F1 Score

Reasoning

- Clinical reasoning quality
- Appropriate follow-up questions
- Diagnostic confidence calibration
- Explanation quality

Efficiency

- Number of requested tests
- Time to diagnosis
- Computational latency
- Memory usage
- Energy consumption

Edge

- CPU utilization
- RAM usage
- Battery consumption

---

# Related Research Areas

This project lies at the intersection of:

- Medical Large Language Models
- Agentic AI
- Clinical Decision Support Systems
- Personalized Healthcare
- Digital Health
- Mobile Health (mHealth)
- Wearable AI
- Multimodal Learning
- Edge AI
- Human-AI Collaboration

---

# Recommended Reading

## Medical LLM Agents

- A Survey of LLM-based Agents in Medicine: How Far Are We from Baymax?

- ClinSeekAgent: Automating Multimodal Evidence Seeking for Agentic Clinical Reasoning

---

## Clinical Reasoning

- Reasoning LLMs in the Medical Domain

---

## Multimodal Medical AI

- Multimodal Large Language Models in Medical Research and Clinical Practice

- Towards Autonomous Decision-Making: A Survey of Multimodal Medical Reasoning

---

## Edge AI

- Medicine on the Edge: Comparative Performance Analysis of On-device LLMs for Clinical Reasoning

---

## Benchmarks

- AgentRx Benchmark

---

# Future Research Directions

- Personalized memory systems
- Continual patient monitoring
- Federated learning
- Privacy-preserving AI
- Explainable medical reasoning
- Medical knowledge graph integration
- Longitudinal health modeling
- Multi-agent clinical collaboration

---

# Long-term Vision

Build an AI physician assistant capable of:

- Understanding personalized health data.
- Interacting naturally with patients.
- Requesting the most informative clinical evidence.
- Reasoning like an experienced physician.
- Operating entirely on personal edge devices.
- Providing transparent, explainable, and personalized healthcare support while preserving patient privacy.

---

# Repository Structure (Proposed)

```
.
├── README.md
├── docs/
│   ├── architecture.md
│   ├── literature_review.md
│   ├── research_questions.md
│   └── roadmap.md
├── datasets/
├── models/
├── feature_extractors/
├── reasoning_engine/
├── edge_deployment/
├── experiments/
├── evaluation/
├── figures/
└── references/
```

---

# Current Status

**Stage:** Research Concept

**Next Steps:**

- Conduct comprehensive literature review
- Define system architecture
- Select a medical LLM
- Design multimodal feature extraction modules
- Develop interactive reasoning framework
- Build evaluation benchmarks
- Prototype edge deployment
- Prepare conference submission
- 
---

# 📚 Curated Literature Roadmap

> This repository maintains a living collection of research papers related to Personalized Agentic Clinical Reasoning, Medical LLMs, Wearable AI, Multimodal Learning, and Edge Intelligence.

---

# Reading Priority

| Priority | Meaning |
|----------|---------|
| 🔥 | Must Read Immediately |
| ⭐⭐⭐⭐⭐ | Essential |
| ⭐⭐⭐⭐ | Highly Recommended |
| ⭐⭐⭐ | Useful |
| ⭐⭐ | Background Reading |

---

# Reading Status

| Status | Meaning |
|---------|---------|
| ⬜ | Not Started |
| 🟨 | Reading |
| 🟩 | Completed |
| 📝 | Notes Completed |
| 💻 | Code Explored |

---

# Research Categories

| ID | Area | Target Papers |
|----|------|--------------:|
| 01 | Medical LLMs | 15 |
| 02 | Agentic AI | 10 |
| 03 | Clinical Reasoning | 10 |
| 04 | Multimodal Learning | 10 |
| 05 | Wearable AI | 10 |
| 06 | Mobile Health | 8 |
| 07 | Edge AI | 10 |
| 08 | Personalized Medicine | 8 |
| 09 | Federated Learning | 8 |
| 10 | Explainable AI | 8 |
| 11 | Healthcare Benchmarks | 8 |
| 12 | Digital Twins | 5 |

Target Total Papers ≈ 110

---

# 01 Medical Large Language Models

| Priority | Paper | Year | Venue | Summary | Code | Paper | Status |
|----------|------|------|-------|----------|------|-------|--------|
| 🔥 | Med-PaLM | 2023 | Nature | First major medical LLM | ✓ | ✓ | ⬜ |
| 🔥 | Med-PaLM 2 | 2024 | Nature | Improved clinical reasoning | ✓ | ✓ | ⬜ |
| 🔥 | A Survey of LLM-based Agents in Medicine | 2025 | ACL Findings | Complete survey | — | ✓ | ⬜ |
| ⭐⭐⭐⭐⭐ | HuatuoGPT | 2023 | arXiv | Open-source medical LLM | ✓ | ✓ | ⬜ |
| ⭐⭐⭐⭐ | DISC-MedLLM | 2024 | arXiv | Medical instruction tuning | ✓ | ✓ | ⬜ |
| ⭐⭐⭐⭐ | DoctorGLM | 2023 | arXiv | Chinese medical LLM | ✓ | ✓ | ⬜ |
| ⭐⭐⭐⭐ | PMC-LLaMA | 2023 | arXiv | Biomedical foundation model | ✓ | ✓ | ⬜ |

---

# 02 Agentic AI

| Priority | Paper | Summary | Status |
|----------|---------|--------|
| 🔥 | ClinSeekAgent | Closest paper to our idea | ⬜ |
| 🔥 | Agent Hospital | Multi-agent healthcare | ⬜ |
| ⭐⭐⭐⭐⭐ | AutoGen | Multi-agent framework | ⬜ |
| ⭐⭐⭐⭐ | ReAct | Reasoning + Acting | ⬜ |
| ⭐⭐⭐⭐ | Toolformer | Tool usage | ⬜ |
| ⭐⭐⭐⭐ | HuggingGPT | AI collaboration | ⬜ |

---

# 03 Clinical Reasoning

| Priority | Paper | Summary | Status |
|----------|------|----------|--------|
| 🔥 | Reasoning LLMs in the Medical Domain | Medical reasoning survey | ⬜ |
| ⭐⭐⭐⭐⭐ | Chain-of-Thought Prompting | Reasoning | ⬜ |
| ⭐⭐⭐⭐⭐ | Tree-of-Thought | Search reasoning | ⬜ |
| ⭐⭐⭐⭐ | Graph-of-Thought | Structured reasoning | ⬜ |
| ⭐⭐⭐⭐ | MedPrompt | Medical prompting | ⬜ |

---

# 04 Multimodal Learning

| Priority | Paper | Summary | Status |
|----------|------|----------|--------|
| 🔥 | Multimodal LLMs in Medical Research | Complete survey | ⬜ |
| ⭐⭐⭐⭐⭐ | LLaVA-Med | Medical vision-language | ⬜ |
| ⭐⭐⭐⭐ | BioViL | Medical representation | ⬜ |
| ⭐⭐⭐⭐ | Med-Flamingo | Medical multimodal | ⬜ |

---

# 05 Wearable AI

| Priority | Paper | Summary | Status |
|----------|------|----------|--------|
| 🔥 | Foundation Models for Wearable Health | Survey | ⬜ |
| ⭐⭐⭐⭐⭐ | Time-Series Foundation Models | Wearables | ⬜ |
| ⭐⭐⭐⭐ | ECG Foundation Models | ECG | ⬜ |
| ⭐⭐⭐⭐ | Sleep Foundation Models | Sleep | ⬜ |

---

# 06 Mobile Health

| Priority | Paper | Summary | Status |
|----------|------|----------|--------|
| 🔥 | Mobile Health Survey | mHealth overview | ⬜ |
| ⭐⭐⭐⭐⭐ | Smartphone Health Monitoring | Continuous monitoring | ⬜ |
| ⭐⭐⭐⭐ | Digital Biomarkers | Personalized medicine | ⬜ |

---

# 07 Edge AI

| Priority | Paper | Summary | Status |
|----------|------|----------|--------|
| 🔥 | Medicine on the Edge | Medical LLM deployment | ⬜ |
| ⭐⭐⭐⭐⭐ | TinyML Survey | Tiny models | ⬜ |
| ⭐⭐⭐⭐ | Edge Intelligence Survey | AI deployment | ⬜ |
| ⭐⭐⭐⭐ | MobileLLM | Efficient LLM | ⬜ |

---

# 08 Personalized Medicine

| Priority | Paper | Summary | Status |
|----------|------|----------|--------|
| 🔥 | Personalized Healthcare Foundation Models | Future healthcare | ⬜ |
| ⭐⭐⭐⭐⭐ | Precision Medicine Review | Clinical personalization | ⬜ |
| ⭐⭐⭐⭐ | Digital Phenotyping | Patient modeling | ⬜ |

---

# 09 Federated Learning

| Priority | Paper | Summary | Status |
|----------|------|----------|--------|
| 🔥 | Federated Learning Survey | Privacy | ⬜ |
| ⭐⭐⭐⭐⭐ | FedAvg | Classic | ⬜ |
| ⭐⭐⭐⭐ | Medical Federated Learning | Healthcare | ⬜ |

---

# 10 Explainable AI

| Priority | Paper | Summary | Status |
|----------|------|----------|--------|
| 🔥 | Explainable Medical AI Survey | XAI | ⬜ |
| ⭐⭐⭐⭐⭐ | SHAP | Interpretability | ⬜ |
| ⭐⭐⭐⭐ | LIME | Interpretability | ⬜ |

---

# 11 Benchmarks

| Priority | Paper | Summary | Status |
|----------|------|----------|--------|
| 🔥 | AgentRx | Medical agent benchmark | ⬜ |
| ⭐⭐⭐⭐⭐ | MedQA | QA benchmark | ⬜ |
| ⭐⭐⭐⭐⭐ | PubMedQA | QA | ⬜ |
| ⭐⭐⭐⭐ | MMLU-Med | Medical reasoning | ⬜ |

---

# 12 Digital Twins

| Priority | Paper | Summary | Status |
|----------|------|----------|--------|
| ⭐⭐⭐⭐⭐ | Digital Twins in Healthcare Survey | Personalized digital patients | ⬜ |
| ⭐⭐⭐⭐ | Human Digital Twin | Longitudinal modeling | ⬜ |

---

# Personal Reading Dashboard

## Statistics

Target Papers: 110

Completed: 0

Reading: 0

Need Notes: 0

---

## Progress

```

□□□□□□□□□□

0%

```

---

# Personal Notes

Each paper will have its own note under

/docs/literature/

Example

```

docs/
literature/
├── MedPaLM.md
├── ClinSeekAgent.md
├── AgentHospital.md
├── LLaVAMed.md
├── MedicineOnTheEdge.md
├── MedPrompt.md

```

Each note will contain

- Abstract
- Main Idea
- Architecture
- Dataset
- Evaluation
- Strengths
- Weaknesses
- Figures
- Future Work
- Relation to Our Project
- My Ideas

# License

This repository currently documents an ongoing research idea and serves as the conceptual foundation for future implementation.
