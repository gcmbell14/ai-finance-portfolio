# AI-Driven Fraud Detection System

## Business Problem
Fraudulent transactions in financial services cause significant financial and reputational losses. Traditional detection methods lack real-time capabilities.

## Solution
An AI-based anomaly detection model using **Azure AI Anomaly Detector** and a **Power BI real-time dashboard** to flag suspicious transactions instantly.

## Dataset
[Kaggle Credit Card Fraud Dataset](https://www.kaggle.com/mlg-ulb/creditcardfraud) (284,807 transactions, 492 fraudulent).

## Technical Stack
- **Languages:** Python (Pandas, Scikit-learn), SQL
- **AI Platform:** Azure AI Anomaly Detector
- **Visualization:** Power BI
- **Integration:** Azure Functions for real-time scoring

## Process
1. Load transaction data into Azure SQL Database.
2. Train anomaly detection model in Azure Machine Learning.
3. Deploy model as an API endpoint.
4. Connect API to Power BI for live monitoring.

## Results
- Achieved **0.98 AUC** for fraud detection.
- Reduced detection latency from hours to <5 seconds.

## Screenshots
![Fraud Dashboard](../visuals/fraud-workflow.png)
