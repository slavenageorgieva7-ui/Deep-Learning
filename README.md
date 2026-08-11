AML Knowledge Assistant

AI-powered decision-support prototype for Anti-Money Laundering (AML) investigations, combining a supervised machine learning transaction classifier with a Retrieval-Augmented Generation (RAG) knowledge assistant.

Deep Learning Final Project — 2026

1. Overview

This project explores how machine learning and Retrieval-Augmented Generation can support AML analysts in two complementary ways:

Transaction risk detection — a supervised classifier that flags potentially suspicious transactions in a large, highly imbalanced dataset.
AML knowledge retrieval — a RAG pipeline that retrieves relevant Belgian AML rules, legal references, and practical interpretations to support case analysis and reporting.

The system is designed as a decision-support tool. It does not replace human AML analysts and does not make autonomous compliance decisions.

2. Problem Statement

AML investigations require analysts to review large volumes of transaction activity, identify unusual patterns, consult regulatory documentation, and prepare investigation reports — a process that is time-consuming and draws on multiple information sources.

This project investigates:

Can a machine learning classifier combined with a Retrieval-Augmented Generation knowledge assistant support AML analysts in prioritising suspicious transactions and retrieving relevant AML knowledge?

3. Research Questions
RQ1 — Can a supervised ML model reliably prioritise suspicious transactions in a realistically imbalanced, time-based evaluation setting?
RQ2 — Does Retrieval-Augmented Generation improve the grounding and relevance of AML-related answers compared with a generic response?
RQ3 — Can a rule-based case analyzer identify meaningful AML red flags and risk levels from transaction scenarios?
RQ4 — How do different classification thresholds and review-capacity levels affect the practical usefulness of the model for an AML investigation team?
RQ5 — Can the system generate a structured, useful Suspicious Activity Report (SAR) draft from an assessed case?
4. What the System Actually Does
4.1 Transaction Classification (Machine Learning)

Three supervised models — Logistic Regression, Decision Tree, and Random Forest — are trained to classify transactions as laundering / non-laundering on the IBM HI-Large synthetic AML transaction dataset.

Random Forest was selected as the final model based on the best overall balance of Precision, F1-score, ROC-AUC, and PR-AUC on the validation set.

Final test-set performance (Random Forest):

Metric	Value
Precision	2.01%
Recall	72.07%
F1-score	3.92%
ROC-AUC	94.77%
PR-AUC	3.88%

Confusion matrix (test set): TN 237,082 · FP 12,560 · FN 100 · TP 258.

Given the extreme class imbalance (~1.6% positive class), the low Precision is expected and is discussed explicitly in the notebook rather than hidden behind ROC-AUC alone.

4.2 AML Knowledge Base + RAG Retrieval

A Belgian AML knowledge base (10 curated entries covering AML/CFT legislation, risk-based approach, customer due diligence, transaction monitoring, AMLCO escalation, etc.) is embedded with a Sentence Transformer model (384-dimensional embeddings) and indexed with FAISS for semantic search.

Given a question, the system retrieves the top-k most relevant knowledge base entries (topic, rule text, legal reference, source, practical interpretation).

This is a retrieval system, not a generative one. The assistant returns retrieved AML knowledge directly — it does not currently pass that context to a generative language model to produce a free-form answer. This is stated explicitly as a limitation (see §7).

4.3 AML Case Analyzer

Given a transaction scenario (amount received, number of senders, rapid outgoing transfer, profile mismatch), the analyzer:

Checks four rule-based red flags (high-value transaction ≥ €50,000, ≥3 unrelated senders, rapid outgoing movement, profile inconsistency).
Computes a risk score and assigns a risk level (LOW / MEDIUM / HIGH).
Retrieves relevant Belgian AML knowledge for the scenario.
Prints recommended investigation actions based on the risk level.
4.4 SAR Draft Generator

Produces a structured Suspicious Activity Report draft (case summary, risk assessment, indicators, relevant AML knowledge, recommended next steps, analyst conclusion) from the same case inputs. The output is explicitly labelled as a draft for AML analyst / AMLCO review, not an auto-submitted report.

4.5 Baseline vs RAG Comparison

A generic predefined response is compared against the RAG-based retrieval on three evaluation questions, measuring legal grounding and topic coverage. The RAG approach achieved 100% legal grounding and 100% topic coverage on this small evaluation set.

Note: the "baseline" here is a static predefined sentence, not an independent generative LLM run without retrieval. This comparison illustrates the value of grounding in a knowledge base, but is not a full LLM-vs-LLM+RAG benchmark (see Limitations).

5. Methodology
Data Acquisition (IBM HI-Large, 190M+ transactions, chunked reading)
        ↓
Data Cleaning & Validation
        ↓
Exploratory Data Analysis
        ↓
Time-Based Train / Validation / Test Split
  (Aug 2022 → Sep 2022 → Oct 2022, proportional sampling)
        ↓
Feature Engineering (time features, same-bank, cross-bank, currency match)
        ↓
Preprocessing (StandardScaler + One-Hot Encoding)
        ↓
Model Training (Logistic Regression, Decision Tree, Random Forest)
        ↓
Threshold / Capacity / PR & ROC Evaluation
        ↓
Belgian AML Knowledge Base → Sentence Embeddings → FAISS Index
        ↓
RAG Retrieval → Case Analyzer → SAR Draft Generator
        ↓
End-to-End Testing
Evaluation principles applied
Original class distribution preserved — no artificial oversampling.
Minority-class metrics (Precision, Recall, F1, PR-AUC) used instead of Accuracy as the primary measure.
Time-based split, not random split — training on August 2022, validating on September, testing on October, to avoid look-ahead bias.
Categorical variables (currency, payment format) encoded with One-Hot Encoding, not ordinal, to avoid implying a false order.
Classification threshold and AML review-capacity trade-offs analysed explicitly (top-100 to top-10,000 review scenarios).
6. Data
IBM HI-Large Transactions — large-scale synthetic AML transaction dataset (~190M rows), read in chunks; ~1.6% of transactions labelled as laundering.
Belgian AML Knowledge Base — 10 manually curated entries based on NBB, CTIF-CFI, and EBA guidance (see References).
7. Limitations
Dataset is synthetic; results should not be read as evidence of real-world production performance.
Precision is low (2%) at default thresholds — the model is a prioritisation tool, not an autonomous classifier; capacity/threshold analysis should guide deployment.
The Belgian AML knowledge base is small (10 entries) — not a production-scale legal corpus.
RAG evaluation used only 3 predefined questions — too small to generalise.
No generative LLM is used. The "baseline vs RAG" comparison uses a static predefined sentence as baseline, not an independent LLM run. This is a known gap between the original project brief (Transformer LM + RAG) and the current implementation, which is retrieval-only.
Account-level leakage between train/validation/test splits (same account/bank appearing across periods) has not yet been explicitly checked.
No probability calibration analysis has been performed.
Not evaluated in a live banking environment; no data security, governance, or monitoring considerations addressed.
8. Future Work
Add a genuine generative model (e.g. a small open-weight LLM) on top of the retrieved context to produce free-form generated answers, and re-run baseline-vs-RAG with that model both with and without retrieval.
Expand red-flag rules to cover unusual frequency, structuring patterns, geographic risk, and behavioural change over time.
Add explicit account-level leakage checks and account-level evaluation.
Add probability calibration analysis.
Expand the Belgian AML knowledge base and the RAG evaluation set.
Add qualitative false positive / false negative case review.
9. Technologies Used

Python, Jupyter Notebook, pandas, NumPy, scikit-learn, matplotlib, sentence-transformers, FAISS (faiss-cpu).

10. How to Run
Open AML_Knowledge_Assistant.ipynb in Jupyter.
Install dependencies: pip install pandas numpy scikit-learn matplotlib sentence-transformers faiss-cpu.
Update the dataset path to point to the local copy of the IBM HI-Large transactions CSV.
Run all cells in order — data loading and sampling of the full dataset can take several minutes due to file size.
11. References
National Bank of Belgium (NBB). Anti-Money Laundering Law of 18 September 2017.
National Bank of Belgium (NBB). Anti-Money Laundering Regulation of the NBB of 21 November 2017.
National Bank of Belgium (NBB). AML/CFT – Definitions.
National Bank of Belgium (NBB). Main Reference Documents – Combating Money Laundering and Financing of Terrorism.
Financial Intelligence Processing Unit (CTIF-CFI). Obligations of Reporting Entities.
European Banking Authority (EBA). Guidelines on Risk-Based Supervision.
European Banking Authority (EBA). Guidelines on ML/TF Risk Factors.
IBM. IBM Transactions for Anti-Money Laundering (HI-Large).
SAML-D. Synthetic Anti-Money Laundering Dataset.
Reimers, N. & Gurevych, I. (2019). Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks. EMNLP 2019.
Johnson, J., Douze, M., & Jégou, H. (2017). Billion-scale similarity search with GPUs. IEEE Transactions on Big Data.
Disclaimer

This is an educational research prototype. It does not make AML compliance decisions, does not replace professional AML investigation, and any generated SAR draft requires
