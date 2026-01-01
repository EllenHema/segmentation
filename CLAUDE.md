# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Customer analytics project using machine learning for segmentation, CLV prediction, and churn analysis. Uses synthetic customer data to demonstrate multiple analytical methodologies.

## Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Run notebooks interactively
jupyter notebook

# Execute full pipeline (must run in order)
jupyter nbconvert --to notebook --execute --inplace customer_segmentation.ipynb
jupyter nbconvert --to notebook --execute --inplace clv_analysis.ipynb
jupyter nbconvert --to notebook --execute --inplace churn_prediction.ipynb
jupyter nbconvert --to notebook --execute --inplace feedback_loop.ipynb
```

## Architecture

**Four-notebook pipeline** with sequential dependencies:

### 1. `customer_segmentation.ipynb` (Start here)
Generates synthetic data and applies segmentation methods.
- **Input:** None (generates data)
- **Output:** `data/customers.csv`, `data/customers_with_segments.csv`
- Unsupervised: K-Means, Hierarchical, DBSCAN, GMM, RFM
- Supervised: Logistic Regression, Decision Tree, Random Forest, Gradient Boosting + SHAP
- Combined: RFM + Propensity Matrix → 9 actionable marketing segments

### 2. `clv_analysis.ipynb`
Calculates and predicts Customer Lifetime Value.
- **Input:** `data/customers_with_segments.csv`
- **Output:** `data/customers_with_clv.csv`
- Simple CLV formula, RFM-weighted CLV, ML-predicted CLV (Gradient Boosting)
- Creates CLV tiers (Bronze → Diamond)

### 3. `churn_prediction.ipynb`
Predicts customer churn and creates prioritization matrix.
- **Input:** `data/customers_with_clv.csv`
- **Output:** `data/customers_final.csv`
- Creates churn risk score and binary churn label
- Models: Logistic Regression, Random Forest, Gradient Boosting + SHAP
- CLV-Churn Integration Matrix for prioritized actions

### 4. `feedback_loop.ipynb`
Implements closed-loop monitoring and optimization.
- **Input:** `data/customers_final.csv`
- **Output:** `data/feedback_metrics.csv`, `data/campaign_results.csv`
- Segment Evolution Tracking: transition matrices, retention rates
- Campaign Performance Simulation: A/B test simulation with lift/ROI
- Model Monitoring & Drift Detection: AUC degradation, feature drift alerts
- A/B Testing Framework: sample size calculator, power analysis

## Data Files

- `data/customers.csv` - Raw generated dataset (5,000 customers, 25 features)
- `data/customers_with_segments.csv` - With segment assignments
- `data/customers_with_clv.csv` - With CLV columns added
- `data/customers_final.csv` - Complete dataset with all analyses
- `data/feedback_metrics.csv` - Model monitoring metrics over time
- `data/campaign_results.csv` - Simulated campaign performance results

## Key Output Columns

- `kmeans_cluster`, `hierarchical_cluster`, `gmm_cluster` - Unsupervised labels
- `rfm_segment` - Business segments (Champions, Loyal Customers, etc.)
- `action_segment_3d` - Actionable marketing segments (VIP, Rising Star, etc.)
- `clv_predicted`, `clv_tier` - Customer lifetime value and tier
- `churn_probability`, `churn_risk_segment` - Churn predictions
- `clv_churn_action` - Prioritized action (URGENT: VIP Win-Back, etc.)
