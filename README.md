
# Anomaly Detection Model

## Overview
This project implements and evaluates fraud detection models on an audit dataset. It includes a supervised learning approach using a Random Forest Classifier and an unsupervised anomaly detection approach using Isolation Forest. The goal is to classify audit cases as either fraudulent or non-fraudulent based on various user and case-related features.

## Dataset
- The dataset consists of audit records with 26 features such as user ID, role name, organization, audit type, time taken, and location details.
- The target variable is `fraud` (binary): 1 indicates fraudulent activity and 0 indicates no fraud.
- Certain columns like IDs and textual identifiers are dropped during preprocessing.
- Categorical features are encoded using Label Encoding for machine learning compatibility.

## Preprocessing
- Dropped irrelevant ID-type columns which do not contribute to predictive power directly.
- Encoded all categorical columns using `LabelEncoder`.
- Split dataset into training and testing subsets with stratification on the `fraud` label to preserve class distribution.

## Models

### Supervised Model - Random Forest Classifier
- Used as the baseline supervised classifier.
- Hyperparameters include: max depth of 10, minimum samples split of 5, with a fixed random seed for reproducibility.
- Evaluated using accuracy and classification metrics (precision, recall, f1-score).
- Achieved approximately 91% accuracy and an f1-score around 0.90 in detecting fraud.

### Unsupervised Model - Isolation Forest
- Used for anomaly detection without label supervision.
- Trained on the same preprocessed features.
- The contamination parameter was set to the proportion of fraud cases in the training data.
- Predicted anomalies treated as fraud, and normal data points treated as non-fraud.
- Achieved about 80% accuracy with moderate precision and recall on fraud detection.

## Usage
1. Load the dataset from an Excel file.
2. Preprocess the data by dropping unnecessary columns and encoding categorical features.
3. Split the data into train and test sets.
4. Train either the Random Forest (supervised) or the Isolation Forest (unsupervised) model.
5. Predict on the test set and evaluate performance using classification metrics.


## Conclusion
- The supervised Random Forest model outperforms the unsupervised Isolation Forest in accuracy and f1-score.
- Isolation Forest provides a baseline for fraud anomaly detection without requiring labeled data.
- Future work could explore feature engineering, hyperparameter tuning, and other anomaly detection techniques.

***
