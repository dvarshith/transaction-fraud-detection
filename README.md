# Transaction Fraud Detection

[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Sklearn%2C%20XGBoost%2C%20LGBM-green)](https://scikit-learn.org/)
[![License](https://img.shields.io/badge/License-YourChoice-blue.svg)](LICENSE)

<br/>

## Overview

This repository contains a **fraud detection** pipeline for financial transactions, leveraging **data preprocessing**, **feature engineering**, **class imbalance handling (SMOTE)**, and a **diverse set of machine learning models** (Logistic Regression, Random Forest, LightGBM, CatBoost, XGBoost, and ensemble methods). 

**Highlights**:
- **Novel feature engineering** (time-based features, transaction amount bucketing, etc.)
- **Handling imbalanced data** via SMOTE
- **Boosting algorithms** (LightGBM, XGBoost, CatBoost) for high-dimensional data
- **Advanced neural network approach** with a supervised AutoEncoder for anomaly detection
- **Stacking and voting ensembles** for robust, high AUC-ROC performance

Our best model (LightGBM) achieved **AUC-ROC of 0.89** on the Vesta Corporation dataset.

<br/>

## Data

We use the **Vesta Corporation dataset** (part of a Kaggle competition) (https://www.kaggle.com/competitions/ieee-fraud-detection/overview) which includes:
- **Transaction data** (TransactionID, card info, transaction amount, time, etc.)
- **Identity data** (Device info, etc.)

**Due to size and privacy concerns,** the real dataset is **not** included in this repo.

**Key columns**:
- `TransactionID`
- `isFraud` (target)
- `TransactionDT`, `TransactionAmt`
- Category features (ProductCD, card1, card2, etc.)
- Identity features (DeviceType, DeviceInfo)
 
<br/>

## Methodology
1. **Data Preprocessing**  
   - Missing value imputation  
   - High-correlation feature removal (via correlation heatmap)  
   - Encoding categorical features (one-hot or label encoding)
2. **Feature Engineering**  
   - **Transaction amount bucketing** (micro, small, etc.)  
   - **Time-based features** (day-of-week, hour-of-day)  
   - **Email domain grouping** (e.g., major providers vs. niche)
3. **Handling Class Imbalance**  
   - **SMOTE** (Synthetic Minority Oversampling Technique) to oversample the minority (fraud) class.
4. **Model Training**  
   - **Logistic Regression**, **Random Forest** (baselines)  
   - **LightGBM**, **CatBoost**, **XGBoost** (boosting methods)  
   - Hyperparameter tuning via Bayesian Optimization  
   - AUC-ROC as primary metric
5. **Ensemble Methods**  
   - **Voting** (soft voting across LGBM, CatBoost, XGB, etc.)  
   - **Stacking** with a meta-learner
6. **AutoEncoder** (Optional Neural Approach)  
   - A supervised autoencoder that outputs fraud probability (or uses reconstruction error).

<br/>

## Results
```
| Model         | AUC-ROC |
|---------------|---------|
| Logistic Reg  | 0.80    |
| Random Forest | 0.855   |
| LightGBM      | **0.89**   |
| CatBoost      | 0.881   |
| XGBoost       | 0.874   |
| Voting Ensembles | ~0.86  |
| Stacking      | 0.88    |
| AutoEncoder   | 0.86    |
```
**LightGBM** emerges as the top performer with **0.89** AUC-ROC, balancing speed and accuracy on this high-dimensional dataset. 

<br/>

## Usage
1. **Clone the repo**:
   ```
   git clone https://github.com/YourUser/transaction-fraud-detection.git
   cd transaction-fraud-detection
   ```
2. **Set up environment**:
   ```
   conda create -n fraud python=3.8
   conda activate fraud
   pip install -r requirements.txt
   ```
   (Create a requirements.txt if you like.)
3. **Jupyter Notebook**:
   ```
   jupyter notebook notebooks/main.ipynb
   ```
   Adjust paths as needed to point to your dataset.

<br/>

## Next Steps
- Explore other techniques for class imbalance (e.g., ADASYN, cost-sensitive learning).
- Investigate deeper neural network architectures or specialized anomaly detection methods.
- Implement real-time streaming pipelines (Spark Streaming, Kafka) for transaction-level fraud detection.

</br>

## Acknowledgments
- Dataset by Vesta Corporation [https://www.kaggle.com/competitions/ieee-fraud-detection/overview].

 </br>

## License
This project is released under the `MIT License`. That means you’re free to use, modify, and distribute the code, but you do so at your own risk.

 </br>

## Contact
Author: Varshith Dupati </br>
GitHub: @dvarshith </br>
Email: dvarshith942@gmail.com </br>
Issues: Please open an issue on this repo if you have questions or find bugs. </br>
