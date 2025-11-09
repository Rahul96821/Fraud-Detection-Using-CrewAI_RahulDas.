# Fraud Detection on PaySim Dataset

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 🔍 Project Overview

This repository contains an exploratory data analysis (EDA) and anomaly detection workflow applied to the **PaySim synthetic financial transactions dataset** from Kaggle. The objective is to identify suspicious transactions such as large `TRANSFER` or `CASH_OUT` events and balance inconsistencies, generating actionable insights and a fraud-detection report.

## 📁 Dataset

* **Dataset Name**: Synthetic Financial Datasets for Fraud Detection (PaySim)
* **Source**: [Kaggle – PaySim1](https://www.kaggle.com/datasets/ealaxi/paysim1)
* **Files**: `PS_20174392719_1491204439457_log.csv` (or similar)
* **Key Columns**:

  * `step` – time step of the transaction
  * `type` – type of transaction (e.g., PAYMENT, TRANSFER, CASH_OUT, etc.)
  * `amount` – transaction amount
  * `nameOrig` – customer account initiating the transaction
  * `oldbalanceOrg`, `newbalanceOrig` – origin account balance before and after
  * `nameDest` – account receiving the transaction (could be merchant or customer)
  * `oldbalanceDest`, `newbalanceDest` – destination account balance before and after
  * `isFraud`, `isFlaggedFraud` – binary labels indicating fraud or flagged fraud by the simulation

## 🧠 Analysis Goals

1. Load and profile the dataset: number of rows, columns, data types, missing values, sample rows.
2. Focus on suspicious transaction types: `TRANSFER`, `CASH_OUT`.
3. Flag large-value transactions (threshold configurable, e.g., > $10,000).
4. Identify balance inconsistencies: where `oldbalanceOrg − amount ≠ newbalanceOrig`, or `oldbalanceOrg < amount`.
5. Generate a structured report summarizing anomalies with row indices and explanations.
6. Provide recommendations for fraud detection processes and monitoring based on findings.

## 🛠 Repository Structure

```
/      
├─ data/                         
│    └─ paysim_log.csv           # Raw dataset (download from Kaggle)  
├─ notebooks/                    
│    └─ analysis.ipynb            # Jupyter notebook for EDA and anomaly detection  
├─ scripts/                      
│    └─ analyze_fraud.py          # Python script to automate anomaly detection and export results  
├─ output/                       
│    ├─ anomalies.csv             # CSV of flagged anomaly rows  
│    └─ fraud_report.md           # Generated Markdown report  
├─ README.md                      # This file  
└─ LICENSE                        # MIT License  
```

## 📦 Usage

1. Download the dataset from Kaggle and place it in the `data/` folder with name `paysim_log.csv`.
2. Create a Python environment:

   ```bash
   pip install pandas
   ```
3. Run the analysis script:

   ```bash
   python scripts/analyze_fraud.py
   ```

   This will generate `anomalies.csv` in `output/` and `fraud_report.md`.
4. Open `output/fraud_report.md` to view the summary and findings.

## 📋 Findings Summary

*(Fill this section with top findings once the analysis is complete, e.g., total rows, number of anomalies, most common transaction types flagged, threshold used.)*

## 🎯 Recommendations

* Set up real-time monitoring for high-value `TRANSFER` and `CASH_OUT` events.
* Implement alerting when origin account’s new balance drops to zero immediately after large transactions.
* Incorporate balance inconsistency checks into your fraud detection model (e.g., `oldbalanceOrg < amount`, `oldbalanceOrg − amount ≠ newbalanceOrig`).
* Periodically review flagged transactions manually and refine thresholds based on institutional risk appetite.
