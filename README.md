# Hybrid Phishing Detection System

This project implements a multi-layered approach to URL classification by combining Deep Learning and Traditional Machine Learning into an ensemble "meta-model."

## System Architecture

The system utilizes a hybrid approach to capture both structural patterns and semantic sequences:

1.  **Deep Learning (Neural) Branch**: A **CNN + Bidirectional LSTM** model that processes raw URL character sequences[cite: 1].
2.  **Traditional ML Branch**: A **Random Forest** classifier trained on extracted lexical features[cite: 1].
3.  **Ensemble Meta-Model**: A **Logistic Regression** model that acts as a blender, taking the prediction probabilities of the first two models to output a final result[cite: 1].

## Key Features
*   **Lexical Extraction**: Captures URL length, digit counts, special characters, and entropy[cite: 1].
*   **Sequence Processing**: Tokenizes URLs at the character level with numerical padding[cite: 1].
*   **Web Deployment**: Includes a **Streamlit** application integrated with `pyngrok` for real-time URL testing[cite: 1].

## Evaluation Metrics
*   **Classification Report**: Precision, Recall, and F1-Score for legitimate and phishing classes[cite: 1].
*   **ROC AUC**: Measures the model's ability to distinguish between classes[cite: 1].
*   **Confusion Matrix**: Visualizes true/false positives and negatives[cite: 1].

# Multi-Feature URL Phishing Detection

A robust machine learning pipeline that leverages URL-based, Domain-based, and Content-based features to detect malicious websites.

## Feature Engineering Overview
The model relies on three core categories of features:
*   **URL (Lexical)**: Structure analysis including dots, slashes, and hostname length.
*   **Domain-Based**: Uses WHOIS lookups to determine **Domain Age** and **Registration Length**.
*   **Content-Based**: Analyzes HTML for forms, iframes, and external link ratios.

## Optimization & Results
*   **Feature Selection**: Used **Recursive Feature Elimination (RFE)** with Random Forest to identify the top 15 predictors.
*   **Top Predictors**: URL length, depth, domain age, and special character counts were found most significant.
*   **Best Model**: **Random Forest** achieved the highest F1-Score (0.8571) and Cross-Validation Accuracy (0.8690).

## Performance Comparison
| Model | F1-Score | Key Strength |
| :--- | :--- | :--- |
| **Random Forest** | 0.8571 | Best overall balance and generalization |
| **SVM** | ~0.84 | Highest Recall for identifying phishing |
| **Naive Bayes** | Lowest | Poor fit for this specific feature set |

## Usage
The system includes a `predict_url` pipeline that handles raw URL input, feature extraction, scaling via `StandardScaler`, and final prediction.
