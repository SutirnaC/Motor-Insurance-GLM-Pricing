# Motor-Insurance-GLM-Pricing
Repository containing my personal project of Motor Insurance Pricing using GLM

## 📊 Executive Summary
This repository contains a complete, end-to-end modernized multivariate pricing engine for a Comprehensive Personal Motor Insurance portfolio. 

In highly commoditized, aggregator-driven markets, outdated one-way tariff structures lead to adverse selection—overpricing low-risk drivers and underpricing high-risk drivers. This project solves that by replacing a legacy pricing model with a multivariate **Generalized Linear Model (GLM)** framework to accurately calculate the technical pure premium (risk cost) and eliminate cross-subsidization.

### Key Business Outcomes:
* **Targeted Rate Adequacy:** Identified a 25% underpricing in the "Urban, Young Driver" segment.
* **Margin Protection:** Developed a rate-capping strategy (+10% maximum annual increase) to correct margins while protecting portfolio retention.
* **Pricing Accuracy Lift:** Achieved a high Gini Coefficient out-of-sample, proving superior risk differentiation compared to the baseline tariff.

---

## 📁 Repository Structure

```text
/Motor-Pricing-GLM
│
├── data/
│   ├── synthetic_data_generator.py          # Script to generate realistic policy & claims data
│   └── motor_pricing_data.csv               # 50k policies with injected heterogeneity & outliers
│
├── notebooks/
│   ├── 01_Exploratory_Data_Analysis.ipynb   # Exposure-weighted marginal summaries & banding
│   ├── 02_GLM_Frequency_Severity.ipynb      # Poisson & Gamma GLM training and feature engineering
│   └── 03_Model_Validation.ipynb            # Gini coefficients, Lorenz curves, and Lift charts
│
├── dashboard/
│   └── Executive_Pricing_Dashboard.pbix     # Power BI dashboard for stakeholder A/E reporting
│
└── README.md


Methodology & Actuarial Framework

1. Data EngineeringSynthetic Generation: Built a dataset of 50,000 policies incorporating realistic actuarial dynamics: non-linear risk curves, missing data (legacy broker systems), exact zeros, and heavy-tailed severity outliers.

Treatment: Implemented exposure-preserving missing value imputation and 99th-percentile large loss capping to stabilize severity models.

2. GLM ArchitectureFrequency Model: Poisson distribution with a Log link function. Offset by $\ln(\text{Exposure})$ to ensure exact linear scaling with time on risk.

Severity Model: Gamma distribution with a Log link function. Weighted by claim count, ensuring the constant coefficient of variation assumption holds true for average claim costs.

Pure Premium: Derived via the multiplicative combination of predicted frequency and expected severity.

3. Validation StrategyOut-of-Sample Testing: Standard 70/30 train-test split.

Lorenz Curve & Gini Index: Used to quantify the model's ability to rank-order risk effectively.

Double Lift Charts: Validated that the new GLM safely out-selects the old tariff model by charting Actual Loss Ratios across price-dislocation deciles.

How to Run the Project

Clone the repository:

Bash

git clone [https://github.com/yourusername/Motor-Pricing-GLM.git](https://github.com/yourusername/Motor-Pricing-GLM.git)
cd Motor-Pricing-GLM

Install required dependencies:
Bash

pip install pandas numpy statsmodels scikit-learn matplotlib seaborn

Generate the data & run the notebooks:

Execute the synthetic_data_generator.py script first, then proceed through the Jupyter Notebooks sequentially.

Future ExtensionsMachine Learning Challengers: Implementing an XGBoost model to automatically surface complex interaction terms (e.g., Age $\times$ Vehicle Power) to feed back into the interpretable GLM.

Price Elasticity Modeling: Building a Logistic Regression retention model to optimize commercial pricing beyond the technical pure premium.

Bayesian Credibility: Applying PyMC for hierarchical modeling to dynamically credibility-weight rural geographic segments with sparse data.
