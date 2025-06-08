# Fair and Safe AI for Alzheimer's Disease Detection

This project explores the use of multimodal machine learning and large language models (LLMs) to detect Alzheimer's Disease (AD) from electronic health records (EHRs), with a focus on **fairness** and **AI safety** across demographic groups. I partnernerd with Harvard Medical School for the study of this project, advised by Sudeshna Das, Ph.D.

## 🧠 Project Overview

We build and compare two core models for AD detection:
1. **Multimodal Model**: Combines structured EHR data (e.g., age, comorbidities) with Gemini-generated summaries of clinical notes.
2. **LLM-Only Model**: Uses Gemini (Google Cloud) to predict AD likelihood from free-text notes and demographic prompts.

To ensure fairness, we rigorously evaluated **demographic biases** across age, sex, and race using standard fairness metrics. Prompt engineering and dimensionality reduction techniques were applied to mitigate model hallucination and disparity.

## 📊 Dataset

- **MIMIC-IV & MIMIC-IV-Note**: A large-scale, de-identified EHR dataset of ICU patients from Beth Israel Deaconess Medical Center.
- **Cohort Construction**: Matched case-control setup using propensity score matching to reduce confounding.

## 🔍 Key Features

- **Multimodal Learning**: Fusion of structured tabular data and LLM-summarized text
- **Prompt Engineering**: Masked and structured prompts for safe clinical inference
- **Bias Analysis**:
  - Equal Opportunity
  - Predictive Parity
  - Equalized Odds
- **Statistical Evaluation**: Chi-squared test, two-proportion z-test

## ⚙️ Technologies & Tools

- **ML Models**: `LightGBM`, `Logistic Regression`
- **LLMs**: `Gemini` via Google Cloud API
- **NLP**: `ClinicalBERT`, prompt engineering, summarization
- **Fairness Evaluation**: `Fairlearn`, `scikit-learn`, `pandas`, `seaborn`
- **Dimensionality Reduction**: `PCA` on Gemini-generated features
- **Causal Inference**: Propensity score matching

## 📈 Results

- Multimodal models outperformed LLM-only baselines in accuracy and fairness.
- Prompt design and feature selection critically influenced demographic equity.
- Highlighted safety concerns where hallucinated LLM outputs may amplify bias.

## 🚀 Future Work

- Integrate retrieval-augmented generation (RAG) to ground LLMs in verified data
- Expand fairness analysis to intersectional groups
- Explore fine-tuning strategies for clinical LLM safety

