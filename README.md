# Phishing Detection via Machine Learning

This project establishes a comprehensive pipeline for identifying malicious URLs using advanced feature engineering and comparative model analysis.

---

## 1. Environment & Data Acquisition

- **Libraries & Tools**
  - `python-whois`, `tld`
  - `scikit-learn`, `pandas`, `numpy`

- **Dataset**
  - Source: Kaggle
  - File: `dataset_phishing.csv`

- **Target Mapping**
  - `status → binary label`
    - `0 → Legitimate`
    - `1 → Phishing`

---

## 2. Multi-Dimensional Feature Extraction

- **Core Function**
  - `extract_all_features()` → Aggregates all feature types

### (a) URL (Lexical) Features
- URL length
- URL depth
- Presence of:
  - `@` symbol
  - IP address
  - Dots (`.`)
  - Hyphens (`-`)

### (b) Domain-Based Features
- Domain Age
- Registration Length
- WHOIS lookup integration
- Robust handling:
  - Timeout management
  - Exception handling

### (c) Content-Based Features
- Number of:
  - Links
  - Scripts
- Presence of:
  - Forms
  - iFrames
- External link ratio

---

## 3. Preprocessing & Feature Selection

### (a) Data Cleaning
- Missing values (`-1`) handled using:
  - **Median Imputation**

### (b) Data Splitting
- Train-Test Split:
  - `80% → Training`
  - `20% → Testing`
- **Stratified Sampling** applied

### (c) Feature Scaling
- `StandardScaler` used for normalization

### (d) Feature Selection
- Method: **Recursive Feature Elimination (RFE)**
- Model: Random Forest
- Top Features Identified:
  - `url_length`
  - `hostname_length`
  - `path_length`
  - `domain_age`
  - (Top 15 predictors selected)

---

## 4. Model Performance & Results

### Evaluation Method
- **10-Fold Stratified Cross-Validation**

| Model                | F1-Score | Interpretation |
|---------------------|----------|----------------|
| Random Forest       | 0.8571   | Top performer; highest accuracy (0.8690) |
| SVM                 | ~0.84    | High recall (0.8854), strong phishing detection |
| Gradient Boosting   | High     | Competitive with Random Forest |
| Logistic Regression | Moderate | Decent but weaker than ensembles |
| Naive Bayes         | Lowest   | Least effective |

---

## 5. Deployment Pipeline

### Core Function
- `analyze_and_predict_url()`

### Workflow
Input URL
↓
Feature Extraction
↓
Scaling (StandardScaler)
↓
Model Prediction (Random Forest)
↓
Output:

Classification (Phishing / Legitimate)
Confidence Score



### Model Persistence
- Saved using `joblib`:
  - Trained Random Forest model
  - Scaler
  - Selected feature list

---

## Key Features

- End-to-end automated pipeline
- Multi-dimensional feature engineering
- Robust error handling (WHOIS failures)
- High accuracy with ensemble models
- Production-ready prediction function

---

## Applications

- Browser security extensions
- Email phishing filters
- Cybersecurity monitoring systems
- Enterprise threat detection pipelines
