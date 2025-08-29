# 📑 Master's Thesis – Detecting Fraudulent Intent in MD&A Sections Using Transformer-based NLP  

This repository contains all data (processed), source code, model outputs, and experimental results for my Master’s thesis:

> **Detecting Fraudulent Intent in Management Discussion & Analysis (MD&A) Sections of SEC Filings Using Transformer-Based NLP Models**

🎓 **University of Ottawa — Master’s in Digital Transformation & Innovation (Data Science)**  
📅 Completion: August 2025  

---

## 📘 Thesis Overview  

This thesis explores how **transformer-based language models** can detect **fraudulent intent** in the *Management Discussion & Analysis (MD&A)* sections of annual 10-K filings submitted to the U.S. Securities and Exchange Commission (SEC). Unlike numerical anomalies, linguistic signals in MD&A can reveal subtle patterns of deception.  

We experiment with **FinBERT, BERT, RoBERTa, and DeBERTa**, and apply **transfer learning** from fake news detection to improve model generalization in a low-resource financial fraud domain.

---

## 📚 Datasets  

### 📄 MD&A Fraud Dataset  
- Source: SEC 10-K filings  
- Labels: Derived from AAER enforcement actions  
- Format: Document-level, raw MD&A text  
- Size: 116 documents (58 fraud, 58 non-fraud)  

### 📰 Fake News Dataset (for Transfer Learning)  
- Source: Kaggle (Fake and Real News dataset)  
- Size: ~44,000 articles  
- Label: Fake / Real  
- Purpose: Proxy task for deception detection  

---

## 🧪 Experiments  

We conduct multiple experiments across three main axes:
- Model architecture (FinBERT, BERT, RoBERTa, DeBERTa)
- Transfer learning strategy
- Text input handling (full vs. chunked)

### 🔁 Transfer Learning Strategy

One of the core challenges in fraud detection within financial text is the **limited availability of labeled data**, especially at the document level. To overcome this, we adopt a **two-stage transfer learning strategy**, leveraging a high-resource deception detection task (fake news classification) to bootstrap learning on our low-resource MD&A dataset.

####  Stage 1 — Pretraining on Fake News
- A model (e.g., FinBERT, DeBERTa) is fine-tuned on a large **fake news classification dataset**, learning to distinguish deceptive vs. truthful language.
- This stage enables the model to capture **domain-agnostic deception cues**, such as hedging, exaggeration, or overly positive framing.

####  Stage 2 — Fine-Tuning on MD&A (Fraud Detection)
- The pretrained model is further fine-tuned on a small but carefully curated MD&A dataset labeled as **fraudulent or non-fraudulent** based on SEC enforcement actions.
- Using **sliding window chunking**, the full MD&A documents are split into overlapping segments, allowing the model to process long-form text and aggregate predictions.

####  Why Transfer Learning?
- Fraudulent intent is often **subtle and context-dependent**, making it hard to learn from limited data alone.
- Transfer from fake news (a deception-rich domain) allows the model to learn generalized linguistic patterns of **manipulation, obfuscation, or misleading optimism**, which are also found in fraudulent corporate disclosures.

This strategy consistently improved performance, particularly in **fraud recall**, making it valuable in high-stakes domains where missing fraud is costly.

