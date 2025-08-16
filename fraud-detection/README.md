# 🛡️ AI-Driven Fraud Detection (30-sec overview)

**What it is:** Real-time fraud alerts with a **Top-K review budget** and **reason codes** so analysts focus on the highest-risk transactions.

**Business impact**
- Cut alert noise while keeping catch rate (Top-K aligned to analyst capacity)
- Clear **reason codes** (“amount 9× baseline”, “3,200km hop”, “device change”) speed decisions
- Live triage table + CSV export for ops handoff

**Results (demo)**
- Precision@100: ~25–35% on backtests  
- Median inference: <1s  
- Daily alert budget: K = 100 (configurable)

**See it live:** Fraud tab in the hero app → https://github.com/gcmbell14/ai-compliance-risk-insights  
**Screenshot:**  
![Fraud Dashboard](../visuals/fraud-workflow.png)

<details>
  <summary><strong>Details (features, modeling, governance, tests)</strong></summary>

## Features (MVP)
- `amount_zscore_by_customer`, `distance_from_last_km`, `device_change`, `is_foreign`, `hour`, `merchant_id/mcc`, `amount`  
*Next: velocity features like `txn_count_1h/24h`, `sum_amount_24h`.*

## Modeling
- **Unsupervised** (Isolation Forest / Azure Anomaly Detector) → 0–100 risk → **Top-K** alerts  
- **Supervised** (LogReg/LightGBM) if labels exist → optimize **Precision@K** + **PR-AUC**  
- **Hybrid:** anomaly score as a feature

## Dataset
- Public: Kaggle Credit Card Fraud (highly imbalanced)  
- Or synthetic transactions (no PII) with velocity/geo/device signals

## Tech stack
- Python (pandas, scikit-learn), SQL; Streamlit or Power BI  
- Optional Azure pieces: Azure ML, Azure AI Anomaly Detector, Azure Functions (API), Azure SQL/Blob, Key Vault, App Insights

## Governance & Auditability
- Redact PAN/PII; tokenized IDs in logs/SHAP  
- Log `model_version`, threshold/K, approver; monitor drift; maintain exception register

## Test scenarios (UAT)
- **Impossible travel:** 5 min apart, 3,000+ km → risk > 90  
- **Night high-amount:** 3am, 8× baseline → risk > 80  
- **Device swap + foreign:** `device_change=1` & `is_foreign=1` → risk > 85  
- **Benign:** small local grocery, same device → risk < 20

## Next steps
- Add velocity features & calibration; add **Precision@K** readout; swap to Azure ML endpoint

</details>
