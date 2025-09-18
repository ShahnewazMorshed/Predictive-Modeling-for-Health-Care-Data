# Predictive Modeling of Hospital Length of Stay (LOS) Using Statistical and Machine Learning Approaches

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/release/python-390/)

**Author:** Mohammad Shahnewaz Morshed  
**Date:** 10 March 2024  

---

A statistical framework was developed to predict how long patients are likely to stay in the hospital at the time they are admitted. This matters because length of stay (LOS) affects how hospitals plan for beds, staff schedules, medicines, and supplies. Hospital stays are always counted in whole days, and the data usually show a right-skewed pattern: most patients stay only a few days, but some stay much longer. Traditional models often struggle with this kind of data because the variation (spread of values) is greater than the average stay. To handle this, special count-based models were applied that can cope with extra variability. In addition, the data showed that a large number of patients had very short stays, such as same-day or one-day discharges. To capture this, mixture models (zero-inflated approaches) were used, which can separate these short stays from the longer ones. By combining these methods, the framework produced more accurate predictions. These forecasts can help hospitals make smarter decisions about resource allocation, reduce overcrowding, and improve both patient care and operational efficiency.

---

## Objectives

- Describe the distribution of hospital length of stay (LOS) and identify key statistical features such as skewness, overdispersion, and short stays.

- Develop predictive models using both statistical (Poisson, Negative Binomial, Zero-Inflated) and machine learning methods (Random Forest, Gradient Boosting, XGBoost).

- Evaluate model performance and interpretability with accuracy metrics and Shapley-based explanations of predictor importance.

- Translate predictions into operational insights for effective planning and operational efficiency.

---

## Methodology

The analysis first employed Poisson regression as the canonical model for count data, extended to Negative Binomial for overdispersion handling, and Zero-Inflated variants for excess short stays. Penalized regression (LASSO/Elastic Net) is applied for feature selection in high-dimensional spaces. Tree-based ensemble learning approaches were applied to capture complex nonlinear patterns.

For full details, [Methodology PDF](Methodology.pdf).

---

## Project Structure

- **Notebooks:**
  - [Notebook 01 – Statistical Characterization of LOS](https://github.com/ShahnewazMorshed/Predictive-Modeling-for-Health-Care-Data/blob/main/Notebook%2001%20-%20Statistical%20characterization%20of%20LOS.ipynb)
: Univariate/bivariate analysis, GLM baseline (Poisson/NB).
  - [02. Development and validation of predictive machine learning models.ipynb](02.%20Development%20and%20validation%20of%20predictive%20machine%20learning%20models.ipynb): Ensemble models, hyperparameter tuning, cross-validation.
  - [03. Derivation of operational insights and policy implications.ipynb](03.%20Derivation%20of%20operational%20insights%20and%20policy%20implications.ipynb): SHAP explanations, business insights.
  - [04. Deployment readiness and integration.ipynb](04.%20Deployment%20readiness%20and%20integration.ipynb): Model persistence (Pickle/Joblib), pipeline integration.

- **Data:** A healthcare facility dataset with features like age, admission type, severity, etc. (not included; synthetic or proprietary).
