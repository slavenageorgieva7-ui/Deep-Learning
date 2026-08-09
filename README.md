# AML Knowledge Assistant

## AI-Powered Assistant for Anti-Money Laundering Investigations

---

## 1. Overview

AML Knowledge Assistant is a Deep Learning project that explores how Transformer-based Language Models and Retrieval-Augmented Generation (RAG) can support Anti-Money Laundering (AML) investigations.

The project aims to develop an AI-powered knowledge assistant that can help AML analysts understand AML concepts, analyze transaction scenarios, identify potential red flags, retrieve relevant regulatory information, assess risk, and generate structured investigation reports.

The system is designed as a decision-support tool and does not replace human AML analysts or make final compliance decisions.

---

## 2. Problem Statement

Anti-Money Laundering investigations require analysts to review transaction activity, identify unusual patterns, consult regulatory and AML documentation, and prepare investigation reports.

This process can be time-consuming and requires information from multiple sources.

The main problem addressed by this project is:

> Can a Transformer-based AI assistant combined with Retrieval-Augmented Generation (RAG) support AML analysts in analyzing transaction scenarios and retrieving relevant AML knowledge?

The project focuses on applying Deep Learning, Transformers, Language Models, and RAG to a real-world financial crime investigation problem.

---

## 3. Project Objectives

The main objectives of the project are:

- Develop an AI-powered AML knowledge assistant.
- Explore the use of Transformer-based Language Models for AML-related tasks.
- Implement a Retrieval-Augmented Generation (RAG) pipeline.
- Build an AML knowledge base using relevant documentation.
- Analyze transaction scenarios and identify potential AML red flags.
- Provide a structured risk assessment.
- Explain the reasons behind the identified risk indicators.
- Recommend appropriate investigation actions.
- Generate a draft Suspicious Activity Report (SAR).
- Evaluate the performance of the implemented approach.
- Compare different approaches and document the results.

---

## 4. Main Features

### 4.1 AML Knowledge Assistant

The assistant can answer questions related to:

- Anti-Money Laundering (AML)
- Know Your Customer (KYC)
- Enhanced Due Diligence (EDD)
- Transaction Monitoring
- Suspicious Activity
- Structuring
- Layering
- Money Mule Activity
- Risk Indicators
- Customer Risk
- Transaction Risk

### 4.2 Transaction and Case Analysis

The system can analyze AML transaction scenarios and identify potential risk indicators.

Example:

    Customer receives 25 incoming transactions.
    Average transaction amount: €950
    Number of senders: 8
    Countries involved: 3
    Time period: 48 hours

The assistant can provide:

- Risk Level
- Potential Red Flags
- Explanation
- Recommended Investigation Actions

### 4.3 Red Flag Identification

The system investigates potential AML indicators such as:

- Unusual transaction frequency
- Multiple counterparties
- Structuring patterns
- Rapid movement of funds
- Unusual transaction amounts
- Geographic risk indicators
- Transactions inconsistent with the expected customer profile
- Unusual changes in customer behaviour

### 4.4 Risk Assessment

The assistant can classify an investigated case into a risk category:

- LOW
- MEDIUM
- HIGH

The risk assessment is supported by identified transaction characteristics and AML indicators.

The final risk assessment is intended to support human investigation and does not represent an autonomous compliance decision.

### 4.5 Retrieval-Augmented Generation (RAG)

The project implements Retrieval-Augmented Generation to provide the Language Model with relevant information from an AML knowledge base.

Instead of relying only on the model's internal knowledge, relevant documents are retrieved and supplied as context before generating an answer.

The general workflow is:

    User Question
          ↓
    Query Processing
          ↓
    Text Embedding
          ↓
    Vector Search
          ↓
    Relevant Documents
          ↓
    Retrieved Context
          ↓
    Language Model
          ↓
    Generated Answer

### 4.6 SAR Generation

The system can generate a structured draft of a Suspicious Activity Report (SAR) based on the information provided during an investigation.

The generated report is intended as a draft for human review and is not automatically submitted to a regulatory authority.

---

## 5. Methodology

The project follows the following workflow:

    Data Acquisition
           ↓
    Data Cleaning
           ↓
    Exploratory Data Analysis
           ↓
    Feature Engineering
           ↓
    Transformer / Language Model
           ↓
    Text Embeddings
           ↓
    Vector Database
           ↓
    RAG Pipeline
           ↓
    AML Case Analysis
           ↓
    Risk Assessment
           ↓
    SAR Generation
           ↓
    Testing and Evaluation
           ↓
    Results and Conclusions

---

## 6. Data

The project uses financial transaction data and AML-related textual information.

The data preparation process includes:

1. Data acquisition
2. Data inspection
3. Data cleaning
4. Missing-value handling
5. Data transformation
6. Feature engineering
7. AML case preparation
8. Preparation of testing data

Where appropriate, synthetic AML cases may also be generated for testing and evaluation.

The final datasets and their sources will be documented in the Jupyter Notebook.

---

## 7. Deep Learning Approach

The project focuses on Deep Learning techniques related to Natural Language Processing and Language Models.

The research includes:

- Tokenization
- Text embeddings
- Transformer architectures
- Attention mechanisms
- Language Models
- Retrieval-Augmented Generation
- Vector similarity search

Different approaches may be implemented and compared as part of the research.

---

## 8. Research Questions

The project investigates the following research questions:

### RQ1

Can Transformer-based Language Models assist with AML-related knowledge and investigation tasks?

### RQ2

Can Retrieval-Augmented Generation improve the relevance and reliability of AML-related answers?

### RQ3

Can an AI-based assistant identify potential AML red flags from transaction scenarios?

### RQ4

How does an LLM-based approach compare with alternative approaches?

### RQ5

Can the system provide useful explanations and investigation recommendations?

---

## 9. Previous Research

The project builds upon previous research in the following areas:

- Deep Learning
- Natural Language Processing
- Transformer architectures
- Large Language Models
- Retrieval-Augmented Generation
- Financial Crime Detection
- Anti-Money Laundering

Relevant academic papers, technical documentation, and AML sources will be referenced and discussed in the final Jupyter Notebook.

The project will include comparisons between the implemented approach and relevant previous approaches where applicable.

---

## 10. Evaluation

The system will be evaluated using predefined AML test cases.

Depending on the implemented models and classification tasks, the following metrics may be used:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix

The RAG component will also be evaluated based on the relevance of retrieved information and the quality of generated responses.

The project will include comparisons between different approaches, including the use of an LLM without retrieval and an LLM combined with RAG.

Final evaluation results will be added after the experiments are completed.

---

## 11. Visualization

The project will include visualizations to support the analysis and evaluation.

Examples include:

- Suspicious vs. non-suspicious transactions
- Transaction amount distributions
- Transaction frequency
- Geographic distributions
- Risk-level distributions
- Red flag frequency
- Confusion Matrix
- Model performance comparison
- Evaluation metrics

All visualizations will be created and explained in the Jupyter Notebook.

---

## 12. Project Structure

    AML-Knowledge-Assistant/
    │
    ├── AML_Knowledge_Assistant_Final_Project.ipynb
    ├── app.py
    │
    ├── data/
    │   ├── raw/
    │   └── processed/
    │
    ├── documents/
    │   └── aml_knowledge/
    │
    ├── src/
    │   ├── preprocessing.py
    │   ├── embeddings.py
    │   ├── rag.py
    │   ├── aml_analyzer.py
    │   └── report_generator.py
    │
    ├── figures/
    │
    ├── tests/
    │
    ├── requirements.txt
    └── README.md

---

## 13. Technologies

The project is primarily developed using Python and Jupyter Notebook.

Main technologies and libraries include:

- Python
- Jupyter Notebook
- PyTorch
- Hugging Face Transformers
- Sentence Transformers
- LangChain
- FAISS
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Streamlit

The final dependencies will be documented in `requirements.txt`.

---

## 14. Testing

Testing will be performed using predefined AML scenarios.

The testing process will evaluate:

- Risk classification
- Red flag identification
- Retrieval relevance
- Generated answers
- SAR generation
- Overall system behaviour

Where applicable, automated tests and quantitative evaluation metrics will be used.

The final testing results will be documented in the Jupyter Notebook.

---

## 15. Results

The final results will present the outcomes of the experiments and evaluations performed during the project.

The analysis will include:

- Model performance
- Risk classification performance
- Red flag identification results
- RAG retrieval performance
- Comparison between different approaches
- Examples of generated AML analyses

All reported results will be based on the actual experiments conducted during the project.

---

## 16. Limitations

The AML Knowledge Assistant is an educational and research project.

The system has several limitations:

- It does not make final AML compliance decisions.
- Generated responses may contain errors.
- Risk assessments depend on the quality and completeness of the input data.
- Synthetic data may not fully represent real-world financial activity.
- The system should not replace professional AML investigation.
- Regulatory requirements may vary between jurisdictions.
- Human review remains essential.

---

## 17. Future Improvements

Possible future improvements include:

- Fine-tuning a specialized AML Language Model
- Integration with real-time transaction monitoring systems
- Graph-based transaction analysis
- Network analysis of related accounts
- Improved explainability
- Integration with additional regulatory sources
- Multilingual AML analysis
- Automated case prioritization
- OCR and document analysis for KYC documentation
- Integration with real banking investigation workflows

---

## 18. Conclusion

The AML Knowledge Assistant demonstrates how Deep Learning, Transformer-based Language Models, embeddings, and Retrieval-Augmented Generation can be applied to a real-world Anti-Money Laundering problem.

The project combines financial transaction analysis with an AML knowledge base to support analysts in identifying potential risk indicators, retrieving relevant AML information, and generating structured investigation outputs.

The final evaluation will determine how effectively the proposed approach can support AML-related tasks and whether the addition of RAG improves the quality and relevance of the generated responses.

The system is designed as a decision-support tool, with human review remaining an essential part of the AML investigation process.

---

Deep Learning Final Project

2026
