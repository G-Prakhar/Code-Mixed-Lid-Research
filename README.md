# Code-Mixed Language Identification & Normalization Research

## Overview
This project explores **token-level language identification (LID)** for **Hindi–English code-mixed text**, focusing on challenges caused by **Romanized Hindi spelling variation and mixed morphology**.

Modern multilingual transformers often struggle with noisy social media text where Hindi words are written in Latin script (e.g., *bahut*, *bohot*, *boht*). These spelling variations create **tokenization fragmentation**, increasing vocabulary sparsity and degrading model performance.

This repository investigates whether a **Romanized Hindi normalization pipeline** can reduce tokenizer fragmentation and improve the performance of multilingual transformer models.

---

## Research Hypothesis
Massively multilingual models struggle with token-level language identification in code-mixed Hindi-English text due to **vocabulary sparsity from non-standard Romanized spelling**.

We hypothesize that applying a **normalization step before tokenization** will reduce subword fragmentation and improve **Macro-F1 scores** for token-level language identification.

---

## Research Questions
1. How do multilingual transformer models perform on token-level LID for code-mixed Hindi-English text?
2. Does Romanized Hindi normalization improve tokenization efficiency and classification accuracy?
3. How much does normalization reduce **subword fragmentation** in transformer tokenizers?

---

## Model Architecture

Primary model used in this study:

- **XLM-RoBERTa** – multilingual transformer trained on large-scale multilingual corpora.

### Pipeline

```
Code-mixed text
       ↓
Romanized Hindi Normalization (optional)
       ↓
Tokenizer (SentencePiece)
       ↓
XLM-RoBERTa
       ↓
Token Classification Head
       ↓
Language label per token
```

---

## Dataset

This project uses publicly available code-mixed datasets.

### GLUECoS
A benchmark dataset for **Hindi-English code-switched NLP tasks** with token-level language labels.

### FIRE Shared Task Datasets
Social media datasets containing noisy code-mixed text annotated for language identification.

### Dakshina Dataset
A transliteration dataset used to design the **Romanized Hindi normalization strategy**.

---

## Repository Structure

```
code-mixed-lid-research/
│
├── data/
│   ├── raw/               # Original downloaded datasets
│   └── processed/         # Preprocessed datasets
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   └── 02_fragmentation_analysis.ipynb
│
├── src/
│   ├── data_loader.py
│   ├── normalizer.py
│   ├── metrics.py
│   └── model.py
│
├── scripts/
│   ├── train_baseline.py
│   ├── train_normalized.py
│   └── evaluate.py
│
├── requirements.txt
└── README.md
```

---

## Experiments

### 1. Baseline Model
XLM-RoBERTa trained directly on raw code-mixed text.

### 2. Normalization-Enhanced Model
The same model trained on text processed by the **Romanized Hindi normalization pipeline**.

---

## Tokenizer Fragmentation Analysis

A secondary experiment analyzes **subword token fragmentation**.

Metric:

```
Average number of subword tokens per word
```

Goal:

Measure how normalization reduces fragmentation produced by the tokenizer.

Example:

| Setting | Avg Subwords per Token |
|--------|-------------------------|
| Raw text | 2.1 |
| Normalized text | 1.4 |

---

## Evaluation Metrics

Performance is evaluated using:

- **Macro-F1 Score**
- Token-level Precision / Recall
- Confusion Matrix
- Code-switch boundary detection accuracy
- Performance stratified by **Code-Mixing Index (CMI)**

---

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/code-mixed-lid-research.git
cd code-mixed-lid-research
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Training

Train the baseline model:

```bash
python scripts/train_baseline.py
```

Train the normalization-enhanced model:

```bash
python scripts/train_normalized.py
```

---

## Evaluation

Run evaluation and generate plots:

```bash
python scripts/evaluate.py
```

This script generates:

- confusion matrices
- F1 score reports
- tokenizer fragmentation plots

---

## Visualization Notebooks

Interactive notebooks are available for:

- dataset exploration
- tokenization analysis
- evaluation visualization

```
notebooks/01_data_exploration.ipynb
notebooks/02_fragmentation_analysis.ipynb
```

---

## Key Contributions

- Investigates multilingual transformer performance on **Hindi-English code-mixed language identification**
- Proposes a **Romanized Hindi normalization pipeline**
- Analyzes **tokenizer fragmentation in multilingual models**
- Provides reproducible experiments for code-mixed NLP research

---

## Future Work

Potential extensions include:

- Character-level normalization models
- Additional multilingual transformer comparisons
- Cross-lingual transfer experiments
- Larger code-mixed benchmarks

---

## License

This project is released under the MIT License.

---

## Author

**Prakhar Gupta**  
B.Tech Computer Science | Machine Learning & Multilingual NLP
