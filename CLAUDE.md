# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Customer segmentation analysis project using machine learning. Generates synthetic customer data and applies multiple segmentation methodologies (unsupervised clustering, supervised learning, and hybrid approaches).

## Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Run the notebook
jupyter notebook customer_segmentation.ipynb

# Execute notebook from command line
jupyter nbconvert --to notebook --execute --inplace customer_segmentation.ipynb
```

## Architecture

**Single notebook design** (`customer_segmentation.ipynb`) containing all analysis:

1. **Data Generation** - Creates synthetic dataset with 5,000 customers, 25 features (demographics, purchase behavior, media consumption), and binary target (Product A purchase)

2. **Unsupervised Methods**:
   - K-Means, Hierarchical, DBSCAN, GMM clustering
   - RFM (Recency, Frequency, Monetary) business segmentation

3. **Supervised Methods**:
   - Logistic Regression, Decision Tree, Random Forest, Gradient Boosting
   - SHAP for model explainability

4. **Combined Method**:
   - RFM + Propensity Matrix (3x3 grid)
   - 9 actionable marketing segments
   - Cluster-enhanced prediction model

## Data Files

- `data/customers.csv` - Raw generated dataset
- `data/customers_with_segments.csv` - Dataset with all segment assignments (36 columns)

## Key Segment Columns

- `kmeans_cluster`, `hierarchical_cluster`, `gmm_cluster` - Unsupervised labels
- `rfm_segment` - RFM business segments (Champions, Loyal Customers, etc.)
- `propensity_segment` - ML-based propensity tiers
- `action_segment` - Final actionable marketing segments (VIP, Rising Star, Hidden Gem, etc.)
